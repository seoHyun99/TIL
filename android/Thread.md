# [Android] Thread란?

## Thread 사용법
### 1. 작업이 끝난 후 UI 변경이 필요 없는 경우

    new Thread(new Runnable() {
      @Override
      public void run() {
        //TODO Auto-generated method stub
      }
    }).start();

### 2. Thread 사용법
: Thread 클래스를 **상속** 받는 thread 클래스 생성  
: Thread 내에 run()을 override 한다. run()은 Thread가 실행되면 수행되는 곳이다.  
: Thread 객체를 생성해주고 start() 메소드로 Thread의 run()메소드를 실행시킨다.  

**Thread 클래스 생성 예제**  

    public class ThreadTest extends Activity {
      protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ExampleThread thread = new ExampleThread();
        thread.start();
      }
    }

    private class ExampleThread extends Thread {
      public ExampleThread() {
         // 초기화 작업
      }

      public void run() {
         // Thread에게 수행시킬 동작들 구현
      }
    }

## Main Thread란?
: 안드로이드의 이벤트 생성 및 처리를 담당한다.  
: 발생되는 여러 이벤트를 그와 관련된 위젯으로 연동시킨다. **→ UI Thread라 불리운다.**   

### Main Thread와 관련된 것들
: 시스템 콜백에 반응하는 메소드들은 프로세스의 UI thread에서 동작한다.
> 시스템 콜백에 반응 하는 메소드 ex.onKeyDown() 또는 LifeCycle과 관련된 메소드
