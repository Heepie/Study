# LSP
LSP는 'Liskov Substitution Principle'로 "객체 T는 객체 T의 특성변화 없이 객체 S로 대체되어야 한다."는 원칙이다. 중요한 것은 특성변화 없이 대체되어야 한다는 것이다.</br>

즉, **상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다.**

![LSP2](http://cfile6.uf.tistory.com/image/99F73A335A2BD4553604BA)
```java
class T {

}

class S extends T {

}
```
