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

### 수량자
어떠한 패턴이 얼마나 등장하는지 그 숫자를 나타내는 것을 수량자라고 한다.
수량자와 관련된 정규표현식 문자열로 *, +, ?가 있다.

1. * 수량자 (0 개 ~ 여러 개)

ex 1)
*는 * 앞에 지정된 패턴이 0 ~ 여러개 존재할 수 있다는 것을 의미한다.
* 앞의 패턴이 있을 수도 있고, 없을 수도 있다.
=> 0개 ~ 여러 개

~~~
[ Source ]
aabc abc bc

[ Regular Expression ]
a*b

[ First match ]
`aab`c abc bc

[ All matches ]
`aab`c `ab`c `b`c
~~~

ex 2)
모든 텍스트(.)가 여러 개(*) 있을 수 있다는 뜻이다.

~~~
[ Source ]
-@-***--"*"--***-@-

[ Regular Expression ]
.*

[ First match ]
`-@-***--"*"--***-@-`

[ All matches ]
`-@-***--"*"--***-@-`
~~~

ex 3)
* 앞의 A가 있을 수도 있고, 없을 수도 있지만 끝에 -가 꼭 있어야 한다.

~~~
[ Source ]
-@-***--"*"--***-@-

[ Regular Expression ]
-A*-

[ First match ]
-@-***`--`"*"--***-@-

[ All matches ]
-@-***`--`"*"`--`***-@-
~~~

ex 4)
대괄호 내부에 선택 후보군을 작성할 수 있다.
문자에 - 혹은 @가 여러개(*) 존재할 수 있다.

~~~
[ Source ]
-@-***--"*"--***-@-

[ Regular Expression ]
[-@]*

[ First match ]
`-@-`***--"*"--***-@-

[ All matches ]
`-@-`***`--`"*"`--`***`-@-`
~~~

2. + 수량자 (1 개 ~ 여러 개)

ex 1)
+ 앞에 지정된 패턴이 꼭 1개 이상은 있어야 한다는 뜻이다.
b 앞에 a가 한개 이상 있어야 매칭된다.
=> 한개 ~ 여러 개

~~~
[ Source ]
aabc abc bc

[ Regular Expression ]
a+b

[ First match ]
`aab`c abc bc

[ All matches ]
`aab`c `ab`c bc
~~~

ex 2)
* 앞에 이스케이프 문자가 있다. *를 문자 그대로 인식하겠다는 뜻이다.
*이 한개 ~ 여러개 있는 문자열을 찾아서 표시한다.

~~~
[ Source ]
-@@@-* **--"*"--* **-@@@-

[ Regular Expression ]
\*+

[ First match ]
-@@@-`*` **--"*"--* **-@@@-

[ All matches ]
-@@@-`*` `**`--"`*`"--`*` `**`-@@@-
~~~

ex 3)
문자 앞 뒤로 -가 있어야 하고, @가 한 개 ~ 여러 개 있는 문자열에 매칭된다.

~~~
[ Source ]
-@@@- * ** -- "*" -- * ** -@@@-

[ Regular Expression ]
-@+-

[ First match ]
`-@@@-` * ** -- "*" -- * ** -@@@-

[ All matches ]
`-@@@-` * ** -- "*" -- * ** `-@@@-`
~~~

ex 4)
대괄호 안에서 캐럿은 부정(not)을 의미한다.
공백이 아닌 것이 하나 이상 있을 때 선택된다.

~~~
[ Source ]
-@@@- * ** -- "*" -- * ** -@@@-

[ Regular Expression ]
[^ ]+

[ First match ]
`-@@@-` * ** -- "*" -- * ** -@@@-

[ All matches ]
`-@@@-` `*` `**` `--` `"*"` `--` `*` `**` `-@@@-`
~~~

3. ? 수량자 (0 개 ~ 1 개)

ex 1)
? 앞에 지정된 패턴이 없거나 한 개가 있어야 한다는 뜻이다.
=> 0개 ~ 1개

~~~
[ Source ]
aabc abc bc

[ Regular Expression ]
a?b

[ First match ]
a`ab`c abc bc

[ All matches ]
a`ab`c `ab`c `b`c
~~~

ex 2)
-XX는 무조건 존재해야 한다.
X의 갯수가 2~4개 인 것을 찾는다.

~~~
[ Source ]
--XX-@-XX-@@-XX-@@@-XX-@@@@-XX-@@-@@-

[ Regular Expression ]
-X?XX?X

[ First match ]
-`-XX`-@-XX-@@-XX-@@@-XX-@@@@-XX-@@-@@-

[ All matches ]
-`-XX`-@`-XX`-@@`-XX`-@@@`-XX`-@@@@`-XX`-@@-@@-
~~~

ex 3)
앞뒤로 -는 무조건 있어야 한다.
@의 갯수는 0 ~ 3개 까지 있을 수 있다.

~~~
[ Source ]
--XX-@-XX-@@-XX-@@@-XX-@@@@-XX-@@-@@-

[ Regular Expression ]
-@?@?@?-

[ First match ]
`--`XX-@-XX-@@-XX-@@@-XX-@@@@-XX-@@-@@-

[ All matches ]
--XX`-@-`XX`-@@-`XX`-@@@-`XX-@@@@-XX`-@@-`@@-
~~~

4. 정확한 수량을 지정할 수 있는 수량자

{} (브레이슬릿) 내부에 수량을 지정할 수 있다.

ex 1)
모든 문자열 가운데 5개를 선택하라는 뜻이다.

~~~
[ Source ]
One ring to bring them all and in the darkness bind them

[ Regular Expression ]
.{5}

[ First match ]
`One r`ing to bring them all and in the darkness bind them

[ All matches ]
`One ring to bring them all and in the darkness bind the`m
~~~

ex 2)
e나 s, l 중에 한 글자가 앞에 오고, 그것이 하나 이상 3 이하 매칭이 됐을 때 해당된다는 뜻이다.

~~~
[ Source ]
One ring to bring them all and in the darkness bind them

[ Regular Expression ]
[els]{1,3}

[ First match ]
On`e` ring to bring them all and in the darkness bind them

[ All matches ]
On`e` ring to bring th`e`m a`ll` and in th`e` darkne`ss` bind th`e`m
~~~

ex 3)
알파벳 소문자 가운데 3 이상인 문자열이 있다면 매칭된다.

~~~
[ Source ]
One ring to bring them all and in the darkness bind them

[ Regular Expression ]
[a-z]{3,}

[ First match ]
One `ring` to bring them all and in the darkness bind them

[ All matches ]
One `ring` to `bring` `them` `all` `and` in `the` `darkness` `bind` `them`
~~~

5. *, +, ? 수량자를 {}로 대체해서 표현

5-1. * 와 {0,}

*는 {0,} 과 일치한다.
0 개 ~ 여러 개를 의미한다.

ex 1)
앞 뒤로 A가 있고 B는 0개 이상 존재할 수 있다.

~~~
[ Source ]
AA ABA ABBA ABBBA

[ Regular Expression ]
AB*A

[ First match ]
`AA` ABA ABBA ABBBA

[ All matches ]
`AA` `ABA` `ABBA` `ABBBA`
~~~

ex 2)
*의 표현과 동일하다.

~~~
[ Source ]
AA ABA ABBA ABBBA

[ Regular Expression ]
AB{0,}A

[ First match ]
`AA` ABA ABBA ABBBA

[ All matches ]
`AA` `ABA` `ABBA` `ABBBA`
~~~

5-2. + 와 {1,}

+는 {1,} 과 일치한다.
1 개 ~ 여러 개를 의미한다.

ex 1)
앞 뒤로 A가 있고 B는 1개 이상 존재할 수 있다.

~~~
[ Source ]
AA ABA ABBA ABBBA

[ Regular Expression ]
AB+A

[ First match ]
AA `ABA` ABBA ABBBA

[ All matches ]
AA `ABA` `ABBA` `ABBBA`
~~~

ex 2)
+의 표현과 동일하다.

~~~
[ Source ]
AA ABA ABBA ABBBA

[ Regular Expression ]
AB{1,}A

[ First match ]
AA `ABA` ABBA ABBBA

[ All matches ]
AA `ABA` `ABBA` `ABBBA`
~~~

