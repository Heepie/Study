# 리스트 뷰 개념과 실습

## 개념
리스트 뷰란 ** 여러 개의 항목의 리스트 중 1개의 항목을 선택 할 수 있게 도와주는 위젯 ** 이다.
안드로이드에서 리스트를 설정하는 방법은 아래 그림과 같다.
![listview1](http://cfile6.uf.tistory.com/image/9950BD3359C0E25513BABA)
Step1. Data와 Adapter를 연결한다.</br>
Step2. Adapter와 ListView를 연결한다. </br>
※ 사전 준비: ListView에 삽입 될 Data가 보여질 형태인 Xml과 ListView 위젯 추가된 xml이 필요하다. 그리고 중요한 Adapter가 필요하다.</br>

## 실습
1. 사전 준비
  - item.xml
  ```xml
  <?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textResult"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginTop="8dp"
        android:gravity="center_horizontal"
        android:text="tempValue"
        android:textAppearance="@style/TextAppearance.AppCompat"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginRight="8dp"
        android:layout_marginTop="8dp"
        android:text="Oh! Heepie Day!"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textResult" />
</android.support.constraint.ConstraintLayout>
  ```

  - activity_main.xml
  ```xml
  <?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.heepie.day016p.ListActivity">

    <ListView
        android:id="@+id/listview"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginTop="8dp"
        app:layout_constraintTop_toBottomOf="@+id/textView"
        app:layout_constraintBottom_toBottomOf="parent"
        android:layout_marginBottom="8dp"
        android:layout_marginRight="8dp"
        app:layout_constraintRight_toRightOf="parent"
        android:layout_marginLeft="8dp"
        app:layout_constraintLeft_toLeftOf="parent" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginTop="8dp"
        android:text="list"
        android:textAppearance="@style/TextAppearance.AppCompat.Large"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</android.support.constraint.ConstraintLayout>
  ```


  - CustomAdapter 클래스
  ```java
  class CustomAdapter extends BaseAdapter {
    Context context;
    List<String> data;

    CustomAdapter(Context context, List<String> data) {
        this.context = context;
        this.data = data;
    }

    // 데이터 총 개수 리턴
    @Override
    public int getCount() {
        return data.size();
    }

    // 다음으로 보여질 데이터 리턴
    @Override
    public Object getItem(int position) {
        return data.get(position);
    }

    // 데이터의 아이디 리턴
    @Override
    public long getItemId(int position) {
        return position;
    }

    // ListView로 나타날 목록을 1개씩 그려주는 메소드
    @Override
    public View getView(int position, View view, ViewGroup viewGroup) {
        // LayoutInflater는 인자로 입력 받은 xml을 메모리에 로드한다.
        view = LayoutInflater.from(context).inflate(R.layout.item, null);

        // 해당 xml에 정의한 TextView를 객체화
        TextView textResult = (TextView)view.findViewById(R.id.textResult);

        // TextView에 데이터 출력
        textResult.setText(data.get(position));

        return view;
    }
}
  ```
2. Step1 Data와 Adapter 연결, Step2. Adapter와 ListView를 연결
  ```java
  public class MainActivity extends AppCompatActivity {
      // ...
      // ...
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          initView();

          // 임의의 데이터 입력
          List<String> data = new ArrayList<>();
          data.add("Hello World!");

          // Step1. Data와 Adapter 연결
          CustomAdapter customAdapter = new CustomAdapter(this, data);

          // Step2. Adapter와 listView 연결
          listView.setAdapter(customAdapter);

      }

      private void initView () {
          listView = (ListView)findViewById(R.id.listview);
      }
      // ...
      // ...
  }
  ```

## 스크린 샷
![screenshot](http://cfile26.uf.tistory.com/image/99F6063359C0FA2419C8F3)
