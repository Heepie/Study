# 커스텀뷰 개념 및 실습

## 개념
커스텀 뷰란 개발자의 입맛에 맞게 뷰(텍스트 뷰, 버튼 등등)를 수정한 뷰를 말한다.</br>
커스텀 뷰를 생성하는 방법은 크게 2가지가 있다.</br></br>
1) XML에 속성을 정의 후 호출해 사용하는 방법
![concept1](http://cfile4.uf.tistory.com/image/9980F83359BFA0A1064C77)</br>
※ attirs.xml의 경우는 안드로이드에서 정한 path의 xml이므로 이름을 변경할 수 없다.</br></br>
2) 액티비티 안에서 Java 코드를 통해 직접 호출 하는 방법
![concept2](http://cfile29.uf.tistory.com/image/99211E3359BFA1CC08D556)

## 실습
1) XML에 속성을 정의 후 호출해 사용하는 방법</br>

- attrs.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <declare-styleable name="CustomButton">
        <attr name="animation" format="string"/>
        <attr name="delimeter" format="string"/>
    </declare-styleable>

    <declare-styleable name="CustomLayout">
        <!-- .... -->
    </declare-styleable>
</resources>
```

- CustomButton.class
```java
public class CustomButton extends AppCompatButton implements View.OnTouchListener{
    private AnimatorSet aniSet;
    private boolean isAni=false;
    public CustomButton(Context context, AttributeSet attrs) {
        super(context, attrs);

        // 1. atrrs.xml에 정의된 속성을 가져온다.
        TypedArray typed = context.obtainStyledAttributes(attrs, R.styleable.AniButton);

        // 2. 해당 이름으로 정의된 속성의 개수를 가져온다.
        int size = typed.getIndexCount();

        // 3. 반복문을 돌면서 해당 속성에 대한 처리를 해준다.
        for(int i =0; i<size; i=i+1) {
            // 3.1 현재 배열에 있는 속성 아이디 가져오기
            int current_attr = typed.getIndex(i);
            switch (current_attr) {
                case R.styleable.AniButton_animation:
                    String animation = typed.getString(current_attr);
                    if (animation.equals("true")) {
                        isAni = true;
                        String currentText = getText().toString();

                        // 원하는 애니메이션 설정
                        ObjectAnimator aniX = ObjectAnimator.ofFloat(this, "scaleX", 1.2f, 1.0f);
                        ObjectAnimator aniY = ObjectAnimator.ofFloat(this, "scaleY", 1.2f, 1.0f);
                        aniSet = new AnimatorSet();
                        aniSet.playTogether(aniX, aniY);
                        aniSet.setDuration(3000);
                    }
                    break;
            }
        }

    }
    public void startAni() {
        if (isAni)
            aniSet.start();
    }
    // ...
}
```

- MainActivity
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    initView();
    initListener();
}
// ...
private void initListener() {
    aniButton.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            CustomButton.startAni();
        }
    });
}
```

2) 액티비티 안에서 Java 코드를 통해 직접 호출 하는 방법</br>

- CustomButton
```Java
public class CustomButton extends AppCompatButton {
    public CustomButton(Context context) {
        super(context);
        setText("hello World");
        setBackgroundColor(Color.CYAN);
    }
}
```

- MainActivity
```java
public class MainActivity extends AppCompatActivity {
    ConstraintLayout stage;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        initView();
    }

    private void initView() {
        stage = (ConstraintLayout)findViewById(R.id.stage);
        // 레이아웃에 생성한 커스텀 버튼 등록
        AniButton aniButton = new AniButton(this);
        stage.addView(aniButton);
    }
}
```
