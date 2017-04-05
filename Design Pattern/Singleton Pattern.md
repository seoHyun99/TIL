# [Design Pattern] Singleton Pattern

## Singleton Pattern이란?
- 생성자가 여러 차례 호출되더라도 실제 생성되는 객체는 하나이다.
- 최초 생성 이후에 호출된 생성자는 이미 생성된 객체를 리턴한다.

### 단일 스레드 환경에서의 Singleton Pattern

    public class Singleton {
	    private static Singleton instance;

	    private Singleton(){ }

	    public static Singleton getInstance(){
    		if (instance == null){
			    instance = new Singleton();
		    }
		    return instance;
	    }
     }

### 멀티 스레드 환경에서의 Singleton Pattern

    public class Singleton {
	    private static Singleton instance;

	    private Singleton(){}

	    public static synchronized Singleton getInstance(){
		    if (instance == null){
			    instance = new Singleton();
		    }
		    return instance;
	    }
     }
