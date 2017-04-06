# [Android] Context

## Context란?

: **Context**, Android Developers에는 이렇게 나와있다.

> Interface to global information about an application environment. This is an abstract class whose implementation is provided by the Android system. It allows access to application-specific resources and classes, as well as up-calls for application-level operations such as launching activities, broadcasting and receiving intents, etc.

:  앱 환경에 대한 전역적인 정보를 담고 있는 Interface이다. 이것은 하나의 추상클래스로 Context의 실행은 Android system에 의해 제공된다. 이것은 Application 별 리소스와 클래스들에 대한 액세스는 물론 launching activities, broadcasting, receiving intents와 같은 application 레벨에 대한 호출을 허용한다.

Android에서 Context를 **Application Context** 와 **Activity Context** 로 구분지을 수 있다.

### 1. Application Context
1. Application Lifecycle에 영향을 받는다.  
2. Application이 실행되어 종료될 때까지 동일한 객체이다. -> **Singleton**  
3. getApplicationContext(), getApplication()을 통해 참조할 수 있다.

### 2. Activity Context
1. Activity Lifecycle에 영향을 받는다.  
2. Activity가 onDestroy()된 경우 사라질 수 있는 객체이다.  
3. getBaseContext(), ActivityName.this를 통해 참조할 수 있다.

### 3. Context 참조하기

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

#### 위 클래스를 Activity나 Servier처럼 생명주기가 있는 클래스에서 참조하면 어떻게 될까?

코드 내의 sInstance가 정적 참조이기 때문에 시스템에서 객체가 GC가 될 수 없음을 의미한다.  
**-> 메모리 누수가 발생한다.**

    public class CustomManager {
        private static CustomManager sInstance;

        public static CustomManager getInstance(Context context) {
            if (sInstance == null) {
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
