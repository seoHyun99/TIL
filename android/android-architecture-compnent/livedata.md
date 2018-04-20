# 1. LiveData
> LiveData is a data holder class that can be observed within a given lifecycle. This means that an Observer can be added in a pair with a LifecycleOwner, and this observer will be notified about modifications of the wrapped data only if the paired LifecycleOwner is in active state.

### 공식 문서
* [가이드](https://developer.android.com/topic/libraries/architecture/livedata.html)
* [레퍼런스](https://developer.android.com/reference/android/arch/lifecycle/LiveData.html)

### 사용시 이점
1. Obserevers를 통해 데이터가 변경되는 경우 즉각적으로 수행할 수 있어 UI가 데이터 상태와 일치하는 것을 보장한다.
2. Observers는 Lifecycle Object에 바인딩 되어 있고, destroyed 되는 경우에 알아서 clean up하기 때문에 memory leaks를 피할 수 있다.
3. Observers는 lifecycle이 inactive인 경우 event를 수신하지 않기때문에 에러가 발생할 염려가 없다.
4. lifecycle이 inactive 상태였다 active 상태로 변한 경우 최신 데이터를 수신해 항상 최신의 데이터를 보장한다.

→ LifecycleOwner의 getLifeCycle() 메서드를 통해 현재의 lifecycle을 가져올 수 있어 상태 체크가 가능하다.


## 1-1. Observer
**observeForever(Observer observer)**와 **observe(LifecycleOwner owner, Observer<T> observer)** 를 통해 복수 개의 observer를 추가할 수 있다.

```java
@MainThread
public void observe(@NonNull LifecycleOwner owner, @NonNull Observer<T> observer) {
    if (owner.getLifecycle().getCurrentState() == DESTROYED) {
        // ignore
        return;
    }
    LifecycleBoundObserver wrapper = new LifecycleBoundObserver(owner, observer);
    ObserverWrapper existing = mObservers.putIfAbsent(observer, wrapper);
    if (existing != null && !existing.isAttachedTo(owner)) {
        throw new IllegalArgumentException("Cannot add the same observer"
                + " with different lifecycles");
    }
    if (existing != null) {
        return;
    }
    owner.getLifecycle().addObserver(wrapper);
}

@MainThread
public void observeForever(@NonNull Observer<T> observer) {
    AlwaysActiveObserver wrapper = new AlwaysActiveObserver(observer);
    ObserverWrapper existing = mObservers.putIfAbsent(observer, wrapper);
    if (existing != null && existing instanceof LiveData.LifecycleBoundObserver) {
        throw new IllegalArgumentException("Cannot add the same observer"
                + " with different lifecycles");
    }
    if (existing != null) {
        return;
    }
    wrapper.activeStateChanged(true);
}
```
두 메서드의 파라미터를 보면 LifeCycleOwner를 갖고 있냐 없냐의 차이가 있다.

또한 내부를 보면 wrapper의 클래스가 다른 것을 볼 수 있다.  
observe 메서드를 통해 생성된 wrapper는 **LifecycleBoundObserver** 이고,  
observeForever 메서드를 통해 생성도니 wrapper의 클래스는 **AlwaysActiveObserver** 이다.


두 메서드는 LiveData에 Observer를 추가한다는 공통점을 갖고 있지만,   
observeForever는 항상 activity 상태인 것으로 간주되므로, 이러한 Observer는 removeObserver(Observer)를 수동으로 호출해주어야 한다.
observe를 통해 추가된 Observer는 해당 lifecycle이 STARTED와 RESUME 상태일 때 active 상태로 간주하며,DESTROYED 상태로 전환될 때 자동으로 제거된다.

### 사용 예제
```java
ViewModel mModel = ViewModelProviders.of(this).get(ExampleViewModel.class);
final Observer<String> nameObserver = newName -> {
    //todo:
};
mModel.getCurrentName().observe(this, nameObserver);
```

## 1-2. data를 set시키는 방법
```java
private final Runnable mPostValueRunnable = new Runnable() {
    @Override
    public void run() {
        Object newValue;
        synchronized (mDataLock) {
            newValue = mPendingData;
            mPendingData = NOT_SET;
        }
        //noinspection unchecked
        setValue((T) newValue);
    }
};

protected void postValue(T value) {
    boolean postTask;
    synchronized (mDataLock) {
        postTask = mPendingData == NOT_SET;
        mPendingData = value;
    }
    if (!postTask) {
        return;
    }
    ArchTaskExecutor.getInstance().postToMainThread(mPostValueRunnable);
}
```
```java
@MainThread
protected void setValue(T value) {
    assertMainThread("setValue");
    mVersion++;
    mData = value;
    dispatchingValue(null);
}
```

메인 스레드에서 데이터를 set시킬 때에는 setValue(value)를 이용하고 작업 스레드에서 value를 세팅해야 될 때에는 postValue(value)를 이용해야 한다.

## 1-3. LifeCycleOwner
현재의 Lifecycle을 반환하는 getLifecycle() 메서드를 포함한 인터페이스이다.
> 2018년 1월 22일부터 FragmentActivity와 AppCompatActivity에서 getLifeCycle() 메서드를 지원한다.  
> aac 1.0에서 지원하던 LifecycleActivity 와 LifecycleFragment은 depreaced 되었다.

```java
public interface LifecycleOwner {
    @NonNull
    Lifecycle getLifecycle();
}
```

Lifecycle의 내부는 public enum으로 Event와 State가 있으며,  
Event에는 ON_CREATE, ON_START, ...(resume, pause, stop), ON_DESTORYED와 모든 이벤트인 ON_ANY가 있다.  
STATE에는 DESTROYED, INITIALIZED, CREATED, STARTED, RESUMED의 다섯 가지 STATE가 있다.
