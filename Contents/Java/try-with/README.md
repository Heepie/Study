# JVM 메모리 영역
JVM 메모리 영역은 Runtime Data Area라고 불린다. JVM이 운영체제 위에 실행되면 할당 받는 메모리 영역이다. JVM 메모리 영역의 구성은 아래 그림과 같다.</br>
![jvm_memory_area](http://cfile1.uf.tistory.com/image/99B8CE3359B1DEBB3829DA)</br>
***
## 메소드 영역(Method Area)
컴파일 결과인 클래스(~.class)를 클래스 로더로 읽어 생성된다. 이 영역은 JVM이 시작할 때 생성되고 모든 쓰레드가 공유하는 영역이다.</br></br>

## JVM 스택 영역 (JVM Stack Area)
각 쓰레드마다 하나씩 존재하며 쓰레드가 시작될 때 할당되는 영역이다. 자바에서 기본적으로 main 쓰레드 1개가 존재하고 쓰레드를 생성할 때마다 1개씩 증가한다.</br></br>

## 힙 영역(Heap Area)
객체와 배열이 생성되는 영역이다. 생성된 객체와 배열은 JVM 스택 영역의 변수나 객체에서 참조한다. 그렇기 때문에 JVM 스택 영역에서 변수나 객체가 참조하지 않으면 의미가 없어진다. 이렇게 의미가 없어지면 JVM은 Garbage Collector를 통해 해당 변수나 객체를 힙 영역에서 자동으로 제거한다.
