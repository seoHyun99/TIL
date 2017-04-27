# [Android] Looper

## Looper란?
: Looper는 Message Queue에서 Message나 Runnable 객체를 차례로 꺼내 Handler가 처리하도록 전달한다.  

### 1. Looper의 생성
#### 1-1. Thread 내부에서 Looper 생성
: MainThread가 아닌 새로 생성한 Thread는 Looper를 가지고 있지 않다.

    class LooperThread extends Thread {
      public Handler mHandler;

      public void run() {
          Looper.prepare();

          mHandler = new Handler() {
              public void handleMessage(Message msg) {
                  // process incoming messages here
              }
          };
          Looper.loop();
      }
    }

#### 1-2. HandlerThread 이용하기
: HandlerThread는 내부적으로 하나의 Looper를 가지고 있다.  
: 자동으로 Looper 내부의 Message Queue도 생성되므로 이를 통해 스레드로 Message나 Runnable을 전달받을 수 있다.

    HandlerThread handlerThread = new HandlerThread("HandlerName");
    handlerThread.start();
    Handler handler = new Handler(handlerThread.getLooper());

### 2. Looper의 중단
: Looper는 무한 루프를 도므로, Handler를 사용하지 않을 때 종료해줘야 한다.  
- quit() - 즉시 종료
- quitSafelt() - 현재 Message Queue에 쌓인 메시지들을 처리한 후 종료
