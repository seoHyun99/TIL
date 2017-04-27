# [Android] ANR

## ANR이란?
: ANR은 Application Not Responding의 약자로, 어플리케이션이 응답하지 않는다는 에러이다.  

### 1. ANR이 발생하는 경우
1. Input event(사용자 입력)에 5초 내에 처리되지 않았을 때
2. BroadcastReceiver가 10초 내에 처리되지 않았을 때
3. Service가 20초 내에 처리되지 않았을 때

### 2. ANR이 발생하는 이유
: Main Thread(UI Thread)가 일정 시간동안 어떠한 Task에 잡혀있으면 발생하게 된다.  
: UI가 없는 BroadcastReceiver와 Service의 실행 주체는 Main Thread이므로 ANR을 발생시킨다.  

### 3. ANR 대응하기
#### 3-1. Activity에서 발생하는 ANR 해결하기
: MainThread는 Activity에서 실행되는 여러 가지 콜백함수들을 호출해 처리하는 역할을 한다.  
: 따라서 **별도의 쓰레드** 를 생성해 처리해야 한다.  

#### 3-2. Service에서 발생하는 ANR 해결하기
: Service가 별도의 Component로 구분되어 있더라도 모든 콜백 함수들은 MainThread에 의해서 처리된다.  
: Service또한 콜백메소드에서 특별한 작업을 하기 위해서는 **별도의 쓰레드** 를 생성해 처리해야 한다.

#### 3-3. Progress Bar 이용해 작업의 진행과정 안내하기

### 쓰레드 를 생성해 처리해야하는 경우
1. 주기적으로 오래 처리해야 하는 작업
2. 네트워크와 관련된 작업 (네트워크 연결 상태에 따라 시간이 무한정으로 늘어날 수 있음)
