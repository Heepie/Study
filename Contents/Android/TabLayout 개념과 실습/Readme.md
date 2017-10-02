# TabLayout 개념과 실습

## 개념
탭을 보여주기 위한 수평 레이아웃이다. 탭 레이아웃은 일반적으로 viewpager와 함께 많이 사용된다.

## 실습
- MainActivity
```java
public class MainActivity extends AppCompatActivity {
    private TabLayout tabLayout;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tabLayout = (TabLayout) findViewById(R.id.tabLayout);

        tabLayout.addTab(tabLayout.newTab().setText("First"));
        tabLayout.addTab(tabLayout.newTab().setText("Second"));
        tabLayout.addTab(tabLayout.newTab().setText("Third"));
    }
    // ...
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
    tools:context="com.example.heepie.tablayout.MainActivity">

    <android.support.design.widget.TabLayout
        android:layout_width="0dp"
        android:layout_height="50dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginTop="8dp"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:id="@+id/tabLayout">
    </android.support.design.widget.TabLayout>
</android.support.constraint.ConstraintLayout>
```

## 스크린 샷
![screenshot](http://cfile29.uf.tistory.com/image/99E4DA3359CE110114CB4B)
