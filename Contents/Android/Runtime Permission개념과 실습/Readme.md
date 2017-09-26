# Runtime Permission
## 개념
Runtime Permission은 구글I/O가 2015년 5월 28~29일 공개한 마시멜로우 버전(API레벨 23)부터 적용된 개념이다. </br>
Runtime Permission은 앱 사용 중 사용자로부터 승인 받아 사용하는 권한입니다.</br>
마시멜로우 버전 전과 후의 Permission은 아래 그림과 같다.</br>
![runtime_permission](http://cfile23.uf.tistory.com/image/99D64A3359C8C7822429C5)

- **마시멜로우 이전 버전** </br>
사용자 입장에서 Play store에 저장된 앱을 설치 할 때 요구하는 권한에 모두 동의해야했다.
개발자 입장에서는 앱에 필요한 권한을 AndroidManifest.xml에 선언만하면 되었다.

- **마시멜로우 이후 버전** </br>
마시멜로우 이후 버전부터는 앱 실행 중 사용자에게 허락을 받아서 사용해야된다.

## 실습
- Step1. AndroidManifest.xml 등록
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.heepie.day022_permisstion">    
    <!-- ...-->    

    <!-- 권한 설정 -->
    <!-- 런타임 권한, 자바 코드로 설정 필요 O -->
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>

    <!-- 빌드타임 권한, 자바 코드로 설정 필요 X -->
    <uses-permission android:name="android.permission.INTERNET"/>

    <!-- ...-->
</manifest>
```
- Step2. MainActivity
```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 앱 버전 체크, M은 마시멜로우를 의미, M아래 버전은 fullname 사용
        // 마시멜로우 이상 버전일 경우, 권한 체크 진행
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
            checkPermission();
        else {
            // 액티비티 초기화 이후 진행
        }
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void checkPermission() {
        // 1. 권한이 있을 경우
        if (((checkSelfPermission(Manifest.permission.READ_EXTERNAL_STORAGE) ==
                                        PackageManager.PERMISSION_GRANTED)) &&
            (checkSelfPermission(Manifest.permission.WRITE_EXTERNAL_STORAGE)) ==
                                        PackageManager.PERMISSION_GRANTED) {
            // 액티비티 초기화 이후 진행
        // 2. 권한이 없을 경우
        } else {
            // 2-1. 요청 권한 변수 설정
            String permission[] = { Manifest.permission.READ_EXTERNAL_STORAGE,
                                    Manifest.permission.WRITE_EXTERNAL_STORAGE};
            // 2-2. 권한 요청
            // 파라미터 (요청 권한 변수, 고유 요청 번호)
            requestPermissions(permission, 999);
        }

    }

    // 3. 권한 요청에 따른 동작
    // 파라미터 (고유 요청 번호, 요청한 권한, 요청 결과)
    @Override
    public void onRequestPermissionsResult(int requestCode,
                                           @NonNull String[] permissions,
                                           @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        switch (requestCode) {
        case 999:
            if (grantResults[0] == PackageManager.PERMISSION_GRANTED
                    && grantResults[1] == PackageManager.PERMISSION_GRANTED) {

                // 액티비티 초기화 이후 진행
            }
            break;
        }
    }
}
```

## 스크린 샷
API 19인 키켓에서는 Runtime Permission이 실행되지 않고
API 23인 마시멜로우에서는 Runtime Permission이 실행되는 것을 볼 수 있다.
![screenshot](http://cfile27.uf.tistory.com/image/996CDD3359C8F2531AE129)
