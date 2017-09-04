# JAVA

* ## JIT VS AOT
  - JIT(just-in-time compile)으로 동적 컴파일과 정적 컴파일을 모두 사용한 방식이다. 코드 실행 시점에서 필요하다고 예성되는 코드만 컴파일하는 방법이다. 이를 통해 성능은 향상되었지만 실행 시마다 하드웨어에 큰 부하를 주는 것이 단점이다.
  - AOT(ahead-of-time compile) 코드가 실행되기 전 한번에 컴파일 완료 후 캐시 메모리를 통해 공유해 사용하는 방법이다.
![jit_vs_aot](https://www.ibm.com/support/knowledgecenter/SSSTCZ_3.0.0/com.ibm.wrt.rtlinux.doc.30/realtime/rt2_aot.gif)
