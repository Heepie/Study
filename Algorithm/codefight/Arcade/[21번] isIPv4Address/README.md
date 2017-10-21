# isIPv4Address
Given a string, find out if it satisfies the IPv4 address naming rules.

> Example </br></br>
> For inputString = "172.16.254.1", the output should be
isIPv4Address(inputString) = true;</br>
For inputString = "172.316.254.1", the output should be
isIPv4Address(inputString) = false.

## 문제 분석
- 조건
  1. String 값이 주어지고 IPv4 주소 형식인지 구하는 문제</br></br>
- 문제 풀이 방법
  IPv4 주소는 "."으로 구분되고 0 ~ 255 사이의 숫자로 구성되어있다.
  1. 입력 String을 "."로 구분해 4개로 나눠지지 않는다면 false 반환
  2. "."로 나눠진 String이 0 ~ 255 사이의 값인지 판단해 모두 범위에 있다면 true 아니면 false 반환</br></br>

## 문제 풀이
```Java
boolean isIPv4Address(String inputString) {
  // 1. "."로 구분
  String[] value = inputString.split("\\.");

  // "."로 구분되지 않는다면 false 반환  
  if (value.length != 4)
      return false;

  for (int i=0; i<value.length; i=i+1) {
      try {
          // 2. 0 ~ 255 사이의 값인지 판단
          if(Integer.parseInt(value[i]) > 255 || Integer.parseInt(value[i]) < 0)
              return false;

      } catch(Exception e) {
          return false;
      }
  }

  return true;
}
```
