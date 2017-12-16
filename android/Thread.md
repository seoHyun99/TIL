# [Android] Thread

## Thread 특징
- 프로세스 내의 정보들의 공유가 쉽다.
- Thread간 서로 공유하는 자원
  * 작업디렉토리
  * 파일지시자들
  * 대부분의 전역변수와 데이터들
  * UID, GID
  * signal

- Thread가 고유하게 가지는 자원
  * 에러번호(errno)
  * Thread 우선 순위
  * 스택
  * Thread ID
  * 레지스터 및 스택 지시자

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

### 3. Thread 종료 방법
#### 3-1. flag 이용
: while문 안에서 지속적으로 flag(ex.boolean)를 체크해준다.

**Thread 종료 예제 1**

    private class ExampleThread extends Thread {
      private boolean flag = false;

      public ExampleThread() {
         // 초기화 작업
      }

      public void run() {
        while(flag) {
          // Thread에게 수행시킬 동작들 구현
        }
      }

      public void setThreadState(boolean flag) {
        this.flag = flag;
      }
    }

#### 3-2. interrupt 이용
: 현재 수행중인 명령을 중지시키는 interrupt()를 이용한다.
: interrupt() 호출 시점에 wait(...), join(...), sleep(...) 메소드가 호출되면 interruptedException이 발생한다.

**Thread 종료 예제 2**

    public class ThreadTest extends Activity {
      protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ExampleThread thread = new ExampleThread();
        thread.start();
      }
    }

#### 추가
Thread.stop()과 Thread.destroy()와 같은 메소드가 존재는 하나, deprecated 되었다. stop의 경우 동작중 정지하게 되면 객체의 안전성을 보장하지 못하고, 이로 인해 손상된 객체가 임의의 동작을 할 수 있는 위험성이 있다. destroy는 dead-lock 상태에 빠질 위험이 크다고 알려져 있다.
(참조 : https://docs.oracle.com/javase/1.5.0/docs/guide/misc/threadPrimitiveDeprecation.html)


## Main Thread란?
: 같은 프로세스에서 실행되는 모든 구성 요소는 UI Thread에서 시작되고, 각 구성 요소를 호출하는 시스템이 해당 Thread에서 발송된다.
: 안드로이드의 이벤트 생성 및 처리를 담당한다.  
: 발생되는 여러 이벤트를 그와 관련된 위젯으로 연동시킨다. **→ UI Thread라 불리운다.**
: UI Thread가 일정 시간 이상 차단되어있으면, ANR이 발생한다.

### Main Thread와 관련된 것들
: 시스템 콜백에 반응하는 메소드들은 프로세스의 UI thread에서 동작한다.
> 시스템 콜백에 반응 하는 메소드 ex.onKeyDown() 또는 LifeCycle과 관련된 메소드
