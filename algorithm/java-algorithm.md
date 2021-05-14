# 자바 알고리즘

## 1.String(문자열)
### 1-1.문자 찾기
Q.
특정 문자열이 주어지고 해당 문자열 안에서 특정 알파벳이 몇개가 있는지 구하는 문제.
(대소문자를 구분하지 않는다.)

A.
문제 풀이 케이스
1) 특정 문자열을 split한 배열을 하나씩 돌면서 특정 알파벳과 일치하는 것이 있는지 확인.
2) 특정 문자열의 각 자리를 charAt() 함수를 써서 특정 알파벳과 일치하는지 확인.
3) 특정 문자열을 toCharArray()을 이용하여 iterable하게 만든 후, for Each를 사용해 돌면서 특정 알파벳과 비교.

* String toUpperCase()
* static char toUpperCase(char ch)
* char charAt(int index)
* char[] toCharArray()
