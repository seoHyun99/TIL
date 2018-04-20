## 1. ViewModel
> ViewModel is a class that is responsible for preparing and managing the data for an Activity or a Fragment. It also handles the communication of the Activity / Fragment with the rest of the application

사용하기 위해서는 ViewModel이 Abstract class라 별도의 클래스를 하나 만들고 ViewModel을 상속받는다.

### 공식 문서
* [가이드](https://developer.android.com/topic/libraries/architecture/viewmodel.html)
* [레퍼런스](https://developer.android.com/reference/android/arch/lifecycle/ViewModel.html)

#### 사용시 이점
: 앱이 회전되거나 다시 그려져야하는 경우, UI에 세팅되어 있던 데이터들을 onSaveInstance() 메서드를 통해 원복할 수 있지만 Serializable이 되는 데이터, 소량의 데이터에만 이용하기에 적합하다. 하지만 ViewModel을 이용하면, UI와 내부 로직을 분리할 수 있고, 리소스 관리가 용이해져 메모리를 관리하는데 간편하다는 장점이 있다.


## 1-1. ViewModel 객체 가져오기

ViewModel은 일반적으로 Object를 생성하는 **new** 키워드로 생성하지 않고 **ViewModelProvider** 를 통해서만 가능하다.

#### CustomViewModel
```java
public class ExampleViewModel extends ViewModel {
    private Integer num;

    public Integer getNum() {
        return num;
    }
    public void setNum(int i) {
        this.num = i;
    }
}
```

### 1-1-1. DefaultFactory를 이용해 가져오기
```java
// ExampleViewModel extends ViewModel
ExampleViewModel viewmodel = ViewModelProviders.of(this).get(ExampleViewModel.class);
```

### 1-1-2. CustomFactory를 이용해 가져오기
```java
// CustomViewModelFactory
public class ViewModelFactory implements ViewModelProvider.Factory {
    private final TempData viewModelData;
    public ViewModelFactory(TempData viewModelData) {
        this.viewModelData = viewModelData;
    }

    @NonNull
    @Override
    public <T extends ViewModel> T create(@NonNull Class<T> modelClass) {
        if (modelClass.isAssignableFrom(ExampleViewModel.class)) {
            return (T) new CustomViewModel(viewModelData);
        }
        throw new IllegalArgumentException("Unknown ViewModel class");
    }
}
```

## 1-2. 두 개의 Fragment에서 ViewModel 공유하기

```java
//ViewModel
public class SharedViewModel extends ViewModel {
    private final MutableLiveData<Item> selected = new MutableLiveData<Item>();

    public void select(Item item) {
        selected.setValue(item);
    }

    public LiveData<Item> getSelected() {
        return selected;
    }
}
```
```java
//Fragment
public class MasterFragment extends Fragment {
    private SharedViewModel model;
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        model = ViewModelProviders.of(getActivity()).get(SharedViewModel.class);
        itemSelector.setOnClickListener(item -> {
            model.select(item);
        });
    }
}

public class DetailFragment extends Fragment {
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        SharedViewModel model = ViewModelProviders.of(getActivity()).get(SharedViewModel.class);
        model.getSelected().observe(this, { item ->
           // Update the UI.
        });
    }
}
```

getActivity()를 통해 같은 ViewModelProviders에 같은 Activity를 전달하여, 동일한 ViewModelProvider를 가져온다.  
가져온 ViewModelProvider에서 get(Class class)메소드를 이용하여 같은 ViewModel을 가져온다.



## 1-3. Related Class
### 1-3-1. ViewModelProviders
> Utilities methods for **ViewModelStore** class.

#### important methods
1. static // **of**(Activity(or Fragment) view, ViewModelProvider.Factory Factory)  
: 주어진 Activity 또는 Fragment가 살아있는 동안 ViewModel을 유지하는 ViewModelProvider를 만든다.  
: ViewModelProvider를 리턴한다.

```java
@NonNull
@MainThread
public static ViewModelProvider of(@NonNull FragmentActivity activity,
        @Nullable Factory factory) {
    Application application = checkApplication(activity);
    if (factory == null) {
        factory = ViewModelProvider.AndroidViewModelFactory.getInstance(application);
    }
    return new ViewModelProvider(ViewModelStores.of(activity), factory);
}
```

### 1-3-2. ViewModelProvider
> An utility class that provides ViewModels for a scope.

#### important methods
1. static // **get**(Class<T﻿﻿ 'extends ViewModel> modelClass)  
```java
private static final String DEFAULT_KEY = "android.arch.lifecycle.ViewModelProvider.DefaultKey";
```
```java
@NonNull
@MainThread
public <T extends ViewModel> T get(@NonNull Class<T> modelClass) {
    String canonicalName = modelClass.getCanonicalName();
    if (canonicalName == null) {
        throw new IllegalArgumentException("Local and anonymous classes can not be ViewModels");
    }
    return get(DEFAULT_KEY + ":" + canonicalName, modelClass);
}
```
```java
@NonNull
@MainThread
public <T extends ViewModel> T get(@NonNull String key, @NonNull Class<T> modelClass) {
    ViewModel viewModel = mViewModelStore.get(key);
    if (modelClass.isInstance(viewModel)) {
        //noinspection unchecked
        return (T) viewModel;
    } else {
        //noinspection StatementWithEmptyBody
        if (viewModel != null) {
            // TODO: log a warning.
        }
    }
    viewModel = mFactory.create(modelClass);
    mViewModelStore.put(key, viewModel);
    //noinspection unchecked
    return (T) viewModel;
}
```
: get(Class modelClass) -> get(String key, Class modelClass)를 참조한다.  
: ViewModelStore 내부 HashMap<String, ViewModel>의 값을 get해서 ViewModel을 가져온다.  

### 1-3-3. ViewModelStores
> Factory methods for ViewModelStore class.

#### important methods
1. static // **of**(Activity(or Fragment) view)  
: 주어진 fragment 또는 Activity의 ViewModelStroe를 반환한다.

```java
@NonNull
@MainThread
public static ViewModelStore of(@NonNull FragmentActivity activity) {
    if (activity instanceof ViewModelStoreOwner) {
        return ((ViewModelStoreOwner) activity).getViewModelStore();
    }
    return holderFragmentFor(activity).getViewModelStore();
}
```

holderFragmentFor(activity) 메소드를 통해 HolderFragment를 반환받고 반환받은 HolderFragment를 통해 ViewModelStore를 가져온다.

### 1-3-4. ViewModelStore
> Class to store ViewModels.

```java
private final HashMap<String, ViewModel> mMap = new HashMap<>();
```

ViewModel을 value로 하는 HashMap을 갖고 있으며, 해당 Map의 데이터를 조작할 수 있는 **put(String key, ViewModel viewModel)**, **get(String key)**, **clear()** 메서드를 갖고 있다.

```java
final void put(String key, ViewModel viewModel) {
    ViewModel oldViewModel = mMap.put(key, viewModel);
    if (oldViewModel != null) {
        oldViewModel.onCleared();
    }
}
final ViewModel get(String key) {
    return mMap.get(key);
}

//Clears internal storage and notifies ViewModels that they are no longer used.
public final void clear() {
    for (ViewModel vm : mMap.values()) {
        vm.onCleared();
    }
    mMap.clear();
}
```

## 1-4. 사용시 주의점
: ViewModel은 View의 Lifecycle과 관련이 없기 때문에 ViewModel에서 Activity 등 UI의 Context를 참조하면 MemoryLeaks를 발생시키는 원인이 될 수 있다.  
: Context를 참조해야되는 상황에서는 안드로이드에서 제공해주는 **AndroidViewModel** 클래스를 이용하면 된다.

```java
public class AndroidViewModel extends ViewModel {
    private Application mApplication;
    public AndroidViewModel(Application application) {
        mApplication = application;
    }
    // Return the application.
    public <T extends Application> T getApplication() {
        return (T) mApplication;
    }
}
```
