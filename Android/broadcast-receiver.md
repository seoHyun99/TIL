# [Android] BroadcastReceiver

## BroadcastReceiver란?
: 안드로이드 4대 컴포넌트 중에 하나로 시스템이나 앱 등에서 이벤트 발생시 방송을 해주는 개념이다. 이렇게 방송된 이벤트는 각 앱에서 필요한 방송 이벤트를 받아들이고 이벤트에 대한 처리를 리시버를 통해 할 수 있게 해준다.  

### Receiver
: 리시버가 10초안에 수행하지 못하면 ANR 에러가 발생한다.

1. 정적 리시버  
: 한 번 등록하면 해제할 수 없다.  
: 매니페스트에 아래 코드처럼 추가해주어야 한다.

**AndroidManifest.xml**

    <receiver android:name=".ExampleReceiver">
        <intent-filter>
            <action android:name="com.br.myapplication.SEND_BROAD_CAST"/>
        </intent-filter>
    </receiver>

**java**
```java
public class TestReceiver extends BroadcastReceiver {

    private static final String TAG = TestReceiver.class.getSimpleName();

    @Override
    public void onReceive(Context context, Intent intent) {
        String name = intent.getAction();

        // Intent SendBroadCast로 보낸 action TAG 이름으로 필요한 방송을 찾는다.          if(name.equals("com.br.myapplication.SEND_BROAD_CAST ")) {
            Log.d(TAG, "BroadcastReceiver :: com.dwfox.myapplication.SEND_BROAD_CAST :: " + intent.getStringExtra("sendString"));
        }
    }
}
```




2. 동적 리시버  
: 등록과 해제가 자유롭다.  
: 필요한 부분에 리시버를 등록하고 해지하면서 시스템이나 앱에 부하를 줄일 수 있지만, 해제를 해주지 않으면 메모리 릭이 발생한다.  
: 자신을 등록한 Component의 생명주기가 끝나면 사라진다.


```java
public class MainActivity extends Activity {

    private static final String TAG = ReceiverVideoFinish.class.getSimpleName();
    private BroadcaastReceiver receiver;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        //브로드캐스트의 액션을 등록하기 위한 인텐트 필터
        IntentFilter intentfilter = new IntentFilter();
        intentfilter.addAction("com.dwfox.myapplication.SEND_BROAD_CAST");

        //동적 리시버 구현
        receiver = new BroadcastRecevier() {
            @Override
            public void onRecevie(Context context, Intent intent) {
                String sendString = intent.getStringExtra("sendString");
                Log.d(TAG, sendString);
            }
        };

        //Receiver 등록
        registerReceiver(receiver, intentFilter);

    }

    //등록된 Receiver는 반드시 해제 해주어야 한다.
    unregisterReceiver(receiver);
}
```
