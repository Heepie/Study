# Viewpager 개념과 실습

## 개념
ViewPager는 좌우로 움직이며 스크린을 확인할 수 있는 위젯이다.
위젯의 특징은 Tablayout을 함께 사용해 데이터를 그룹화해 사용자에게 보여줄 수 있다.

## 실습
- MainActivity
```java
public class MainActivity extends AppCompatActivity {
    private ViewPager viewPager;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        viewPager = (ViewPager) findViewById(R.id.viewpager);

        List<String> data = new ArrayList<>();
        data.add("Hello");
        data.add("YOLO");
        data.add("Heepie");
        data.add("Carpe Diem");

        CustomAdapter adapter = new CustomAdapter(this, data);
        viewPager.setAdapter(adapter);
    }
}
```

- CustomAdapter
```java
public class CustomAdapter extends PagerAdapter {
    private Context context;
    private List<String> data;

    public CustomAdapter(Context context, List<String> data) {
        this.context = context;
        this.data = data;
    }

    // 데이터를 설정하는 메소드
    @Override
    public Object instantiateItem(ViewGroup container, int position) {
        // 뷰 객체 생성
        View view = LayoutInflater.from(context)
                                  .inflate(R.layout.layout_viewpager, null);

        // 데이터 추출
        String value = data.get(position);

        // 값 설정
        TextView textView = view.findViewById(R.id.textView);
        textView.setText(value);

        // 뷰 그룹에 추가
        container.addView(view);

        return view;
    }

    // 데이타의 전체 개수
    @Override
    public int getCount() {
        return data.size();
    }

    // instantiateItem에 아이템을 추가한 후 리턴된 Object가
    // View가 맞는지 확인하는 메소드
    @Override
    public boolean isViewFromObject(View view, Object object) {
        return view == object;
    }

    // 현재 사용하지 않는 데이터를 삭제하는 메소드
    @Override
    public void destroyItem(ViewGroup container, int position, Object object) {
        container.removeView((View)object);
//        super.destroyItem(container, position, object);
    }
}
```

- activity_main
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >
    <android.support.v4.view.ViewPager
        android:id="@+id/viewpager"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginBottom="8dp"
        android:layout_marginTop="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent">
    </android.support.v4.view.ViewPager>
    <Spinner
        android:id="@+id/spinner"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        android:layout_marginBottom="8dp"
        android:layout_marginRight="8dp"
        app:layout_constraintRight_toRightOf="parent"
        android:layout_marginLeft="8dp"
        app:layout_constraintLeft_toLeftOf="parent"
        android:layout_marginTop="8dp"
        app:layout_constraintTop_toBottomOf="@+id/viewpager" />
</android.support.constraint.ConstraintLayout>
```

- layout_viewpager.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >
    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginTop="8dp"
        android:text="Data"
        android:textSize="30dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</android.support.constraint.ConstraintLayout>
```

## 스크린 샷
![screenshot](http://cfile2.uf.tistory.com/image/9968B03359CCED5C098342)
