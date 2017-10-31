# 서비스(Service) 실습 - Notification

## 개념
Notification는 상태표시줄에 서비스의 기능을 알려준다.</br>

![concept1](http://cfile10.uf.tistory.com/image/99DD423359DE04C8158064)</br>

## 실습 1 (startService + Notification)
- MainActivity
```java
public class MyService extends Service {
    // ...
    @Override    
    public int onStartCommand(Intent intent, int flags, int startId) {
        setNotification();
        return super.onStartCommand(intent, flags, startId);
    }
    // ...

    // 알람의 고유 번호 cf) StartActivityForResult의 requestCode와 동일 기능
    private final int TEST_FLAG = 111;

    private void setNotification() {
        // 알람을 관리하는 알람 매니저 설정
        NotificationManager notificationManager
                = (NotificationManager)getSystemService(Context.NOTIFICATION_SERVICE);

        // 알람 알리기
        notificationManager.notify(TEST_FLAG, makeNotification());
    }

    private Notification makeNotification() {        
        // 알람바 변수
        Notification notification=null;

        // 알람바를 생성하기 위한 빌더 변수, 빌더 패턴
        NotificationCompat.Builder notifBuilder = new NotificationCompat.Builder(this);

        Bitmap largeIcon = BitmapFactory.decodeResource(getResources(), R.mipmap.up);

        // 빌더에 설정
        notifBuilder.setContentTitle("Content Title")
                    .setContentInfo("Content Info")
                    .setContentText("Content Text")
                    .setProgress(100, 20, false)
                    .setCategory("Category")
                    .setSmallIcon(R.mipmap.happy)
                    .setLargeIcon(largeIcon);

        // 빌더를 통해 알람바 생성
        notification = notifBuilder.build();

        return notification;
    }
}
```

## 실습 2 (bindService + Notification)
- MainActivity
```java
public class MyService extends Service {
    // ...
       @Override    
    public IBinder onBind(Intent intent) {
        customBinder = new CustomBinder();
        setNotification();
        return customBinder;
    }    
// ...
    // 알람의 고유 번호 cf) StartActivityForResult의 requestCode와 동일 기능
    private final int TEST_FLAG = 111;

    private void setNotification() {
        // 알람을 관리하는 알람 매니저 설정
        NotificationManager notificationManager
                = (NotificationManager)getSystemService(Context.NOTIFICATION_SERVICE);

        // 알람 알리기
        notificationManager.notify(TEST_FLAG, makeNotification());
    }

    private Notification makeNotification() {        
        // 알람바 변수
        Notification notification=null;

        // 알람바를 생성하기 위한 빌더 변수, 빌더 패턴
        NotificationCompat.Builder notifBuilder = new NotificationCompat.Builder(this);

        Bitmap largeIcon = BitmapFactory.decodeResource(getResources(), R.mipmap.up);

        // 빌더에 설정
        notifBuilder.setContentTitle("Content Title")
                    .setContentInfo("Content Info")
                    .setContentText("Content Text")
                    .setProgress(100, 20, false)
                    .setCategory("Category")
                    .setSmallIcon(R.mipmap.happy)
                    .setLargeIcon(largeIcon);

        // 빌더를 통해 알람바 생성
        notification = notifBuilder.build();

        return notification;
    }
}
```

## 스크린 샷
![screenshot](http://cfile29.uf.tistory.com/image/9986DA3359E09873313EBB)</br>
