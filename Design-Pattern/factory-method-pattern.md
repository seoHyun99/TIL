# [Design Pattern]Factory Method Pattern

## Factory Method Pattern이란?

> 객체를 만들어내는 부분을 서브 클래스에 위임하는 패턴

즉, new 키워드를 호출하는 부분을 서브 클래스에 위임한다.
-> 객체를 만들어내는 공장을 만드는 패턴

### 사용하는 이유
- 클래스의 결합도 낮추기 (결합도: 클래스의 변경점이 생겼을 때 얼마나 다른 클래스에 영향을 주는가)
- 객체 생성의 변화에 대비하는데 유용


### Factory Method Pattern 예시

//framework 패키지
public abstract class ItemCreator {
       public Item void create() {
              Item item;

              //step1
              requestItemsInfo();
              //step2
              item = createItem();
              //step3
              createItemLog();

              return item;
       }

       //아이템을 생성하기 전에 db에 아이템 정보를 요청
       abstract protected void requestItemsInfo();

       //아이템을 생성 후 db에 아이템 생성 로그를 남김
       abstract protected void createItemLog();

       //아이템을 생성하는 알고리즘
       abstract protected Item createItem();

}

public interface Item {
       public void use();
}

//concrete 패키지
public class HpPotion implements Item {
       @Override
       public void use {
              System.out.println("체력 회복!");
       }
}

public class MpPotion implements Item {
       @Override
       public void use {
              System.out.println("마력 회복!");
       }
}

public class HpCreator extends ItemCreator {

       @Override
       protected void requestItemsInfo() {
              System.out.println("db에서 체력 회복 물약의 정보를 가져옵니다.");
       }

       @Override
       protected void createItemLog() {
              System.out.println("체력 회복 물약을 새로 생성했습니다." + new Date());
       }

       @Override
       protected Item createItem() {
              return new HpPotion();
       }
}

public class MpCreator extends ItemCreator {

       @Override
       protected void requestItemsInfo() {
              System.out.println("db에서 마력 회복 물약의 정보를 가져옵니다.");
       }

       @Override
       protected void createItemLog() {
              System.out.println("마력 회복 물약을 새로 생성했습니다." + new Date());
       }

       @Override
       protected Item createItem() {
              return new MpPotion();
       }
}

public class Main {
       public static void main(String[] args) {
              ItemCreator creator;
              Item item;

              creator = new HpCreator();
              item = creator.create();
              item.use();

              creator = new MpCreator();
              item = creator.create();
              item.use();
       }
}
