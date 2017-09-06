# Anagram
아나그램이란?  
일종의 말장난으로 어떠한 단어의 문자를 재배열하여 다른 뜻을 가지는 다른 단어로 바꾸는 것을 말한다. - 나무위키-

```Java
/**
* 아나그램 알고리즘
*
* 두 개의 문자열 입력을 받아서 두 개의 관계가 아나그램 관계인지 확인하는 알고리즘
* ex) 'cat', 'atc'     -> true
*     'hello', 'olleh' -> true
*     'take', 'kata'   -> false
*
* 풀이법
* 1. 받은 문자열의 길이 체크 -> 길이가 다르면 로직 실행 X
* 2. 받은 문자열 정렬
* 3. 정렬된 문자열을 비교
*
* @param str1
* @param str2
* @return
*/
public static boolean isAnagram(String str1, String str2) {
	boolean ret = false;

	// 문자열 별 길이 확인
	if (str1.length() != str2.length())
		return ret;

	// 정렬하기 위해 String -> char 배열로 변환
	char[] cArray1 = str1.toCharArray();
	char[] cArray2 = str2.toCharArray();

	// 정렬
	Arrays.sort(cArray1);
	Arrays.sort(cArray2);

// Log ----
//	for (char c : cArray1)
//		System.out.print(c + " ");
//	System.out.println("");
//	for (char c : cArray2)
//		System.out.print(c + " ");
// ----

	// 배열 비교
	ret = Arrays.equals(cArray1, cArray2);

	return ret;
}
```
