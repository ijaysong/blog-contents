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

