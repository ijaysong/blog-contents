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

### 1-2.대소문자 변환
Q.
문자열은 영어 알파벳으로만 구성되어 있으며, 문자열의 길이는 100을 넘지 않는다.
대문자는 소문자로, 소문자는 대문자로 변환된 문자열을 출력한다.

A.
문제 풀이 케이스
1) 대문자를 담은 배열과 소문자를 담은 배열을 준비하여 문자열의 각 자리 수를 돌면서 대문자 배열에 속하는지 아닌지 확인한다. 
   대문자이면 소문자로 변환하고, 소문자이면 대문자로 변환한다.
2) toCharArray()를 사용하여 문자열을 array로 만들고 forEach문을 사용해서 돌린다.
    각각의 문자가 소문자인지 대문자인지 구별하여 소문자이면 대문자로, 대문자이면 소문자로 변환한다.

* static boolean isLowerCase(char ch)
* static boolean isUpperCase(char ch)
* ascii code 65~90 : 대문자
* ascii code 97~122 : 소문자 (대소문자는 32 차이가 남)