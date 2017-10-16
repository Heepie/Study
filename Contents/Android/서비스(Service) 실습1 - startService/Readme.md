# 서비스(Service) 실습 - startService

## 개념
서비스를 실행시키는 첫번째 방법인 startService을 실습할 예정이다.</br>
![concept1](http://cfile10.uf.tistory.com/image/99775D3359DD629012CC7A)</br>

## 실습
- MainActivity
MainActivity에서는 xml에 버튼에 대한 onClick 메소드만 설정해 준다.
```java
public class MainActivity extends AppCompatActivity {
    // 서비스를 호출하기 위한 인텐트
    Intent intent;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        intent = new Intent(this, MyService.class);
    }

    // 서비스 시작
    public void start(View v) {
        startService(intent);
    }

    // 서비스 종료
    public void stop(View v) {
        stopService(intent);
    }
}
```

- MyService
MyService는 프로젝트 오른쪽 버튼 -> New -> Service -> Service 클릭해 기본 Service를 생성한다. </br>이 후 생명 주기를 확인하기 위해 메소드를 오버라이딩 했다.
```java
public class MyService extends Service {
    private final String CLASSNAME = getClass().getSimpleName() + " ";

    public MyService() {
    }

    @Override
    public void onCreate() {
        Log.i("heepie", CLASSNAME + "onCreate");
        super.onCreate();
    }

    // 서비스의 로직은 onStartCommand에 작성
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Log.i("heepie", CLASSNAME + "onStartCommand");
        return super.onStartCommand(intent, flags, startId);
    }

    @Override
    public IBinder onBind(Intent intent) {
        Log.i("heepie", CLASSNAME + "onBind");
        // TODO: Return the communication channel to the service.
        throw new UnsupportedOperationException("Not yet implemented");
    }

    @Override
    public boolean onUnbind(Intent intent) {
        Log.i("heepie", CLASSNAME + "onUnbind");
        return super.onUnbind(intent);
    }

    @Override
    public void onDestroy() {
        Log.i("heepie", CLASSNAME + "onDestory");
        super.onDestroy();
    }
}
```

## 스크린 샷
![screenshot](http://cfile23.uf.tistory.com/image/9958823359DD6305138464)</br>
