# arrayMaximalAdjacentDifference
Given an array of integers, find the maximal absolute difference between any two of its adjacent elements.

> Example </br></br>
> For inputArray = [2, 4, 1, 0], the output should be
arrayMaximalAdjacentDifference(inputArray) = 3.

## 문제 분석
- 조건
  1. 배열 주어지고 인접한 두 수의 차의 절대값 중 가장 큰 값을 구하는 문제</br></br>
- 문제 풀이 방법
  1. 인접 두 수의 차의 절대값을 구한다.(Math 클래스 사용)
  2. 절대값을 비교해 최대값을 갱신한다.</br></br>

## 문제 풀이
```Java
int arrayMaximalAdjacentDifference(int[] inputArray) {
  // 최대값을 저장할 변수 설정
  int max=-1;

	// 인접한 두 수 차이를 구함
  for(int i=0; i<inputArray.length-1; i=i+1) {
	// 최대값과 비교해 절대값 갱신
  if (Math.abs(inputArray[i] - inputArray[i+1]) > max )
    max = Math.abs(inputArray[i] - inputArray[i+1]);
  }

  return max;
}
```
