# 리사이클러 뷰 개념과 실습

## 개념
리사이클러 뷰란 리스트 뷰의 문제점을 보완한 리스트를 보여주는 위젯이다.</br>
안드로이드에서 리사이클러 뷰를 설정하는 방법은 아래 그림과 같다. </br>
![concept](http://cfile22.uf.tistory.com/image/99B47C3359C68C1B18C5CB)</br>
리스트 뷰 설정과 step2까지는 동일하며 리사이클러 뷰는 LayoutManager를 통해 다양한 템플릿으로 사용자에게 리스트를 보여줄 수 있다.

## 실습
- item.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="4dp">
    <android.support.v7.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="50dp" >
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="horizontal">
            <TextView
                android:id="@+id/textData"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="3"
                android:padding="3dp"
                android:text="TextView"
                android:textSize="20dp" />
            <Button
                android:id="@+id/btnToast"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:padding="3dp"
                android:text="Toast" />
        </LinearLayout>
    </android.support.v7.widget.CardView>
</LinearLayout>
```

- activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.heepie.gradle_orm.MainActivity">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="RecyclerView"
        android:textAppearance="@style/TextAppearance.AppCompat.Medium"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:id="@+id/textView" />
    <android.support.v7.widget.RecyclerView
        android:id="@+id/recyclerView"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginBottom="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginTop="8dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView"
        app:layout_constraintVertical_bias="0.503"
        tools:listitem="@layout/item" />
</android.support.constraint.ConstraintLayout>
```

- CustomAdapter
```java
public class CustomAdapter extends RecyclerView.Adapter<Holder>{
    private List<String> data;

    public void setData(List<String> data) {
        this.data = data;
    }
    @Override
    public int getItemCount() {
        return data.size();
    }
    @Override
    public Holder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext())
                                  .inflate(R.layout.item_list, parent, false);

        Holder holder = new Holder(view);
        return holder;
    }
    @Override
    public void onBindViewHolder(Holder holder, int position) {
        String content = data.get(position);
        holder.setString(content);
    }
}
class Holder extends RecyclerView.ViewHolder {
    TextView textString;
    Button button;
    public Holder(View itemView) {
        super(itemView);

        textString = itemView.findViewById(R.id.textData);
        button = itemView.findViewById(R.id.btnToast);

        initListener();
    }
    private void initListener() {
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(view.getContext(),
                        textString.getText(),
                        Toast.LENGTH_SHORT).show();
            }
        });
    }
    public void setString(String content) {
        textString.setText(content);
    }
}
```

- Step1. Data와 Adapter 연결, Step2. Adapter와 RecyclerView를 연결 Step3. LayoutManager 선택
```java
public class MainActivity extends AppCompatActivity {
    private RecyclerView recyclerView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initView();

        List<String> data = new ArrayList<>();
        data.add("heepie");
        data.add("YOLO");
        data.add("Carpe Diem");

        CustomAdapter adapter = new CustomAdapter();
        adapter.setData(data);

        recyclerView.setAdapter(adapter);
        recyclerView.setLayoutManager(new LinearLayoutManager(this));
    }

    private void initView () {
        recyclerView = (RecyclerView) findViewById(R.id.recyclerView);
    }
}
```
## 스크린 샷
![screenshot](http://cfile30.uf.tistory.com/image/995C453359C68C903191F2)
