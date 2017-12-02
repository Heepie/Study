# OCP
LSP는 'Liskov Substitution Principle'로 "**모든 구성요소는 확장에는 열려 있고 수정에는 닫혀있다.**"는 원칙이다. </br>

## 실습
'카니발'이라는 차가 이번에 새로 출시되어 하드웨어 성능이 올라가 가속도가 높아졌다고 가정하고 코드에 적용해보자. (m/s^2는 가속도 단위)
- OCP 원칙 적용 전
```java
class Carnival {
    void accelerate() {
        System.out.println("10m/s^2");
    }
}
// 직접 Carnival 클래스 코드 수정
class Carnival {
    void accelerate() {
        System.out.println("20m/s^2");
    }
}
```
- OCP 원칙 적용 후
```java
class Carnival {
    void accelerate() {
        System.out.println("10m/s^2");
    }
}
// Carnival 클래스 확장 후 메소드 오버라이딩
class NewCarnival extends Carnival{
    @Override
    void accelerate() {
        System.out.println("20m/s^2");        
    }
}
```
OCP 원칙을 적용하면 기존의 코드를 직접 수정하는 것이 아니라(수정에 닫혀있다) 해당 코드를 상속 받아 코드를 수정해야 한다.(확장에는 열려있다)

## 장점
- 이전 버전이 모두 호환 가능하다. (기존 코드는 수정하지 않기 때문에)
