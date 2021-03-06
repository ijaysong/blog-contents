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

~~~
public String Solution(String str) {
    String answer;
    char[] charArr = str.toCharArray();
    int lt = 0, rt = str.length() -1;

    while (lt < rt) {
        if (!Character.isAlphabetic(charArr[lt])) lt++;
        else if (!Character.isAlphabetic(charArr[rt])) rt--;
        else {
            char tmp = charArr[lt];
            charArr[lt] = charArr[rt];
            charArr[rt] = tmp;
            lt++;
            rt--;
        } 
    }
    answer = String.valueOf(charArr);
    return answer;
}
~~~

### 1-6. 중복문자제거
Q.
소문자로 된 한개의 문자열이 입력되면 중복된 문자를 제거하고 출력한다.
중복이 제거된 문자열의 각 문자는 원래 문자열의 순서를 유지한다.

ex) ksekkset => kset

A.
문제풀이 케이스

1. 주어진 문자열을 각 자리별로 돌면서 첫번째 등장하는 위치와 현재 돌고 있는 위치가 일치하는지 판단하여 일치하면 그대로 두고, 일치하지 않는다면 제외시킨다. (문자열의 첫번째 위치만 반환하는 indexOf()의 특성을 활용한 것)

- int indexOf(String str) : 처음 등장하는 위치를 반환한다. 해당 하는 것이 없으면 -1을 반환한다.
- char charAt(int index)

~~~
public String solution(String str) {
    String answer = "";
    for (int i = 0; i < str.length(); i++) {
        if (str.indexOf(str.charAt(i)) == i) {
            answer += str.charAt(i);
        }
    }
    return answer;
}
~~~

### 1-7. 회문문자열
앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열을 회문 문자열이라고 한다.
회문 문자열이 입력되면 YES를, 회문 문자열이 아니면 NO를 출력하는 프로그램을 작성하라.
단, 회문을 검사할 때 대소문자를 구분하지 않는다.
ex) gooG => YES

A.
문제풀이 케이스

1. 주어진 문자열을 다 대문자로 만든다. 문자열을 절반으로 나누어 절반은 왼쪽 끝에서, 절반은 오른쪽 끝에서 시작하여 서로의 값이 같은지 비교한다. 

* String toUpperCase()


~~~
public String Solution(String str) {
    String answer = "YES";
    str = str.toUpperCase();
    int len = str.length();
    for (int i = 0; i < len/2; i++) {
        if (str.charAt(i) != str.charAt(len - i -1)) return "NO";
    }
}
~~~

### 1-8.유효한 팰린드롬(replaceAll 정규식 이용)

Q.
앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열을 팰린드롬이라고 한다.
입력된 문자열이 팰린드롬이면 "YES", 아니면 "NO"를 출력한다.
단, 회문을 검사할 때 알파벳만 가지고 회문을 검사하며, 대소문자를 구분하지 않는다.
알파벳 이외의 문자들은 무시한다.

ex)
found7, time; study; Yduts; emit, 7Dunof => YES

A.
문제풀이 케이스

1. 알파벳을 모두 대문자로 바꾼다. 알파벳이 아닌 것들은 지운다. 반대로 출력한 비교군을 준비하여 원래 문자열과 일치하는지 확인한다.

- String toUpperCase()
- String replaceAll​(String regex, String replacement)

~~~
public String Solution(String s) {
   String answer = "NO";
   s = s.toUpperCase().replaceAll("[^A-Z]", "");
   tmp = StringBuilder(s).reverse().toString();
   if (s.equals(tmp)) answer = "YES";

   return answer;
}
~~~
