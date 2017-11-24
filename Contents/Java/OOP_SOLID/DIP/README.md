# DIP - Dependency Inversion Principle
![DIP](http://cfile26.uf.tistory.com/image/99ECD43359BCF1E72ABBA0)
1. 상위 모듈이 하위 모듈에 의존하면 안된다. 둘 다 추상화에 의존해야한다.
2. 추상화된 것이 구체적인 것에 의존하면 안된다. 구체적인 것이 추상화에 의존해야한다.</br>

## 실습
추상화에 의존해야한다는 것은 상위 모듈이 하위 모듈을 생성 할 때 객체를 직접 생성하는 것이 아니라 Interface나 abstract를 통해 생성한다는 것을 의미한다.
- DIP 원칙 적용 전
```java
class Add {
    public void add (int a, int b) {
        System.out.println("++합은 "
                + a + b + "입니다.++");
    }
}
class Calculator {
    private Add addClass;

    Calculator() {
        addClass = new Add();
    }

    public void add (int a, int b) {
        addClass.add(a, b);
    }
}
```

- DIP 원칙 적용 후
```java
interface Iadd {
    void add(int a, int b);
}
class Add implements Iadd {

    @Override
    public void add(int a, int b) {
        System.out.println("++ Sum is "
                     + a + b + ".");
    }
}
class Calculator {
    private Iadd addClass;
    
    Calculator() {
        addClass = new Add();
    }

    public void add (int a, int b) {
        addClass.add(a, b);
    }
}
```
