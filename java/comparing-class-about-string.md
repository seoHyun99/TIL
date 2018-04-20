# [Java] 문자열 관련 클래스 비교

자바에서 문자열 관련 클래스로 String, StringBuffer, StringBuilder가 존재한다.

### String
- 한 번 생성된 String 인스턴스가 갖고 있는 문자열 읽는 것은 가능하나, 변경은 불가능.
- '+' 연산자를 사용할 때 마다 결합된 문자열을 담은 String 인스턴스가 생성되는 것이다.

### StringBuilder
- append() 함수를 사용해 String과 달리 생성된 이후에도 문자열 변경이 가능
- JDK 1.5 버전 이후 컴파일 단계에서 String 객체를 사용해도 StringBuilder로 컴파일 되도록 변경


### StringBuffer
- 문자열을 다루는 클래스이며, 문자열 변경이 가능하다.
- 객체 생성시 크기를 지정하지 않아도 기본적으로 16개의 문자를 저장할 수 있는 버퍼 공간을 가진다.
- 동기화를 지원한다.
