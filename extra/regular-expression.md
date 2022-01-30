# 정규 표현식
생활코딩 `정규표현식` 관련 강의를 듣고..

## 정규 표현식이란?
문자열을 처리하는 방법 중의 하나로 특정한 조건의 문자를 '검색'하거나 '치환'하는 과정을 매우 간편하게 처리 할 수 있도록 하는 수단이다.

## 정규 표현식 패턴들
### 기본 패턴

찾고자 하는 텍스트를 적어준다.

ex 1)
~~~
[ Source ]
Hello, world!

[ Regular Expression ]
Hello

[ First match ]
`Hello`, world!

[ All matches ]
`Hello`, world!
~~~

ex 2)
대소문자를 구분하므로 매치되는 것이 없다.
~~~
[ Source ]
Hello, world!

[ Regular Expression ]
hello

[ First match ]
Hello, world!

[ All matches ]
Hello, world!
~~~

ex 3)
공백이나 tab, new line이 포함된 경우도 엄격하게 구분한다.
그러므로 매치되는 것이 없다ㅠㅠ

~~~
[ Source ]
Hello, world!

[ Regular Expression ]
Hello,   world

[ First match ]
Hello, world!

[ All matches ]
Hello, world!
~~~

### 위치와 이스케이핑

1. 위치

문자 ^ (캐럿)안 캐럿 뒤에 표현된 패턴이 소스 상에서 시작 위치에 있을 때 매치된다.
문자 $ (달러)는 달러 사인 앞에 표현된 패턴으로 끝나는 소스를 찾는다.

ex 1)
who로 시작하는 소스를 찾는다.

~~~
[ Source ]
who is who

[ Regular Expression ]
^who

[ First match ]
`who` is who

[ All matches ]
`who` is who
~~~

ex 2)
who로 끝나는 소스를 찾는다.

~~~
[ Source ]
who is who

[ Regular Expression ]
who$

[ First match ]
who is `who`

[ All matches ]
who is `who`
~~~

2. 이스케이핑

정규표현식에서 역할이 있는 문자열을 일반 문자열처럼 사용하고 싶을 때 \를 지정하여 escape 한다.

ex 1)
^과 $ 모두 정규 표현식에서 특수한 의미를 지니는 문자이므로 달러 사인으로 시작하는 문자열을 찾는 것에 실패했다. 

~~~
[ Source ]
$12$ \-\ $25$

[ Regular Expression ]
^$

[ First match ]
$12$ \-\ $25$

[ All matches ]
$12$ \-\ $25$
~~~

ex 2)
\ (백 슬래쉬)를 앞에 작성해주어 특수한 의미를 지닌 문자가 아닌, 문자열 그 자체로 역할을 할 수 있도록 해준다.

~~~
[ Source ]
$12$ \-\ $25$

[ Regular Expression ]
\$

[ First match ]
`$`12$ \-\ $25$

[ All matches ]
`$`12`$` \-\ `$`25`$`
~~~

ex 3)
$로 시작하는 문자열을 찾는다.

~~~
[ Source ]
$12$ \-\ $25$

[ Regular Expression ]
^\$

[ First match ]
`$`12$ \-\ $25$

[ All matches ]
`$`12$ \-\ `$`25$
~~~

ex 4)
$로 끝나는 문자열을 찾는다.

~~~
[ Source ]
$12$ \-\ $25$

[ Regular Expression ]
\$$

[ First match ]
$12$ \-\ $25`$`

[ All matches ]
$12`$` \-\ $25`$`
~~~

### 모든 문자 그룹
문자열 .은 모든 문자에 매칭된다.
일종의 와일드 카드 같은 역할을 한다.

ex 1)

~~~
[ Source ]
Regular expressions are powerful!!!

[ Regular Expression ]
.

[ First match ]
`R`egular expressions are powerful!!!

[ All matches ]
`Regular expressions are powerful!!!`
~~~

ex 2)
문자열 .을 6개 지정해주었다.
문자열 길이가 6개인 것이 매칭된다.
All matches의 경우, 길이 6개인 문자열 다섯 덩이가 선택된 것이다. 

~~~
[ Source ]
Regular expressions are powerful!!!

[ Regular Expression ]
......

[ First match ]
`Regula`r expressions are powerful!!!

[ All matches ]
`Regular expressions are powerf`ul!!!
~~~

ex 3)
모든 문자열 1개에 매칭되는 것을 선택한다.

~~~
[ Source ]
O.K.

[ Regular Expression ]
.

[ First match ]
`O`.K.

[ All matches ]
`O.K.`
~~~

ex 4)
이스케이프 문자를 사용하여, 문자열 .과 일치하는 것을 선택한다.
모든 문자열을 의미하는 정규표현식에서의 .의 역할에서 벗어난다.

~~~
[ Source ]
O.K.

[ Regular Expression ]
\.

[ First match ]
O`.`K.

[ All matches ]
O`.`K`.`
~~~

ex 5)
점과 점 사이에 문자열 1개가 포함된 패턴과 매칭하는 것을 선택한다.

~~~
[ Source ]
O.K.

[ Regular Expression ]
\..\.

[ First match ]
O`.K.`

[ All matches ]
O`.K.`
~~~

### 특정 문자와 범위

1. 특정 문자

[]은 대괄호, 영어로는 square brackets라고 부른다.
대괄호 사이에 적힌 문자열들 중에서 매칭되는 것을 찾는다.
여러 후보군을 둔 셈이다!

ex 1)
~~~
[ Source ]
How do you do?

[ Regular Expression ]
[oyu]

[ First match ]
H`o`w do you do?

[ All matches ]
H`o`w d`o` `you` d`o`?
~~~

ex 2)
문자열의 길이가 2개인 것을 찾는다.
단, 첫번째 문자는 d와 H 중에서 매칭되는 것이 있어야 하고
두번째 문자는 어떤 문자열이 와도 괜찮다.

~~~
[ Source ]
How do you do?

[ Regular Expression ]
[dH].

[ First match ]
`Ho`w do you do?

[ All matches ]
`Ho`w `do` you `do`?
~~~

ex 3)
문자열의 길이가 2개인 것을 찾는다.
단, 첫번째 문자는 o와 w, y 중에서 매칭되는 것이 있어야 하고
두번째 문자는 y와 o, w 중에서 매칭되어야 한다.

~~~
[ Source ]
How do you do?

[ Regular Expression ]
[owy][yow]

[ First match ]
H`ow` do you do?

[ All matches ]
H`ow` do `yo`u do?
~~~

2. 범위

문자 - (dash)는 범위를 의미한다.

ex 1)
C에서 K까지의 문자열 중 매칭되는 문자 1개를 표시한다.

~~~
[ Source ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ Regular Expression ]
[C-K]

[ First match ]
AB`C`DEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ All matches ]
AB`CDEFGHIJK`LMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789
~~~

ex 2)
정규 표현식 [C-K]와 [CDEFGHIJK] 일치한다.

~~~
[ Source ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ Regular Expression ]
[CDEFGHIJK]

[ First match ]
AB`C`DEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ All matches ]
AB`CDEFGHIJK`LMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789
~~~

ex 3)
대소문자를 구분하며 범위를 표현한다.

~~~
[ Source ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ Regular Expression ]
[a-d]

[ First match ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
`a`bcdefghjiklmnopqrstuvwxyz 0123456789

[ All matches ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
`abcd`efghjiklmnopqrstuvwxyz 0123456789
~~~

ex 4)
숫자를 구분하며 범위를 표현한다.

~~~
[ Source ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ Regular Expression ]
[2-6]

[ First match ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 01`2`3456789

[ All matches ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 01`23456`789
~~~

ex 5)
[] 내부에서 복수 개의 범위를 표현할 수 있다.

~~~
[ Source ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ Regular Expression ]
[C-Ka-d2-6]

[ First match ]
AB`C`DEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ All matches ]
AB`CDEFGHIJK`LMNOPQRSTUVWXYZ
`abcd`efghjiklmnopqrstuvwxyz 01`23456`789
~~~

3. 범위 부정

문자열 ^(캐럿)은 단독으로 사용될 때는 캐럿 바로 뒤의 패턴으로 시작하는 문자열을 찾는다는 의미를 가진다.
하지만, [] 대괄호 내부에서 사용할 때는 부정(not)의 의미를 가진다.

ex 1)
CDghi45에 해당하지 않는 문자열을 선택한다. 

~~~
[ Source ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ Regular Expression ]
[^CDghi45]

[ First match ]
`A`BCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ All matches ]
`AB`CD`EFGHIJKLMNOPQRSTUVWXYZ`
`abcdef`ghj`iklmnopqrstuvwxyz 0123`45`6789`
~~~

ex 2)
W ~ Z에 해당하지 않는 문자열을 선택한다. 

~~~
[ Source ]
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ Regular Expression ]
[^W-Z]

[ First match ]
`A`BCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghjiklmnopqrstuvwxyz 0123456789

[ All matches ]
`ABCDEFGHIJKLMNOPQRSTUV`WXYZ
`abcdefghjiklmnopqrstuvwxyz 0123456789`
~~~

### 서브 패턴

() 소괄호 안에 지정된 문자들 중 매칭되는 것을 선택한다.
소괄호 내부의 각 문자는 | 파이프로 구분한다.

ex 1)

~~~
[ Source ]
Monday Tuesday Friday

[ Regular Expression ]
(on|use|rida)

[ First match ]
M`on`day Tuesday Friday

[ All matches ]
M`on`day T`ues`day F`rida`y
~~~

ex 2)
공통된 부분을 서브 패턴으로 빼서 공통 문자열을 지정해 줄 수 있다.

~~~
[ Source ]
Monday Tuesday Friday

[ Regular Expression ]
(Mon|Tues|Fri)day

[ First match ]
`Monday` Tuesday Friday

[ All matches ]
`Monday` `Tuesday` `Friday`
~~~

ex 3)
문자 두개와 공통 문자열 ay 사이에 id 나 esd, nd 가 들어 갈 수 있다.

~~~
[ Source ]
Monday Tuesday Friday

[ Regular Expression ]
..(id|esd|nd)ay

[ First match ]
`Monday` Tuesday Friday

[ All matches ]
`Monday` `Tuesday` `Friday`
~~~

