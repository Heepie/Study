# 서비스(Service) 실습 - bindService

## 개념
서비스를 실행시키는 두번째 방법인 bindService을 실습할 예정이다.</br>

![concept1](http://cfile4.uf.tistory.com/image/990A923359DDF5891E2116)</br>

## 실습 1
- MainActivity
```java
public class MainActivity extends AppCompatActivity {
    // ...
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        intent = new Intent(this, MyService.class);
    }

    // 서비스와의 연결 통로
    ServiceConnection conn = new ServiceConnection() {
        // 서비스가 Bind(연결)되는 순간 호출되는 메소드
        @Override
        public void onServiceConnected(ComponentName name, IBinder iBinder) {
            Log.i("heepie", CLASSNAME + "onServiceConnected, Name: " + name.getClass().getSimpleName());
            // 일회성 결과
            int result = ((MyService.CustomBinder)iBinder).getResult();
            Toast.makeText(MainActivity.this, result+"", Toast.LENGTH_SHORT).show();
        }

        // 서비스가 중단되거나 연결이 끊어지면 호출되는 메소드
        // 서비스가 정상적으로 종료되면 호출되지 않는다.
        @Override
        public void onServiceDisconnected(ComponentName name) {
            Log.i("heepie", CLASSNAME + "onServiceDisconnected");
        }
    };
    // ...
    public void bind(View v) {
        bindService(intent, conn, Context.BIND_AUTO_CREATE);
    }

    public void unBind(View v) {
        unbindService(conn);
    }
}
```

- MyService
```java
public class MyService extends Service {
    // ...
    @Override
    public IBinder onBind(Intent intent) {
        Log.i("heepie", CLASSNAME + "onBind");
        // TODO: Return the communication channel to the service.
        customBinder = new CustomBinder();

        for (int i=0; i<100; i=i+1) {
            result += i;
        }
        customBinder.setResult(result);
        // 결과를 입력한 객체를 onServiceConnected 메소드로 전달
        return customBinder;
    }
    // ...
    class CustomBinder extends Binder {
        private int result;

        public int getResult() {
            return result;
        }

        public void setResult(int result) {
            this.result = result;
        }
    }
}
```

## 문제점 및 해결
위의 코드는 서비스를 통해 결과 확인을 1회 밖에 할 수 없다. </br>
![problem](http://cfile7.uf.tistory.com/image/99085C3359DDED38023810)</br></br>
bindService 메소드를 사용해 iBinder로 서비스와 통로가 형성되어야하는 장점을 사용하지 못한 것이다. 그래서 아래와 같은 그림으로 코드를 변경할 예정이다.</br>
![solution](http://cfile22.uf.tistory.com/image/99DBBA3359DDED6C1AD47D)</br>

## 실습 2
- MainActivity
```java
public class MainActivity extends AppCompatActivity {
    // ...
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        intent = new Intent(this, MyService.class);
    }

    // 지속적인 연결 유지를 위한 MyService 변수 설정
    MyService service;

    // 서비스와의 연결 통로
    ServiceConnection conn = new ServiceConnection() {
        // 서비스가 Bind(연결)되는 순간 호출되는 메소드
        @Override
        public void onServiceConnected(ComponentName name, IBinder iBinder) {
            Log.i("heepie", CLASSNAME + "onServiceConnected, Name: " + name.getClass().getSimpleName());
            // 일회성 결과
            int result = ((MyService.CustomBinder)iBinder).getResult();
            Toast.makeText(MainActivity.this, result+"", Toast.LENGTH_SHORT).show();

            // 서비스 할당
            service = ((MyService.CustomBinder) iBinder).getService();
        }

        // 서비스가 중단되거나 연결이 끊어지면 호출되는 메소드
        // 서비스가 정상적으로 종료되면 호출되지 않는다.
        @Override
        public void onServiceDisconnected(ComponentName name) {
            Log.i("heepie", CLASSNAME + "onServiceDisconnected");
        }
    };
    // ...
    public void bind(View v) {
        bindService(intent, conn, Context.BIND_AUTO_CREATE);
    }

    public void unBind(View v) {
        unbindService(conn);
    }
}
```

- MyService
```java
public class MyService extends Service {
    private final String CLASSNAME = getClass().getSimpleName() + " ";

    private CustomBinder customBinder;
    int result=0;
    public MyService() {
    }
    // ...
    @Override
    public IBinder onBind(Intent intent) {
        Log.i("heepie", CLASSNAME + "onBind");
        // TODO: Return the communication channel to the service.
        customBinder = new CustomBinder();

        for (int i=0; i<100; i=i+1) {
            result += i;
        }

        return customBinder;
    }

    // 합 결과 반환
    public int getResult() {
        return result;
    }

    // ...
    class CustomBinder extends Binder {
        private int result;

        // 지속적인 연결 유지를 위한 MyService 반환
        public MyService getService() {
            return MyService.this;
        }
    }
}
```

## 스크린 샷
![screenshot](http://cfile1.uf.tistory.com/image/99338D3359E74812316310)</br>
