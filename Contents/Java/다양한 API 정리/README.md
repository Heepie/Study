# 다양한 API 정리
개인적으로 혼돈하기 쉬운 Java Api 정리입니다. 더 자세한 Api는 [공식 Java API Doc](http://docs.oracle.com/javase/8/docs/api/index.html)에서 확인 할 수 있습니다.
## String API
스트링과 관련된 Api입니다.
1. length - 문자열의 길이를 출력해주는 메소드
```java
String str = "Oh heepie Day";
int length = str.length();                        // 14
```

2. indexOf - 문자열의 위치를 리턴해주는 메소드
```java
int idx = str.indexOf("heepie");                  // 4
```

3. split - 문자열을 파라미터로 구분해 결과를 문자열 배열에 저장하는 메소드  
```java
String tmp[] = str.split("/");                    // Oh , heepie Day
```
4. substring - 문자열을 구분하는 메소드
```java
String subString = str.substring(2, 10);          // ! heepie
```

5. replace - 첫 번째 파라미터의 문자열을 두 번째 파라미터로 변경하는 메소드
```java
String newString = str.replace("Oh", "YOLO");     // YOLO! heepie Day
```

6. startsWith - 특정 문자열로 시작 여부를 boolean으로 알려주는 메소드
```java
boolean isStart1 = str.startsWith("heepie");       // false
boolean isStart2 = str.startsWith("Og");           // true
```

## Math와 Random API
수학과 난수와 관련된 Api입니다.
1. abs - 절대값 출력해 주는 메소드
```java
double a = Math.abs(-100);                        // 100
```

2. round, ceil, floor - 반올림, 올림, 내림과 관련된 메소드
```java
double b = Math.round(1.55);                      // 2.0
double c = Math.ceil(1.33);                       // 2.0
double d = Math.floor(1.88);                      // 1.0
```

3. nextInt - 0 ~ 첫 번째 문자열 범위 안에서 랜덤 값을 반환하는 메소드
```java
Random random = new Random();
int rndValue = random.nextInt(100);
System.out.println(rndValue);                     // 0~100사이(100 포함X) 중 랜덤 값 반환
```
