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

~~~
public String solution(String str) {
    String answer = "";
    for (char x : str.toCharArray()) {
        if (Character.isLowerCase(x)) answer += Character.toUpperCase(x);
        else answer += Character.toLowerCase(x);
    }
    return answer;
}
~~~

### 1-3. 문장 속 단어

Q.
한 문장 속에서 가장 긴 단어를 구하는 문제.
가장 길이가 긴 단어가 여러개일 경우, 문장의 가장 앞쪽에 위치한 단어를 답으로 한다.

A.
문제 풀이 케이스
(문자의 길이를 비교할 때
newKeyword.length() > max 이면 뒤에서 같은 길이의 단어가 등장해도 교체되지 않지만,
newKeyword.length() >= max 로 비교하면 뒷쪽 단어로 교체된다는 점에 주의할 것!)

1. 특정 문장을 white space로 split 한 배열을 for문으로 돌리며 가장 긴 단어인지 확인한다.
   가장 긴 단어이면 반환한다.
2. indexOf로 특정 문장의 white space 위치가 반환되면 다음 동작을 실행한다.
   substring을 사용하여 white space 이전까지의 단어를 뽑아 내어 가장 긴 단어인지 확인한다.
   마지막 단어는 white space가 포함되어 있지 않아 로직을 타지 않으므로 추가로 꼭 처리를 해주어야 한다.

- 필드 초기화
  ex)

```
int max = Integer.MIN_VALUE;
```

- String[] split(String regex)
- int indexOf(String str) : 처음 등장하는 위치를 반환한다. 해당 하는 것이 없으면 -1을 반환한다.
- String substring(int beginIndex, int endIndex) : beginIndex 부터 endIndex 전까지!

~~~
String solution(String str) {
    String result = "";
    int max = Integer.MIN_VALUE;

    for(String keyword : str.split(" ")) {
        if (keyword.length() > max) {
            max = keyword.length();
            result = keyword;
        }
    }
    return result;
}
~~~