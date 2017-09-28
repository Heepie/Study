# ISP
ISP는 '** Interface Segregation Principle **'로 특화된 여러 개의 인터페이스가 하나의 범용 인터페이스보다 낫다(유연하다.)는 원칙이다.</br>

## 실습
- ISP 원칙 적용 전
```java
interface IBird {
    public void fly();
    public void eat();
    public void chirp();
}
class Penguin implements IBird {
    @Override
    public void fly() {
        // TODO Auto-generated method stub
    }
    @Override
    public void eat() {
        // TODO Auto-generated method stub
    }
    @Override
    public void chirp() {
        // TODO Auto-generated method stub
    }
}
```
- ISP 원칙 적용 후
```java
interface Flyable {
    public void fly();
}
interface Eatable {
    public void eat();
}
interface Chirpable {
    public void chirp();
}
interface Swimable {
    public void swim();
}
class Penguin implements Eatable, Chirpable, Swimable {
    @Override
    public void swim() {
        // TODO Auto-generated method stub
    }
    @Override
    public void chirp() {
        // TODO Auto-generated method stub
    }
    @Override
    public void eat() {
        // TODO Auto-generated method stub
    }
}
```

예제처럼 범용적인 IBird이라는 인터페이스를 Penguin에서 구현하면 fly(), eat(), chirp() 메소드를 모두 구현해야 한다.</br>
그러나 범용적인 IBird 인터페이스 구현으로 Penguin의 날지 못하고 수영할 수 있는 **특성을 표현 할 수 없다**. </br>
그래서 특화된 3개의 인터페이스(Flyable, Eatable, Chirpable)로 분리하면 원하는 인터페이스를 유연하게 구현 할 수 있다.
