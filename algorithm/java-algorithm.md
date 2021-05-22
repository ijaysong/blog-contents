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

~~~
int Solution (String str, char c) {
    int answer = Integer.MIN_VALUE;
    str = str.toUpperCase();
    c = Character.toUpperCase(c);
    for (char x : str.toCharArray()) {
        if (x === c) {
            answer++;
        }
    }
    return answer;
}
~~~

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

### 1-4. 단어 뒤집기

Q.
N개의 단어가 주어지면 각 단어를 뒤집어 출력하는 문제.
뒤집은 단어를 한줄 한줄 표시할 것.

A.
문제풀이 케이스

1. white space로 단어를 구분하여 Array에 저장한다. StringBuilder의 reverse()를 사용하여 문자열의 순서를 뒤집어 출력한다.

- StringBuilder(String str)
- StringBuilder reverse()

* String 클래스가 있는데 왜 StringBuilder 클래스가 있을까?
  String 연산을 할때 마다 객체가 새롭게 생긴다.
  반면에 StringBuilder 클래스는 연산을 하여도 객체가 하나만 생성되기 때문에 메모리 낭비가 적다.
  그래서 문자열 연산을 많이 할 경우에는 StringBuilder를 사용하는 것이 좋다.

ex)

~~~
String a = "aa";
String b = "bb";
String c = a + b;
~~~

=> String 객체 a, b, c가 각각 생성된다.

~~~
void Solution(string str) {
   String[] keywords = str.split(" ");

   for(string keyword: keywords) {
      string reversed = new StringBuilder(keyword).reverse().toString();
      System.out.println(reversed);
   }
}
~~~

Q.
단어 안에서 특정 조건(문자 앞뒤 쌍을 이루는 것)에 맞는 문자만 뒤집어 출력하는 문제.
뒤집은 단어를 한줄 한줄 표시할 것.
ex) study -> yduts, good -> doog

A.
문제풀이 케이스

1. white space로 단어를 구분하여 Array에 저장한다. 단어를 Char 타입으로 바꾸어 각 자리의 글자를 바꿔준다.

- char[] toCharArray()
- static String valueOf(char[] data)

~~~
void Solution(string str) {
  String[] keywords = str.split(" ");

  for(string keyword: keywords) {
     char[] charArr = keyword.toCharArray();
     int lt = 0, rt = x.length() -1;
     while (lt < rt) {
        char tmp = charArr[lt];
        charArr[lt] = charArr[rt];
        charArr[rt] = tmp;
        lt++;
        rt--;
     }
     System.out.println(String.valueOf(charArr));
  }
}
~~~

### 1-5. 특정 문자 뒤집기
Q. 
길이가 100을 넘지 않는 문자열이 주어진다. 
알파벳만 뒤집힌 문자열을 출력한다.
ex)
a#b!GE*T@S => S#T!EG*b@a

A.
문제풀이 케이스

1. 문자열의 왼쪽 끝과 오른쪽 끝의 문자가 둘다 알파벳인지 확인한다. 알파벳이면 위치를 교환한다.
   그리고 왼쪽을 나타내는 지표의 값은 증가, 오른쪽을 나타내는 지표의 값은 감소 시킨다.

- char[] toCharArray()
- static boolean isAlphabetic(int codePoint)
- static String valueOf(char[] data)
