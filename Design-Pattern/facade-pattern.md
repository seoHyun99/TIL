# [Design Pattern] Facade Pattern

## Facade Pattern이란?
> facade : 정면, 외관

- 통일된 인터페이스를 통해 복잡한 서브시스템들을 간단히 사용하도록 만든 패턴

### Facade Pattern 예시

    public class Facade {
           private HelpSystem1 helpSystem1;
           private HelpSystem2 helpSystem2;
           private HelpSystem3 helpSystem3;

           public Facade() {
                  helpSystem1 = new HelpSystem1;
                  helpSystem2 = new HelpSystem2;
                  helpSystem3 = new HelpSystem3;
           }

           public void process() {
                  helpSystem1.process();
                  helpSystem2.process();
                  helpSystem3.process();
           }
    }

    //서브 시스템 1
    class HelpSystem1 {
           public HelpSystem() {
                  System.out.println("Call Constructor : " + getClass().getSimpleName());
           }

           public void process() {
                  System.out.println("Call Process :" + getClass().getSimpleName());
           }
    }

    //서브 시스템 2
    class HelpSystem2 {
           public HelpSystem() {
                  System.out.println("Call Constructor : " + getClass().getSimpleName());
           }

           public void process() {
                  System.out.println("Call Process :" + getClass().getSimpleName());
           }
    }

    //서브 시스템 3
    class HelpSystem3 {
           public HelpSystem() {
                  System.out.println("Call Constructor : " + getClass().getSimpleName());
           }

           public void process() {
                  System.out.println("Call Process :" + getClass().getSimpleName());
           }
    }

    // 다른 패키지
    public class Application {
           public static void main(String[] args) {
                  Facade facade = new Facade();
                  facade.process();
           }
    }
