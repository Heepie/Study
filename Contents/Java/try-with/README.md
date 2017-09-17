# try-with 개념과 실습

## 개념
try-with문은 Java 7부터 지원하는 개념으로 try statement에 선언된 **리소스(close해주어야 하는)를 try statement 종료 후 자동으로 close해주는 장점** 이 있다.

## 실습
- Java 7 이전
```Java
try {
    fos = new FileOutputStream(database, true);
    OutputStreamWriter osw = new OutputStreamWriter(fos);
    BufferedWriter bw = new BufferedWriter(osw);
    String row = item.no + COLUMN_SEP + item.name + "\n";

    bw.append(row);
    bw.flush();
    } catch (Exception e) {
        e.printStackTrace();
    } finally {
        if (fos != null) {
        try {
            fos.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

- Java 7 이후
```Java
try (FileOutputStream fos = new FileOutputStream(database, true)){
    OutputStreamWriter osw = new OutputStreamWriter(fos);
    BufferedWriter bw = new BufferedWriter(osw);
    String row = item.no + COLUMN_SEP + item.name + "\n";

    bw.append(row);
    bw.flush();
} catch (Exception e) {
    e.printStackTrace();
}
```

기존의 try-catch문을 사용 할 경우, FileOutputStream을 finally문을 통해 닫아주어야한다. 그리고 FileOutputStream을 닫는 것 또한 try-catch문으로 감싸줘야한다. </br>

그러나 try-with문을 사용할 경우, FileOutputStream을 try 구문의 변수로 설정해 자동 close를 보장받는다. 이를 통한 이점은 </br>
1) 코드의 가독성(finally 없어짐)</br>
2) 기존 코드에서는 FileOutputStream를 닫기 위해 try 밖에 FileOutputStream변수를 선언했는데 하지 않아도 됨

있다.
