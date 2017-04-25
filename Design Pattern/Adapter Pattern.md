# [Design Pattern] Adapter Pattern

## Adapter Pattern이란?
- 한 클래스의 인터페이스를 클라이언트에서 사용하고자하는 다른 인터페이스로 변환한다.
- 어댑터를 이용해 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해 사용할 수 있다.
- Target - Adapter - Adaptee

## Object Adapter Pattern
: Adpater는 감싸야할 클래스의 객체를 포함하고 있다.  
: 이러한 상황에서 Adapter는 감싸진 객체를 호출하는 일을 한다.

## Class Adapter Pattern
: 여러 개의 다형성 인터페이스를 사용한다.  
: 구현될 예정인 인터페이스나 이미 구현된 인터페이스를 상속받아 만들어진다.  
: 구현될 예정인 인터페이스는 순수(pure) 인터페이스 클래스로 만들어지는 것이 일반적이다.

### Object Adpater Pattern 예시

    // 제공해주는 클래스
    public class Math {
         public static double twoTime(double num) { return num * 2;}
         public static double half(double num) { return num / 2;}
    }

    public interface Adapter {
         public Float twiceOf(Float f);
         public Float halfOf(Float f);
    }

    public class AdapterImpl implements Adapter {
         @Override
         public Float twiceOf(Float f) {
              return (float) Math.twoTime(f.doubleValue());
         }

         @Override
         public Float halfOf(Float f) {
              return (float) Math.half(f.doubleValue());
         }
    }

    public class Main {
         pulbic static void main(String[] args) {
              Adapter adpater = new AdapterImpl();
              System.out.println(adapter.twiceOf(100f));
              System.out.println(adapter.halfOf(100f));
         }
    }
