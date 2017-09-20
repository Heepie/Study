# Activity 생명주기(Life Cycle)
안드로이드의 액티비티는 **사람과 같이 Activity 탄생에서 죽음까지 생명주기**가 있다. 다양한 조건에 따라 생명주기는 변한다.
지금은 2가지 조건을 살펴보자.</br>
 1) 기본 액티비티 A 위에 액티비티 B가 호출되어 전체를 가릴 경우</br>
 2) 기본 액티비티 A 위에 액티비티 B가 호출되어 투명하거나 일부를 가릴 경우
이다.</br>
액티비티 B가 투명하거나 일부를 가리는 예로는 '로딩 중'인 프로그레스바나 팝업 등이 있다.


## 전체를 가릴 경우
- ### 생명주기
![all](http://cfile4.uf.tistory.com/image/992CE63359C25205192B52)</br>

- ### 실습
![all_test](http://cfile6.uf.tistory.com/image/99FF513359C250BA3A4B12)

## 부분을 가릴 경우
- ### 생명주기
![part](http://cfile23.uf.tistory.com/image/996C8A3359C2521332AAF6)</br>

- ### 실습
![part_test](http://cfile30.uf.tistory.com/image/99E71C3359C250E627A663)
