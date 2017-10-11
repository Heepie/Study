# 서비스(Service) 개념과 알아야할 점

## 개념

![concept1](http://cfile10.uf.tistory.com/image/993BFA3359DCBF8D337EB7)</br>
출처 - 안드로이드 공식 문서</br></br>
서비스의 특징은 </br>
1) Xml이 없고 백그라운드에서 실행되고</br>
2) 사용자가 new 키워드를 통해 호출하는 것이 아니라 시스템이 호출</br>
한다.</br>

## 사용 방법
![how_to_use](http://cfile25.uf.tistory.com/image/99E8C73359DCC068285F74)

## 알아야 할 점
![noti](http://cfile21.uf.tistory.com/image/99C05F3359DCC65D18CF91)
그림과 같이 Service를 호출한 Activity와 Service는 동일한 Thread로 동작하기 때문에 병렬적으로 동작하지 않는다.</br>
이를 해결하기 위해서는 Service를 새로운 Thread를 생성해 처리해주면 된다.</br>
