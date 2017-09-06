# 다양한 Api 정리

## String Api
스트링과 관련된 Api입니다.
1. length - 문자열의 길이를 출력해주는 메소드
```java
String str = "Oh heepie Day";
int length = str.length();
```

2. indexOf - 문자열의 위치를 리턴해주는 메소드
```java
int idx = str.indexOf("heepie");
```

3. split - 문자열을 파라미터로 구분해 결과를 문자열 배열에 저장하는 메소드  
```java
String tmp[] = str.split("/");
```

3. replace - 첫 번째 파라미터의 문자열을 두 번째 파라미터로 변경하는 메소드
```java
str.substring("Oh", "YOLO");
```

4. startsWith - 특정 문자열로 시작 여부를 boolean으로 알려주는 메소드
```java
boolean isStart = str.startsWith("heepie");
```

## Math와 Random Api
수학과 난수와 관련된 Api입니다.
1. abs - 절대값 출력해 주는 메소드
```java
Math.abs(-100);
```

2. round, ceil, floor - 반올림, 올림, 내림과 관련된 메소드
```java
Math.round(1.55);
Math.ceil(1.33);
Math.floor(1.88);
```

3. nextInt - 첫 번째 파라미터의 문자열
