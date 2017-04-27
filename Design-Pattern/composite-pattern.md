# [Design Pattern] Composite Pattern

## Composite Pattern이란?
- 객채와 객체의 그룹을 구분없이 하나의 인터페이스로 다룰 수 있게 한다.
- 객체(Leaf)와 구성(Composite)을 트리로 구성하여 하나의 인터페이스에서 사용하도록 고려한 패턴이다.


### Composite Pattern 예시

    public class Main {
           public static void main(String[] args) {
                  Folder
                  root = new Foler("root"),
                  home = new Foler("home"),
                  seohyun = new Foler("seohyun"),
                  music = new Foler("music"),
                  picture = new Foler("picture"),
                  usr = new Foler("usr");

                  File
                  track1 = new File("track1"),
                  track2 = new File("track2"),
                  pic1 = new File("pic1"),
                  java = new File("java");

                  root.addComponent(home);
                         home.addComponent(seohyun);
                                seohyun.addComponent(music);
                                       music.addComponent(track1);
                                       music.addComponent(track2);
                                seohyun.addComponent(picture);
                                       picture.addComponent(pic1);

                  root.addComponent(usr);
                         usr.addComponent(java);

           }
    }

    abstract public class Component {

           private String name;

           public Component(String name) {
                  this.name = name;
           }

           public String getName() {
                  return name;
           }

           public void setName(String name) {
                  this.name = name;
           }
    }

    public class File extends Component {
           private Object data;

           public File(String name) {
                  super(name);
           }

           public Object getData() {
                  return data;
           }

           public void setData(Object data) {
                  this.data = data;
           }
    }    

    public class Folder extends Component {
           List<Component> children = new ArrayList<>();

           public Folder(String name) {
                  super(name);
           }

           public boolean addComponent(Component component) {
                  return children.add(component);
           }

           public boolean removeComponent(Component component) {
                  return children.remove(component);
           }
    }
