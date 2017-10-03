# Viewpager와 TabLayout 연결
탭을 보여주기 위한 수평 레이아웃인 TabLayout과 Viewpager를 연결해보자.

## 실습
- MainActivity
```java
public class MainActivity extends AppCompatActivity {
    private TabLayout tabLayout;
    private ViewPager viewpager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // ...
        connectViewpagerAndTabLayout();
        // ...
    }
    // ...
    // TabLayout과 Viewpager 연결
    private void connectViewpagerAndTabLayout() {
        tabLayout.addOnTabSelectedListener(
                new TabLayout.ViewPagerOnTabSelectedListener(viewpager)
        );

        viewpager.addOnPageChangeListener(
                new TabLayout.TabLayoutOnPageChangeListener(tabLayout)
        );
    }
}
```

- activity_main
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.heepie.tabandviewpager.MainActivity">
    <android.support.design.widget.TabLayout
        android:id="@+id/tabLayout"
        android:layout_width="0dp"
        android:layout_height="50dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginTop="8dp"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:layout_marginStart="8dp"
        android:layout_marginEnd="8dp">

    </android.support.design.widget.TabLayout>
    <android.support.v4.view.ViewPager
        android:id="@+id/viewpager"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginTop="8dp"
        app:layout_constraintTop_toBottomOf="@+id/tabLayout"
        android:layout_marginRight="8dp"
        app:layout_constraintRight_toRightOf="parent"
        android:layout_marginLeft="8dp"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        android:layout_marginBottom="8dp">
    </android.support.v4.view.ViewPager>
</android.support.constraint.ConstraintLayout>
```

- viewpager.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
    <TextView
        android:id="@+id/textData"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="center"
        android:gravity="center"
        android:text="Data"
        android:textAppearance="@style/TextAppearance.AppCompat.Large"
        tools:layout_editor_absoluteX="0dp"
        tools:layout_editor_absoluteY="0dp" />
</LinearLayout>
```

## 스크린 샷
![screenshot](http://cfile25.uf.tistory.com/image/99DFEE3359CF8D8F0F5408)
