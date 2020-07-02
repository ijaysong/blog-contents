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

## `문자열 연결과 StringBuilder 클래스`
StringBuilder 클래스는 문자열을 만들기 위해 사용한다.  
append 메소드를 사용해 문자열 혹은 숫자를 연결한다.  
초기 용량을 지정하여 데이터 용량이 초과하면 자동적으로 용량이 2배 늘어나기 때문에 부하가 커진다.  
그러므로 처음부터 필요한 양을 지정할 것.  
+로 연결하는 것과 같음.  
sb.append("abc").append("def").append() 처럼 메소드 체인으로 기술할 수 있다.

~~~
public static void main(String[] args) {
    StringBuilder sb = new StringBuilder(500);
    sb.append(2020); // 숫자를 추가
    sb.append("년"); // 문자열을 추가
    sb.append(7);
    sb.append("월");
    String str = sb.toString();
    System.out.println(str);
}
~~~
OUTPUT:2020년7월  

#### `컨스트럭터`
|컨스트럭터                         | 내용                                        |
|--------------------------------|--------------------------------------------|
|StringBuilder()                 | 초기용량 16문자로 작성한다                       |
|StringBuilder(int capacity)     | 초기용량을 지정해 작성한다                        |
|StringBuilder(String s)         | s를 초기값으로 하는 StringBuilder를 작성한다      |
|StringBuilder(CharSequence seq) | 다른 StringBuilder 등과 동일한 내용의 것을 작성한다 |

#### `주요 메소드`
|컨스트럭터                          | 내용                                         |
|---------------------------------|---------------------------------------------|
|StringBuilder appned(a)          | 데이터를 추가한다. 오브젝트는 문자열의 변수로서 추가한다. |
|StringBuilder insert(p, a)       | 위치 p에 a를 삽입한다. (p는 0부터 센다.)           |
|StringBuilder delete(p1, p2)     | 위치 p1에서부터 p2-1 까지의 문자를 삭제한다.         |
|StringBuilder replace(p1, p2, a) | 위치 p1에서부터 p2-1 까지의 범위를 a로 변환한다.      |
|StringBuilder substring(p1, p2)  | 위치 p1에서부터 p2-1 까지의 부분 문자를 반환한다.     |
|StringBuilder reverse()          | 순서를 역순으로한 문자열을 반환한다.                 |
|StringBuilder indexOf(a)         | a가 처음부터 출현하는 문자위치를 반환한다.            |
|StringBuilder length()           | StringBuilder내의 문지열 전체의 길이를 반환한다.     |
|StringBuilder toString()         | 내용을 String으로 하여 반환한다.                   |


## `정규표현`
정규표현(Regular Expression)은, 문자열 안에 포함되어 있는 특정 패턴을 문자열로 표현하는 방법이다.

#### `문자와 예약문자`
정규표현 안에서는 일반 문자를 그대로 쓴다.  
이스케이프(Escape) 문자를 사용하는 것이 가능하다. 다음과 같이 사용한다.  

|정규표현 패턴  | 의미                      |
|-----------|---------------------------|
|\\         | \기호 자체는 \\라고 쓴다.      |
|\t         | 예약문자 ('\u0009')         |
|\n         | 개행문자 ('\u000A')         |
|\r         | 탈출문자 ('\u000D')         |
|\f         | 새로운 페이지 문자 ('\u000C') |

정규표현식을 위해서 예약된 문자(예약 문자)가 있다.  
예약 문자는 다음과 같다.  
예약 문자를 다음과 같이 사용할 때는 왼쪽에 \를 붙인다.  
예를 들어, $는 \$, *는 \*라고 쓴다.

~~~
[ ] ( ) ^ $ . + * ? |
~~~

#### `임의의 1문자`
임의의 1문자를 나타내는 것은 `.(도트)`로 몇개 연속해서 지정하는 것이 가능하다.  

|정규표현 | 의미        | 예시                         |
|-------|-----------|-----------------------------|
|.      | 임의의 1문자 | ab.c 는 ab c 나 abbc에 매치된다 |

**ab.c**
abc `ab c` ac % `abbc` ABC A_ 12.133 # A aAA aAAAA dogdog aabc

#### `선두, 선미의 문자가 매치하는지`
* 선두 문자 지정 : ^
* 선미 문자 지정 : $

정규표현 | 의미     | 예시               |
|------|---------|-------------------|
|^     | 행의 선두 | ^abc 행의 선두는 abc |
|$     | 행의 말미 | abc$ 행의 말미는 abc |

**^abc**
`abc` ab c abbc ac % abbbc ABC A_ 12.133 # A aAA aAAAA dogdog aabc

**abc$**
abc ab c abbc ac % abbbc ABC A_ 12.133 # A aAA aAAAA dogdog a`abc`

#### `문자의 반복`
`+` 나 `*`는 문자의 연속을 표현한다.  
어떤 문자를 X로 하면, X*는 0개 이상의 X, X+는 1개이상의 X를 표시한다.  
X?는 0개 혹은 1개의 X를 표시한다. 

정규표현 | 의미     | 예시               |
|------|---------|-------------------|
|X?    | 0 혹은 1개의 X | ab?c  ac 혹은 a`b`c |
|X*    | 0개 이상의 X   | ab*c  ac, a`b`c, a`bb`c 등 |
|X+    | 1개 이상의 X   | ab+c  a`b`c, a`bb`c. a`bbb`c 등 |

**ab?c** : a와 c 사이에 0 ~ 1개의 b가 끼어있는 문자열
`abc` ab c abbc ac % abbbc ABC A_ 12.133 # A aAA aAAAA dogdog a`abc`

**ab*c** : a와 c 사이에 0개 이상의 b가 끼어있는 문자열
`abc` ab c `abbc` `ac` % `abbbc` ABC A_ 12.133 # A aAA aAAAA dogdog a`abc`

**ab+c** : a와 c 사이에 1개 이상의 b가 끼어있는 문자열
`abc` ab c `abbc` ac % `abbbc` ABC A_ 12.133 # A aAA aAAAA dogdog a`abc`

**a.*c** : a와 c 사이의 임의의 문자열
`*`는 될 수 있는 한 넓은 범위에서 매치하는 것을 찾는 최장 일치를 의미한다
`abc ab c abbc ac % abbbc ABC A_ 12.133 # A aAA aAAAA dogdog a abc`

**a.*?c** : a와 c 사이에 최단 일치하는 문자열
`?`는 최단 일치를 의미한다. a 다음에 처음으로 출현하는 c의 위치까지.
`abc` `ab` `c` `abbc` `ac` % `abbbc` ABC A_ 12.133 # A `aAA aAAAA dogdog a abc`

#### `문자 클래스`
`[]`로 감싼 문자를 `문자 클래스`라고 한다.  
[]에는 복수의 문자를 지정할 수 있고, 그 안에서 어떤 것이든 매치한다라는 의미이다.  
[]안에서 `^`는 부정의 의미이다.
`-`를 사용해서 범위를 나타낼 수 있다.

|정규 표현 | 의미                     | 표시                    |
|--------|------------------------|------------------------|
|[...]   | []안의 어떤 문자          | a 혹은 b 혹은 c           |
|[^...]  | []안에 지정된 문자 이외의 것 | [a 혹은 b 혹은 c] 이외의 것 |
|[.-.]   | 범위를 지정한다            | a로부터 z까지 <br> a로부터 z까지와 A로부터 Z까지 |

**[abc]+** : a, b, c로 구성된 문자열
`abc` `ab` `c` `abbc` `ac` % `abbbc` ABC A_ 12.133 # A `a`AA `a`AAAA dogdog `aabc`

**[0-9]+** : 숫자로 구성된 문자열
abc ab c abbc ac % abbbc ABC A_ `12`.`133` # A aAA aAAAA dogdog aabc

**[^a-zA-Z]+** : 영어 이외의 문자열
abc` `ab` `c` `abbc` `ac` % `abbbc` `ABC` `A`_ 12.133 # `A` `aAA` `aAAAA` `dogdog` `aabc

#### `정의된 문자 클래스`
숫자이나 공백 등 정규표현 안에 있는 문자를 간단하게 지정할 수 있는 단축형이다.  
대문자로 하면 ~이외의 반대 의미가 된다.  
Java프로그램 안에서 작성시엔 \d를 \\d처럼 작성한다.(`\`는 이스케이프 문자)
|정규표현 | 의미                                       |
|-------|-------------------------------------------|
|\d     |숫자                                        |
|\D     |숫자가 아닌 문자                               |
|\s     |공백문자(\t \n \r \f를 포함)                   |
|\S     |공백문자 이외 ([^\s]와 동일한 의미)               |
|\w     |영단어를 구성하는 문자 ([a-zA-Z0-9_]와 동일한 의미) |
|\W     |영단어를 구성하는 문자 이외 ([^\w]와 동일한 의미)    |

**\d+** : 숫자만으로 구성된 문자열
abc ab c abbc ac % abbbc ABC A_ `12`.`133` # A aAA aAAAA dogdog aabc

**\w+** : 영단어를 구성하는 문자열로 구성된 문자열 
`abc` `ab` `c` `abbc` `ac` % `abbbc` `ABC` `A_` `12`.`133` # `A` `aAA` `aAAAA` `dogdog` `aabc`

**c\s+** : 문자 C 다음에 오는 1개 이상의 공백문자
ab`c `ab `c `abbc a`c `% abbbc ABC A_ 12.133 # A aAA aAAAA dogdog aabc

#### `지정된 범위에서 반복`
문자의 개수를 지정하고 싶은 경우, *나 + 가 아닌, {} 형식으로 지정한다.
이 형식에서는 x{2}처럼 {}에 문자의 개수를 지정한다.
혹은, {n,}은 n 이상, {n,m}에서는 n부터 m까지의 반복을 의미한다.

|정규표현 | 의미                  | 예시                        |
|-------|----------------------|---------------------------|
|X{n}   |n개의 X                | A{2} : AA                 |
|X{n,}  |n개 이상의 X            | A{2,} : AA, AAA, AAAA 등등 |
|X{n,m} |n개 이상 이며 m개 이하의 X | A{2, 3} : AA 혹은 AAA      |

**A{1,3}** : A가 1개부터 3개까지의 패턴
abc ab c abbc ac % abbbc `A`BC `A`_ 12.133 # `A` a`AA` a`AAA``A` dogdog aabc

**d{2}\.\d** : 정수 부분이 2자리의 소수
abc ab c abbc ac % abbbc ABC A_ `12.133` # A aAA aAAAA dogdog aabc

#### `그룹화와 선택`
`()`는 정규표현을 한데 모아 그룹핑 한다. 수식에서의 ()와 같다.
`|`는 혹은 이라는 의미의 논리기호이다.

|정규표현 | 의미                       | 예시                                 |
|-------|---------------------------|-------------------------------------|
|(X)    | 정규표현을 하나로 묶는다.       | (dog){2} : "dogdog"                 |
|X|Y    | X `혹은` Y. `|`로 연결한다.   | (dog){2} | a{2} : "dogdog" 혹은 "aa" |

## `포함과 불포함`
패턴 매치는 일부분이 일치하는지 확인하는 것이 아니라, 일치하는 것이 있는지 없는지 조사하는 것이다.
Lookahead(전방탐색)이라고 하는데 이는 독특한 기법을 사용한다.
임의의 정규표현 X의 오른쪽에 `()`를 적고, `?=`는 정규표현 reg가 나타내는 문자열을 X의 오른쪽에 포함,  
`?!`는 X의 오른쪽에 포함하지 않는다라는 의미이다.

|정규표현     | 의미                     | 예시 |
|----------|-------------------------|-----|
|X(?=reg)  | X의 오른쪽에 ~를 포함        | mk(?=abc) : `mk`abc mkdefg |
|X(?!=reg) | X의 오른쪽에 ~를 포함하지 않음 | mk(?!abc) : mkabc `mk`defg |

**windows(?=10)** : windows의 오른쪽에 10을 포함하는 windows
windows3.1 windows7 `windows`10

**windows(?!10)** : windows의 오른쪽에 10을 포함하지 않는 windows
`windows`3.1 `windows`7 windows10

#### `~를 포함한다`
windowsxx10xx처럼 windows의 오른쪽, 임의의 위치에 10가 있는 것을 정규표현식에 매치하도록 하려면,  
10이 아닌, `.*10`이라고 한다.
`.*`은 0개 이상의 임의의 문자를 나타내는 것으로, 0개 이상의 임의의 문자 뒤에 10이 나타나도록 표현한 것이다.

**windows(?=.\*10)** : windows의 오른쪽 임의의 위치에 10을 포함한다.
`windows`xx10xx `windows`10

일반 문자열의 선두의 오른편에 특정 문자(10)가 있는 문자열인지 확인할 때 사용될 수 있다. -> ^(?=.\*10).\*

**^(?=.\*10).\*** : 10을 포함하는 문자열
`xxx10xxx`

`^(?=.\*10)\d+`라던지 `^(?=.*10)[a-z]`처럼 필요에 따라서 변경할 수 있다.

**^(?=.\*10).{1,6}** : 10을 포함하는 6문자까지의 문자열
`xxx10x`xx

정규표현식의 말미에 `$`를 붙이면 행이 끝남, 혹은 문자가 끝남을 의미한다.
문자열 전체가 매치하는 것을 찾고 싶은 경우, 항상 정규표현식의 말미에 $를 붙인다.

**^(?=.\*10).{1,6}$** : 10을 포함하는 6자리의 문자열
`xxx10x`

포함에 대한 조건을 추가하고 싶은 경우, `(?=.*~)`를 추가하면 된다. --> 복수지정 가능
조건을 나열하는 것은 자유이며, 어떤 순서로 나열해도 같은 결과가 추출된다.

**^(?=.\*10)(?=.\*A).{1,6}$** : 문자열의 오른쪽, 임의의 위치에 10과 A를 포함하는 6문자까지의 문자열
`x10xAx`


#### `~를 포함하지 않는다`
`~를 포함한다`는 표현인 `?=`를 `?!`로 바꾼 것 뿐이며, `(?!.*B)`처럼 표현하면 된다.

**^(?!.\*B).\*$** : B를 포함하지 않는다
`x10xAx`

포함하지 않는다는 조건도 몇개라도 지정 가능하다. --> 복수 지정 가능
예를 들어 C를 포함하지 않는다 라는 조건을 추가한다면, `^(?!.\*B)(?!.\*C).*`라고 표현할 수 있다.

포함하는 것과 포함하지 않는 조건을 동시에 지정할 수도 있다.
예를 들어, A를 포함하고, B를 포함하지 않는, 6문자까지의 문자열의 경우, 다음과 같이 지정할 수 있다.

***^(?=.\*A)(?!.\*B).{1,6}$** : A를 포함하고, B를 포함하지 않는, 6문자까지의 문자열
`x10xAx`

## `정규표현식의 이용`

#### `문자열의 교환과 분할`
String 클래스에는 정규표현식을 써서 문자열을 교환하거나 분할하는 메소드가 있다.  
replaceAll, split, matches의 각 메소드에서 정규표현을 활용할 수 있다.

**replaceAll 메소드**
~~~
public class ReplaceAllExample {
    public void main(String[] args) throws IOException {
        String str = "<title>타이틀</title>";

        // <와 >, 그 사이의 임의의 문자열을 공백문자("")로 교환한다
        System.out.println(str.replaceAll("<.+?>)", "");
    }
}
~~~
OUTPUT : 타이틀

**split 메소드**
~~~
public class SplitExample2 {
    public static void main(String[] args) {
        String dt = "100, 홍길동, 60.5";

        // 컴마 전후에 존재하는 0개 이상의 공백문자
        String[] dts = dt.split("\\s*,\\s*");
        Arrays.stream(dts).forEach(System.out::println);
    }
}
~~~
OUTPUT : 100  
홍길동  
60.5

#### `문자열의 검사`
matches 메소드는 인수의 정규표현에 매치하는 경우, true를 반환한다.
문자열이 올바른 패턴인지 체크하는 것이 가능하다.  

* (?=.*[A-Z])) : 대문자를 포함
* (?!.*\\W) : 단어구성문자 이외를 포함하지 않음
* .{5,} : 길이가 5문자 이상

**matches 메소드**
~~~
public class MatchesExample {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("Jack110", "suzu-10", "Ken3", "tom10");

        for(String s : list) {
            // 대문자를 포함 단어 구성 문자 이외의 문자를 포함하지 않는 5문자 이상의 문자열
            if(s.matches("^(?=.*[A-Z])(?!.*\\W).{5,}$")) {
                System.out.println(s);
            } 
        }

        // 스트림 식을 사용하여 다음과 같이 표현할 수 있다
        list.stream()
            .filter(s -> s.matches("^(?=.*[A-Z])(?!.*\\W).{5,}$")) // 선택한다
            .forEach(System.out::println);
    }
}
~~~
OUTPUT : Jack110  
Jack110 

#### `Scanner 클래스의 단락 구분`



## `정규표현을 사용하는 메소드`
* String 클래스의 split 메소드 : 분할 위치를 결졍하는 문자열을 지정한다. 
* String 클래스의 replaceAll 메소드 : 치환할 문자열을 지정한다.
* String 클래스의 matches 메소드 : 정규표현에 매치하는 문자열인지 조사한다.
* String 클래스의 useDelimiter 메소드 : 분할 기준이 되는 문자를 변경한다.  