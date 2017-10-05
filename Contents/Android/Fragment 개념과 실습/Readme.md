# Fragment 개념과 실습

## 개념
Fragment는 Activity에 배치되는 화면과 동작의 조각이다. </br>
Fragment는 Android 3.0(API 11)부터 적용된 개념이며 등장배경은 다음과 같다.
![concept](http://cfile3.uf.tistory.com/image/99AC9B3359CB7FA8298F17)</br>
스마트폰 사용과 함께 테블릿이 등장하며 App의 Layout이 커졌고 View의 독립적인 기능과 View를 다른 크기의 Layout에서도 재활용하기 위해 도입된 개념이다.

## 실습
Fragment는 Activity 안에서 Fragment Manager에 의해 관리된다.</br>
![manage](http://cfile9.uf.tistory.com/image/99E04F3359CB81E826D53E)</br>

- MainActivity
```java
public class MainActivity extends AppCompatActivity {    
    // ...
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 1. Fragment Manager 호출
        // SupportFragmentManager()를 사용하는 이유는 하위 버전과 호환성을 위함이다.
//        FragmentManager manager = getFragmentManager();
        FragmentManager manager = getSupportFragmentManager();

        // 2. 트랜젝션 관리자 설정
        FragmentTransaction transaction = manager.beginTransaction();

        // 3. 트랜젝션에 Fragment 추가(추가할 위치, 생선한 Fragment)
        transaction.add(R.id.stage, new ListFragment());

        // 4. 트랜젝션 시작
        transaction.commit();
    }
    // ...
}
```

- Fragment
```java
public class ListFragment extends Fragment {

    public ListFragment() {
        // Required empty public constructor
    }
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_list, container, false);
    }
}
```

- activity_main.xml - main.xml에 id를 설정한 것을 주목
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/stage"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.heepie.fragment.MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="MainActivity"
        android:textAppearance="@style/TextAppearance.AppCompat.Large"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintHorizontal_bias="0.501"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.255" />
</android.support.constraint.ConstraintLayout>
```

## 스크린 샷
![screenshot](http://cfile24.uf.tistory.com/image/99B2993359CB842F21C9BE)
