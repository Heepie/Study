# Thread 안드로이드 실습

## 도입
이번에는 SubThread를 통해 SeekBar를 회전시키고 MainThread의 버튼을 통해 SubThread를 제어해 보자.</br>
![intro](http://cfile10.uf.tistory.com/image/99755A3359CE300E3345E4)

## 실습
- MainActivity
```java
public class MainActivity extends AppCompatActivity {
    private SeekBar seekBar;
    private Rotator rotator;

    public static final int ROTATOR = 999;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        seekBar = (SeekBar) findViewById(R.id.seekBar);

        // seekBar를 제어하기 위한 toogleButton 선언
        final ToggleButton toggleButton =
                (ToggleButton) findViewById(R.id.toggleButton);

        // Thread를 다룰 handler 선언
        final Handler handler = new Handler() {
            @Override
            public void handleMessage(Message msg) {
                switch (msg.what) {
                    case ROTATOR:
                        seekBar.setRotation(seekBar.getRotation() + 6);
                }
            }
        };

        toggleButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if (toggleButton.isChecked()) {
                    // On이라면 Thread 새로 생성성
                    rotator = new Rotator(handler);
                    rotator.start();
                }
                else
                    // Off라면 Stop
                    rotator.setStop();
            }
        });

        // Thread 초기화면 및 시작
        rotator = new Rotator(handler);
        rotator.start();

    }
}
class Rotator extends Thread {
    private Handler handler;
    private boolean isRotate = true;
    public Rotator(Handler handler) {
        this.handler = handler;
    }

    @Override
    public void run() {
        while (isRotate) {
            try {
                sleep(100);
                handler.sendEmptyMessage(MainActivity.ROTATOR);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public void setStop() {
        isRotate = false;
    }
}
```

## 스크린 샷
![screenshot](http://cfile24.uf.tistory.com/image/992BDC3359CE303105E5A4)
