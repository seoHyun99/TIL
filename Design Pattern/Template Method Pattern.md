# [Design Pattern] Template Method Pattern

## Template Method Pattern이란?
- 알고리즘의 구조를 메소드에 정의하고 하위 클래스에서 알고리즘 구조의 변경없이 알고리즘을 **재정의** 하는 패턴
- 코드의 중복을 줄이고, Refactoring에 유리한 패턴으로 상속을 통한 확장 개발 방법

## 사용 시기
- 구현하려는 알고리즘이 일정한 프로세스가 있다.
- 구현하려는 알고리즘이 변경 가능성이 있다.

## 사용 단계
1. 알고리즘을 여러 단계로 나눈다.
2. 나눠진 알고리즘의 단계를 메소드로 선언한다.
3. 알고리즘을 수행할 템플릿 메소드를 만든다.
4. 하위 클래스에서 나눠진 메소드들을 구현한다.

## 고려사항
- 멤버 함수들의 접근 범위 지정에 대한 명확화가 필요
- 가상함수, 일반함수로 선언에 대한 결정이 필요
- 재정의 함수(virtual)의 수를 줄이는 것이 필요(virtual table 확장에 따른 performace 문제점 발생)

### Template Method Pattern 예시

public abstract class AbstGameConnetHelper {
       protected abstract String doSecurity(String string);
       protected abstract boolean authentication(String id, String password);
       protected abstract int authorization(String userName);
       protected abstract String connetion(String info);

       //템플릿 메소드
       public String requestConnetion(String encodedInfo) {
              //보안 작업 -> 암호화 된 문자열을 복호화
              String decodedInfo = doSecurity(str);

              //반환된 것을 가지고 아이디, 암호를 할당한다.
              String id = "id";
              String password = "pw";

              if(!authentication(id, password)) {
                throw new Error("아이디 암호 불일치");
              }

              String userName = "userName";
              int i = authorization(userName);

              switch (i) {
              case 0: // 게임 매니저
                     break;
              case 1: // 유료 회원
                     break;
              case 2: // 무료 회원
                     break;
              case 3: // 권한 없음
                     break;
              default: // 기타 상황
                     break;
              }

              return connetion();
       }
}

public class DefaultGameConnetHelper extends AbstGameConnetHelper {
       @Override
       protected String doSecurity(String string) {
              System.out.println("디코드");
              return string;
       }

       @Override
       protected boolean authentication(String id, String password) {
              System.out.println("아이디/암호 확인 과정");
              return true; // 맞다고 가정
       }

       @Override
       protected int authorization(String userName) {
              System.out.println("권한 확인");
              return 0;
       }

       @Override
       protected String connetion(String info) {
              System.out.println("마지막 접속단계");
              return info; // 접속에 필요한 정보 전달
       }
}

public class Main {
       public static void main(String[] args) {
              AbstGameConnetHelper helper = new DefaultGameConnetHelper();

              helper.requestConnetion("아이디 암호 등 접속 정보");
       }
}
