# OOP와 SOLID
OOP란 **Object-Oriented Programming** 로 객체 지향 프로그래밍을 의미한다. 한국어로는 객체 지향 프로그래밍이다. 'Java'는 대표적인 객체 지향 프로그래밍 언어

### 객체지향 프로그래밍의 개념
객체 지향 프로그래밍은 <u>**'객체(Object)'**</u>를 <u>**'잘 사용해서 좋은 코드(Oriented)'**</u>를 <u>**'만드는 방법(Programming)'**</u></br>
객체라는 개념을 통해 현실 세계를 컴퓨터 세계로 잘 반영하는 것이 객체 지향 프로그래밍이라고 생각</br>
![Object](http://cfile3.uf.tistory.com/image/9907133359B1277416B9BE)</br>
객체란 메모리 안의 주소로서 변수, 함수, 데이터 구조 등이고 객체가 모여 객체가 될 수도 있다.

***
SOLID란 OOP의 5대 원리의 앞글자를 따온 것</br>OOP에 대해 아래서 자세히 살펴보자.
### SRP - Single Responsibility Principle
![SRP](http://cfile2.uf.tistory.com/image/993A5D3359AFD6562DED93)</br>
모든 클래스나 모듈은 하나의 책임만 맡는다는 원칙</br></br>
**실습**
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

### OCP - Open Closed Principle
![OCP](http://cfile3.uf.tistory.com/image/99CE973359AFD7180541BD)</br>모든 구성요소는 확장에는 열려 있고 수정에는 닫혀있다는 원칙</br></br>
**실습**</br>
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

### LSP - Liskov Substitution Principle
**"객체 T는 객체 T의 특성변화 없이 객체 S로 대체되어야 한다." **는 원칙이다. 중요한 것은 특성변화 없이 대체되어야 한다는 것이다.</br>

**실습**</br>

### ISP - Interface Segregation Principle
![ISP](http://cfile1.uf.tistory.com/image/9964833359AFDD6A14FCAC)</br>
특화된 여러 개의 인터페이스가 하나의 범용 인터페이스보다 낫다(유연하다.)는 원칙</br></br>
**실습**  
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

예제처럼 범용적인 IBird이라는 인터페이스를 Penguin에서 구현하면 fly(), eat(), chirp() 메소드를 모두 구현해야 한다.
그러나 범용적인 IBird 인터페이스 구현으로 Penguin의 날지 못하고 수영할 수 있는 **특성을 표현 할 수 없다**.
그래서 특화된 3개의 인터페이스(Flyable, Eatable, Chirpable)로 분리하면 원하는 인터페이스를 유연하게 구현 할 수 있다.

### DIP - Dependency Inversion Principle
의존 관계 역전</br>
추상화 된 것은 구체적인 것에 의존하면 안된다.
