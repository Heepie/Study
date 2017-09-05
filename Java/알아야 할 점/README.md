# 알아야 할 점

* ## JIT VS AOT
  - JIT(just-in-time compile)으로 동적 컴파일과 정적 컴파일을 모두 사용한 방식이다. 코드 실행 시점에서 필요하다고 예성되는 코드만 컴파일하는 방법이다. 이를 통해 성능은 향상되었지만 실행 시마다 하드웨어에 큰 부하를 주는 것이 단점이다.
  - AOT(ahead-of-time compile) 코드가 실행되기 전 한번에 컴파일 완료 후 캐시 메모리를 통해 공유해 사용하는 방법이다.
![jit_vs_aot](https://www.ibm.com/support/knowledgecenter/SSSTCZ_3.0.0/com.ibm.wrt.rtlinux.doc.30/realtime/rt2_aot.gif)

* ## 기본 연산 시 주의 할 점
  - 일반적으로 소수는 모두 double형으로 간주되기 때문에 float는 float라는 것을 명시하기 위해 접미사를 붙인다.
  ```JAVA
  float d = 3.14(X) / float d = 3.14F(O)  
  ```
  - 일반적으로 정수는 모두 int형으로 간주되기 때문에 long 또한 long이라는 것을 명시하기 위해 접미사를 붙인다.
  ```JAVA
  long y = 2147482648(X) / long y = 2147482648L(O)
  ```
  - 실수 연산은 직접 처리하지 않도록 노력한다.
  ```JAVA
  public void compareDouble(double x, double y) {
      if (x == y)
        System.out.println("X == Y");
      else
        System.out.println("X != Y");
  } (X)

  public void compareDouble(double x, double y) {
      if (Double.compareDouble(x, y) == 0)
        System.out.println("X == Y");
      else
        System.out.println("X != Y");
  } (O)
  ```
