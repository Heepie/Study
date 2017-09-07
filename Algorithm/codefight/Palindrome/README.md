# Palindrome

팰린드롬이란?  
팰린드롬(palindrome)은 거꾸로 읽어도 제대로 읽는 것과 같은 문장이나 낱말이다. -위키피디아(ko)-
```Java
  /**
   * palindrome 확인 알고리즘
   *
   * 한 개의 문자열을 받아 palindrome인지 확인하는 알고리즘
   * ex) 'aabaa'  -> true
   *     'ckkd'   -> false
   *     'a'      -> true
   *
   * 풀이법
   * 1. 가운데를 기준으로 X, Y로 구분
   * 2. X 범위 안의 값을 역순으로 Y 범위 안의 값과 비교
   * ex) 'acbca'  X의 역순 = 'ca', Y = 'ca'
   *
   * 3. 같다면 true, 다르면 false
   *
   * @param inputString
   * @return
   */
   static boolean checkPalindrome(String inputString) {
    char[] inputArray = inputString.toCharArray();

    int length = inputString.length();
    int midIdx, i, j;
    int xIdx, yIdx;
    char[] chrArray;

    // 가운데 Idx
    midIdx = length / 2;

    // X 부분의 배열 생성
    chrArray = new char[midIdx];

    // X 인덱스 설정
    xIdx = 0;

    // X 부분을 배열에 입력
    for(i=xIdx; i<midIdx; i=i+1) {
      chrArray[i] = inputArray[i];
    }

    // X 인덱스 갱신
    xIdx = i-1;

    // Y 인덱스 설정   
    if (length%2 == 0)
      yIdx = midIdx;		  // 짝수의 경우
    else
      yIdx = midIdx+1;		// 홀수의 경우

    // X 부분의 역순 배열과 Y부분 비교
    for(j=yIdx; j<length; j=j+1) {
      // 다른 로직이면 종료
      if (chrArray[xIdx-((j-yIdx))] != inputArray[j])
        return false;
    }

    return true;
}
```
