# [Android] Context

## Context란?

: **Context**, Android Developers에는 이렇게 나와있다.

> Interface to global information about an application environment. This is an abstract class whose implementation is provided by the Android system. It allows access to application-specific resources and classes, as well as up-calls for application-level operations such as launching activities, broadcasting and receiving intents, etc.

:  앱 환경에 대한 전역적인 정보를 담고 있는 Interface이다. 이것은 하나의 추상클래스로 Context의 실행은 Android system에 의해 제공된다. 이것은 Application 별 리소스와 클래스들에 대한 액세스는 물론 launching activities, broadcasting, receiving intents와 같은 application 레벨에 대한 호출을 허용한다.

Android에서 Context를 **Application Context** 와 **Activity Context** 로 구분지을 수 있다.

### 0. Context 가져오기
- **View.getContext() / this**  
: 현재 실행되고 있는 View의 context를 리턴
- **Activity.getApplicationContext() / getApplication()**  
: 어플리케이션의 Context가 return된다.
- **ContextWrapper.getBaseContext()**  
: 다른 Context를 access하려 할 때 사용한다. ContextWrapper는 getBaseContext()를 경유해서 Context를 참조할 수 있다.


### 1. Application Context
1. Application Lifecycle에 영향을 받는다.  
2. Application이 실행되어 종료될 때까지 동일한 객체이다. -> **Singleton**  
3. 액티비티 또는 서비스의 getApplication(), Context에서 상속한 다른 객체의 getApplicationContext()와 같은 메소드를 통해 액세스 할 수 있다.
4. 액세스하는 위치나 방법에 관계없이 항상 프로세스 내에서 동일한 인스턴스를 수신한다.

#### 1-1. getApplicationContext()와 getApplicationContext()의 차이
1. getApplication()과 getApplicationContext()는 리턴하는 형이 다르다. getApplication()은 Application을, getApplicationContext()는 현재 프로세스의 global Application Context를 반환한다. 따라서 Manifest에 등록된 Application 클래스를 원한다면, getApplicationContext()를 사용해 Application 클래스로 캐스팅하면 안 된다.

2. getApplication()은 Activity 클래스와 Service 클래스에서만 사용이 가능하지만, getApplicationContext()는 Context 클래스에 정의되어있다.



### 2. Activity Context
1. Activity Lifecycle에 영향을 받는다.  
2. Activity가 onDestroy()된 경우 사라질 수 있는 객체이다.  
3. getContext(), ActivityName.this를 통해 참조할 수 있다.

### 3. Context 참조하기

    // 안좋은 예시
    public class CustomManager {
        private static CustomManager sInstance;

        public static CustomManager getInstance(Context context) {
            if (sInstance == null) {
                sInstance = new CustomManager(context);
            }

            return sInstance;
        }

        private Context mContext;

        private CustomManager(Context context) {
            mContext = context;
        }
    }

#### 위 클래스를 Activity나 Service처럼 생명주기가 있는 클래스에서 참조하면 어떻게 될까?

코드 내의 sInstance가 정적 참조이기 때문에 시스템에서 객체가 GC가 될 수 없음을 의미한다.  
**→ 메모리 누수가 발생한다.**

    public class CustomManager {
        private static CustomManager sInstance;

        public static CustomManager getInstance(Context context) {
            if (sInstance == null) {
                // 고쳐진 부분
                sInstance = new CustomManager(context.getApplicationContext());
            }

            return sInstance;
        }

        private Context mContext;

        private CustomManager(Context context) {
            mContext = context;
        }
    }

context를 Application Context를 참조하면 된다.   
Application Context는 Singleton이기 때문에 다른 정적 참조를 걸어도 메모리 누수가 생길 일이 없다.
