# [Design Pattern] Strategy Pattern

## Strategy Pattern이란?
- 동적으로 알고리즘을 교체할 수 있는 구조
- 알고리즘 인터페이스를 정의하고, 각각의 알고리즘 클래스별로 캡슐화하여 각각의 알고리즘을 교체 사용가능하게 한다.

### interface
- 기능에 대한 **선언과 구현의 분리**
: 선언은 따로하고 다른 파일에서 구현한다.

#### interface 예시
    public interface Ainterface {
         // 기능 선언
         public void funcA();
    }

    public class AinterfaceImpl implements Ainterface {
         @Override
         public void funcA() {
              System.out.println("AAA");
         }
    }

    public class Main {
         public static void main(String[] args) {
              Ainterface ainterface = new AinterfaceImpl();

              ainterface.funcA();
         }
    }

#### Startegy Pattern 예시
    public interface Weapon {
         public void attack();
    }

    public class Knife implements Weapon {
         @Override
         public void attack() {
              System.out.println("칼 공격");
         }
    }

    public class Sword implements Weapon {
         @Override
         public void attack() {
              System.out.println("검 공격");
         }
    }

    public class Ax implements Weapon {
         @Override
         public void attack() {
              System.out.println("도끼 공격");
         }
    }

    public class GameCharacter {
         //접근점
         private Weapon weapon;

         //교환가능
         public void setWeapon(Weapon weapon) {
              this.weapon = weapon;
         }

         //델리게이트
         public void attack() {
              if (weapon == null) {
                  System.out.println("맨손 공격");
              } else {
                  weapon.attack();
              }
         }
    }

    public class Main {
         public static void main(String[] args) {
              GameCharacter character = new GameCharacter();

              character.attack();

              character.setWeapon(new Knife);
              character.attack();

              character.setWeapon(new Sword);
              character.attack();

              character.setWeapon(new Ax);
              character.attack();
         }
    }
