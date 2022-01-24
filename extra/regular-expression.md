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

