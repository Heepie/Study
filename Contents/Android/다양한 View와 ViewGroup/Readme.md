# 각종 View와 ViewGroup
View는 **사용자와 통신하기 위한 객체**이고</br>
View Group은 **직접 보이지는 않지만 다른 View를 담는 컨테이너의 역할을 하는 View**이다.</br>

상속관계는 아래 그림과 같다. (※ 상속 관계의 전부가 아닌 일부이다.)</br>
![inheritance](http://cfile10.uf.tistory.com/image/9952343359BBAA2D10E19E)
### 토글 버튼
```java
// 여러개의 리스너 설정 가능
toggleButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        switch (view.getId()) {
            case R.id.btnToggle:
                Toast.makeText(getApplicationContext(),
                                            "클릭 토글", Toast.LENGTH_LONG).show();
                break;
        }
    }
});

// Default는 'off'이고 클릭 여부는 false
toggleButton.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(CompoundButton compoundButton, boolean check) {
        switch (compoundButton.getId()) {
            case R.id.btnToggle:
                if (check)
                    Toast.makeText(getApplicationContext(),
                                            "on 토글", Toast.LENGTH_LONG).show();
                else
                    Toast.makeText(getApplicationContext(),
                                            "off 토글", Toast.LENGTH_LONG).show();
                break;
        }
    }
});

```

### 체크 버튼
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    // ...
    // 리스너 설정
    chk1.setOnCheckedChangeListener(onCheckedChangeListener);
    chk2.setOnCheckedChangeListener(onCheckedChangeListener);
    chk3.setOnCheckedChangeListener(onCheckedChangeListener);
    // ...
}

// 체크 버튼 리스너 선언
CompoundButton.OnCheckedChangeListener onCheckedChangeListener
            = new CompoundButton.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(CompoundButton compoundButton, boolean check) {
        switch (compoundButton.getId()) {
            case R.id.chk1:
                if (check)
                    Toast.makeText(getApplicationContext(),
                            "checkBox1 seleced", Toast.LENGTH_LONG).show();
                else
                    Toast.makeText(getApplicationContext(),
                            "checkBox1 unseleced", Toast.LENGTH_LONG).show();
                break;
            case R.id.chk2:
                if (check)
                    Toast.makeText(getApplicationContext(),
                            "checkBox2 seleced", Toast.LENGTH_LONG).show();
                else
                    Toast.makeText(getApplicationContext(),
                            "checkBox2 unseleced", Toast.LENGTH_LONG).show();
                break;
            case R.id.chk3:
                if (check)
                    Toast.makeText(getApplicationContext(),
                            "checkBox3 seleced", Toast.LENGTH_LONG).show();
                else
                    Toast.makeText(getApplicationContext(),
                            "checkBox3 unseleced", Toast.LENGTH_LONG).show();
                break;

        }
    }
};

```

### 라디오 버튼
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    // ...
    // 라디오 버튼 리스너 설정
    radioGroup.setOnCheckedChangeListener(radioListener);    
    // ...
}

// 라디오 버튼 리스너 선언
RadioGroup.OnCheckedChangeListener radioListener = new RadioGroup.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(RadioGroup radioGroup, @IdRes int i) {
        switch (i) {
            case R.id.radio1:
                Toast.makeText(getApplicationContext(),
                                        "radio1 seleced", Toast.LENGTH_LONG).show();
            break;
            case R.id.radio2:
                Toast.makeText(getApplicationContext(),
                                        "radio2 seleced", Toast.LENGTH_LONG).show();
                break;
            case R.id.radio3:
                Toast.makeText(getApplicationContext(),
                                        "radio3 seleced", Toast.LENGTH_LONG).show();
                break;
        }
    }
};

```

### 스위치와 프로그래스바
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    // ...
    // 스위치 버튼 리스너 설정        
    mSwitch.setOnCheckedChangeListener(switchListener);    
    // ...
}

// 스위치 버튼 리스너 선언
CompoundButton.OnCheckedChangeListener switchListener
                                = new CompoundButton.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(CompoundButton compoundButton, boolean check) {
        switch (compoundButton.getId()) {
            case R.id.mSwitch:
                if (check)
                    progressBar.setVisibility(View.INVISIBLE);
                else
                    progressBar.setVisibility(View.VISIBLE);
                break;
        }
    }
};

```

### SeekBar
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    // ...
    // SeekBar 리스너 설정        
    seekBar.setOnSeekBarChangeListener(seekBarChangeListener);    
    // ...
}

// SeekBar 리스너 선언
SeekBar.OnSeekBarChangeListener seekBarChangeListener
            = new SeekBar.OnSeekBarChangeListener() {

    // SeekBar가 변경되었을 때 동작하는 메소드
    @Override
    public void onProgressChanged(SeekBar seekBar, int current, boolean b) {
        seekBarResult.setText(current+"");
    }

    // SeekBar가 터치 되었을 때 동작하는 메소드
    @Override
    public void onStartTrackingTouch(SeekBar seekBar) {

    }
 
    // SeekBar의 터치 떼었을 때 동작하는 메소드
    @Override
    public void onStopTrackingTouch(SeekBar seekBar) {

    }
};

```

## 스크린 샷
![screenshot](http://cfile23.uf.tistory.com/image/9973173359BBAF22267B75)
