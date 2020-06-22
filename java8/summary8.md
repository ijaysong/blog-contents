# 자바 내용 정리 8

## `문자열의 특징`
#### `문자열은 불편 오브젝트`
String 클래스는 불변 클래스이다.  
작성한 인스턴스의 내용을 이후에 변경하는 것이 불가능하다.  
변경할 필요가 있을 때는 원래 인스턴스와 별도로 새로운 인스턴스를 작성할 때이다.  
예를 들어, 소문자를 대문자로 바꿀 때 toUpperCase()메소드를 사용하면 원래 문자열의 내용을 바꾸는 것이 아니라,모든 것을 대문자로 한 새로운 문자열을 작성해서 반환한다. 
-> 내용이 변경되지 않으므로 다른 메소드나 스레드에 안심하고 인스턴스를 보낼 수 있다.

~~~
String s1 = "Hello";
String s2 = s1.toUpperCase(); // toUpperCase() 메소드는 영어를 대문자로 변환한다.
~~~

#### `문자열 리터럴은 여러번 사용된다`
모든 문자열이 다 같은 것은 아니다.  
하나는 `리터럴(literal)`이고, 다른 하나는 `인스턴스`이다.  

~~~
String s1 = "Hello"; // 리터럴
String s2 = new String("Hello"); // 인스턴스
~~~

new로 작성한 문자열은 메모리의 힙 영역에 놓여진다.  
반면에, 대입연산자로 작성한 문자열은 `문자열 리터럴`이라 부르고, 힙 영역에 놓여진 후, 참조(메모리 상 위치)가 `문자열 리터럴풀`에 등록된다.  
다음에 동일한 문자열 리터럴이 작성될 때, 먼저 문자열 리터럴풀에서 참조를 찾아내 반환한다. 반복해서 사용하며, 신규 인스턴스를 작성하지 않아도 된다.    
다음의 s1과 s2는 동일한 참조를 가진다.

~~~
String s1 = "Hello";
String s2 = "Hello";
~~~

new를 사용해 작성하면 리터럴풀은 사용할 수 없다.  
new로 작성한 문자열 오브젝트는 매회 신규 작성된다.
다음의 s3와 s4는 각각 다른 참조를 가진다.

~~~
String s3 = new String("Hello");
String s4 = new String("Hello");
~~~

## `String 클래스의 주요 API`
`컨스트럭터`
|메소드                           |기능                          |
|-------------------------------|-----------------------------|
|String (String str)            | 문자열로부터 작성               |
|String (byte[] bytes, charset) | byte 배열과 문자열 셋으로부터 작성 |
|String (byte[] bytes)          | byte 배열로부터 작성            |
|String (char[] values)         | char 배열로부터 작성            |

`문자의 추출, 길이 취득`
|메소드                |기능                                        |
|--------------------|-------------------------------------------|
|char charAt(i)      | i번째 문자를 반환                             |
|int codePointAt(i)  | i번째 문자의 유니코드를 반환                     |
|int indexOf(str, i) | i번째 위치로부터 str을 찾아, 출현위치의 인덱스를 반환 |
|int length()        | 문자열의 길이를 반환                           |
|boolean isEmpty()   | 문자열의 길이가 0 (null이 아닌) 경우, true를 반환  |

`문자열 비교`
|메소드                         |기능                                        |
|-----------------------------|-------------------------------------------|
|int compareTo(str)           | 사전순으로 str을 비교하고, 음수, 0, 정수의 값을 반환 |
|int compareToIgnoreCase(str) | 위와 같음. 다만, 대문자와 소문자를 구별하지 않음      |
|boolean contains(str)        | str이 문자열에 포함되어 있다면 true를 반환         |

`치환, 부분 문자열`
|메소드                     |기능                                    |
|-------------------------|---------------------------------------|
|String replace(old, new) | 문자열 안에서 모든 old를 new로 치환          |
|String substring(i)      | i번째부터 마지막까지 문자열을 추출             |
|String substring(i, j)   | i번째부터 j-1번째까지 문자열을 추출 (j번째 포함) |

`변환`
|메소드                     |기능                                  |
|-------------------------|-------------------------------------|
|byte[] getBytes()        | byte 배열로 변환                       |
|byte[] getBytes(charset) | 문자셋을 지정하고, byte 배열로 변환         |
|char[] toCharArray()     | 문자 배열로 하여 반환                     |
|String toLowerCase()     | 대문자를 소분자로 변환한 문자열을 반환         |
|String toUpperCase()     | 소문자를 대문자로 변환한 문자열을 반환         | 
|String trim()            | 문자 앞뒤로 존재하는 공백을 삭제한 문자열을 반환 |


`static 메소드`
|메소드                       |기능                                    |
|---------------------------|---------------------------------------|
|String valueOf(~)          | 다른 타입의 문자열로 변환하여 반환             |
|String join(delim, elm...) | 배열등의 요소를 구분 문자로 결합한 문자열을 반환  |
|String join(delim, list)   | 위의 내용과 같지만, 리스트 요소를 사용함        |
|String format(fmt, elm...) | 포맷 문자열 fmt로 요소를 편집한 문자열을 반환    |

`정규표현을 이용한 메소드`
|메소드                          |기능                                       |
|------------------------------|------------------------------------------|
|boolean matches(reg)          | reg에 매치할 때 treu를 반환                   |
|String replaceAll(reg, new)   | reg에 매치하는 모든 부분을 new로 변환            |
|String replaceFirst(reg, new) | reg에 매치한 첫부분만 new로 변환                |
|String[] split(reg)           | reg에 매치하는 문자열을 기준으로 분할하여 배열로 반환 |

`스트림 생성`
|메소드                   |기능                                                |
|-----------------------|---------------------------------------------------|
|IntStream chars()      | 문자열로부터 IntStream을 반환 (surrogate pair 사용 안함) |
|IntStream codePoints() | 문자열로부터 IntStream을 반환 (surrogate pair 사용 함)   |

## `String 클래스의 메소드 사용법`
#### `byte배열로부터 String 작성`
**byte[] Files.readAllBytes(Path p);**
패스가 가리키는 파일 내용을 전부 읽어들여 byte 배열로 반환한다.

~~~
public static void main(String[] args) {
    // 파일을 byte배열로서 읽어들임
    byte[] bytes = Files.readAllBytes(Paths.get("sample.html"));

    // byte 배열로부터 문자열을 작성해 표시
    String str = new String(bytes, "UTF-8");
    System.out.println(str);
}
~~~
OUTPUT : \<!DOCTYPE html>  
\<html>  
\<title>샘플\</title>  
\<body>
\<h1>My First Hompate\</h1>  
\<p>안녕하세요!\</p>
\</body>
\</html>

#### `배열/리스트를 결합해 문자열로 한다`
**String String.join(str, String[]);**
join은 String 클래스의 static 메소드이다.  
String[] 타입이나 List<String> 타입의 값에 대해서, 모든 요소를 지정한 문자(str)로 연결한 문자열을 반환한다.  

~~~
public static void main(String[] args) {
    String[] array = { "2020", "07", "15" };
    System.out.println(String.join("-", array));
    System.out.println(String.join("\n", array));
}
~~~
OUTPUT : 2020-07-15  
2020  
07  
15  

#### `문자열 안의 특정 문자를 치환한다`
**String String.replace(str1, str2);**
문자열 안의 특정 문자(str1)를 다른 문자(str2)로 치환한다. 
~~~
public static void main(String[] args) {
    String str = "12/25 크리스마스\n" +
                 "02/14 발렌타인데이\n" + 
                 "03/14 화이트데이";
    System.out.println(str.replace("/", "-")); 
}
~~~
OUTPUT : 12-25 크리스마스  
02-14 발렌타인데이  
03-14 화이트데이  

#### `문자열을 분할 문자로 나누어 배열로 한다`
**String[] String.split(str)**
split 메소드는 분할 문자(str)를 지정하여, 해당 문자를 기준으로 문자열을 분할하여 배열로 반환한다. 

~~~
public static void main(String[] args) {
    String data = "월, 화, 수, 목, 금";
    String[] dayOfWeek = data.split(",");
    Arrays.stream(dayOfWeek)
            .forEach(System.out::pringln);
}
~~~
OUTPUT: 월  
화  
수  
목  
금  

#### `대소문자를 구별하지 않고 비교한다`
**Comparator<T> str1.compareTo(str2)**
**Comparator<T> str1.compareToIgnoreCase(str2)**
정렬을 위해서 비교를 이용한다. 
결과 값으로 음수, 0, 양수를 반환한다.
sort메소드의 인수는 Compartor 타입이다.
compareToIgnoreCase메소드는 대문자와 소문자를 구별하지 않고 비교하여 리스트를 사전 순으로 정렬한다.

****
~~~
public static void main(String[] args) {
    List<String> list = Arrays.asList("Bb", "ac", "ba");
    list.sort((s1, s2) -> s1.compareToIgnoreCase(s2)); // 비교
    System.out.println(list); // 출력
}
~~~
OUTPUT : [ac, ba, Bb]


## `String 클래스`
new를 사용해, 인스턴스를 다른 문자열이나 byte 배열로부터 작성할 수 있다.  
byte 배열로부터 작성한 경우, 될수 있는 만큼 문자 셋을 지정해서 작성한다.  
join 메소드를 사용하면, 리스트나 배열의 요소를 결합해서 하나의 문자열로 할 수 있다.  
문자열 안에 특정 부분을 치환하던가, 특정 위치에서 분할 하는것이 가능하다.  
치환과 분할에는 정규표현을 사용하는 것이 가능하다.  
StringBuilder는 +로 문자열을 연결하는 것과 같다.   
+=를 사용해 반복해서 문자열을 연결하는 경우, StringBuilder를 사용한다.  
Stringbuilder는 초기용량을 지정해서 작성하는 것이 낫다.  

## `정규표현`
정규표현(Regular Expression)은, 문자열 안에 포함되어 있는 특정 패턴을 문자열로 표현하는 방법이다. 

|정규표현 패턴        | 의미                                  |
|------------------|-------------------------------------|
|.                 | 임의의 1문자                           |
|^a                | 선두 문자가 a                          |
|a$                | 마지막 문자가 a                         |
|a?                | 1개 이하의 a                           |
|a+                | 1개 이상의 a                           |
|a*                | 0개 이상의 a                           |
|a?? a*? a+?       | ?를 붙이면 부분 일치가 된다                |
|[abc] [a-z]       | abc 중 어떤 것  a부터 z 중 어떤 것        |
|[^abc]            | abc 어떤 것도 아니다                    |
|\d \s \w          | 숫자  공백문자(공백, 탭)  단어구성문자       |
|\D \S \W          | 위의 내용을 부정                        |
|x{n} x{n,} x{n,m} | n개의 X  n개 이상의 X  n개부터 m개까지의 X |
|(X)               | 정규표현을 하나로 묶음                    |
|X\|Y              | X 혹은 Y                             |


## `포함과 불포함`
* 정규표현 reg를 포함하는 문자열 : ^(?=.*reg).*$ 
* 정규표현 reg를 포함하지 않는 문자열 : ^(?!.*reg).*$
* 복수 지정이 가능 (포함) : ^(?=.*reg1)(?=.*reg2).*$
* 복수 지정이 가능 (불포함) :^(?!.*reg3)(?!.reg4).*$
* 포함, 불포함은 섞어서 사용 가능 : ^(?=reg1)(?!.*reg3).*$
* .*은 필요에 따라서 변경한다 : ^(?=.reg).{1,6}$  
* ^(?=.*reg)\d+$


## `정규표현을 사용하는 메소드`
* String 클래스의 split 메소드 : 분할 위치를 결졍하는 문자열을 지정한다. 
* String 클래스의 replaceAll 메소드 : 치환할 문자열을 지정한다.
* String 클래스의 matches 메소드 : 정규표현에 매치하는 문자열인지 조사한다.
* String 클래스의 useDelimiter 메소드 : 분할 기준이 되는 문자를 변경한다.  