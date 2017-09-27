# SRP
SRP는 'Single Responsibility Principle'로 모든 클래스나 모듈은 하나의 책임만 맡는다는 원칙이다.

## 실습
- SRP 원칙 적용 전
```java
class Car {
    void go() { ... }
    void stop() { ... }
    void checkOil() { ... }
    void drive() { ... }
}
```
- SRP 원칙 적용 후
```java
class Car {
    void go() { ... }
    void stop() { ... }
}
class Driver {
    void drive() { ... }
}
class Mechanic {
    void checkOil() { ... }
}
```
