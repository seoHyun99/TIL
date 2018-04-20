# [Android] Activity Lifecycle

|    메소드   |                                                            설명                                                           |          다음 메소드         |
|:-----------:|:-------------------------------------------------------------------------------------------------------------------------:|:----------------------------:|
| onCreate()  | 액티비티가 생성될 때 호출되며 사용자 인터페이스 초기화에 사용됨.                                                          | onStart()                    |
| onRestart() | 액티비티가 멈췄다가 다시 시작되기 바로 전에 호출됨.                                                                       | onStart()                    |
| onStart()   | 액티비티가 사용자에게 보여지기 바로 직전에 호출됨.                                                                        | onResume() 또는 onStop()     |
| onResume()  | 액티비티가 사용자와 상호작용하기 바로 전에 호출됨.                                                                        | onPause()                    |
| onPause()   | 다른 액티비티가 보여질 때 호출됨. 데이터 저장, 스레드 중지 등의 처리를 하기에 적당한 메소드.                              | onResume() 또는 onStop()     |
| onStop()    | 액티비티가 더이상 사용자에게 보여지지 않을 때 호출됨. 메모리가 부족할 경우에는 onStop() 메소드가 호출되지 않을 수도 있음. | onRestart() 또는 onDestroy() |
| onDestory() | 액티비티가 소멸될 대 호출됨. finish() 메소드가 호출되거나 시스템이 메모리 확보를 위해 액티비티를 제거할 때 호출됨.        | 없음                         |


## Task
> A task is a collection of activities that users interact with when performing a certain job. The activities are arranged in a stack (the back stack), in the order in which each activity is opened.

→ 하나의 Activity는 서로 다른 Application에서 공유가 가능해, 현재 실행중인 Application의 Activity Stack을 저장하는 곳이다.

## Back Stack
: Activity에 대한 Focus를 잃었을 경우 Activity의 실행 순서대로 Back Stack에 쌓인다.  
: LIFO 구조로 스택에 쌓여있는 Activity는 다시 재정렬되지 않는다.  
: 백버튼을 눌러 이전의 Activity를 팝시키면, 원래 띄워져있던 Activity는 소멸된다.

-------

### TIP & TECH   
**사용자가 홈 키를 눌렀는지를 파악하는 방법**
Activity 클래스에는 사용자가 홈 키를 눌렀을 때 호출되는 **onUserLeaveHint()** 메소드가 제공한다.  
참고로 이 메소드가 호출된 뒤에는 Activity의 onPause() 메소드가 호출된다.
