# KNN 알고리즘

## 오렌지와 자몽 분류하기
자몽은 오렌지보다 붉고 크다.
* x축 : 크기 (작다-크다)
* y축 : 색상 (오렌지색 - 붉은색)

어떤 과일이 자몽인지 오렌지인지 어떻게 분류할 수 있을까?
그래프 상에서 주변을 둘러보는 것이다.
예를 들어, 가장 가까운 이웃 3개가 오렌지이고 자몽보다 많다면, 이 과일은 아마도 오렌지 일 것이다.

이러한 과정을 통해 분류를 하는 것을 KNN 알고리즘이라고 한다.
1. 분류할 과일이 있다.
2. 가장 가까운 3개의 이웃을 살펴본다.
3. 이웃 중에 오렌지가 많으면 이 과일은 오렌지이다.

## 추천 시스템 만들기
넷플릭스에서 일한다고 생각해보자. 고객을 위한 영화추천 시스템을 만들고 싶다.

우선 모든 고객을 그래프에 그린다.
유사도를 이용하여 고객을 그래프 상에 표현한다. 즉, 서로 취향이 비슷한 고객을 근접한 위치에 그린다.
A라는 고객을 위해 어떤 영화를 추천해야 한다고 가정하자.
A와 취향이 가장 비슷한 다섯 명의 고객을 찾는다.

이 그래프가 있으면 추천 시스템을 만드는 것은 쉽다.
만약 비슷한 취향을 가지고 있는 B가 영화를 좋아한다면 그 영화를 A에게도 추천한다.
1. B가 어떤 영화를 봤다.
2. B는 그 영화가 마음에 든다.
3. A에게 그 영화를 추천한다.

그렇다면 도대체 고객 사이의 유사도는 어떻게 구하는 것일까?

### 특징 추출
자몽 문제에서는 과일의 크기와 불은 정도를 통해 과일을 분류하였다.
이 특징을 이용해서 세 개의 과일을 그래프에 그릴 수 있다.

|비교대상 | 크기 | 붉은 정도 |
|-------|-----|--------|
| A     | 2   | 2      |
| B     | 2   | 1      |
| C     | 4   | 5      |

그래프 상, 두 점 사이의 거리를 재려면 피타고리스의 정리를 사용한다.
~~~
루트(x1-x2)제곱 + 루트(y1-y2)제곱
~~~

A와 B의 거리는 다음과 같이 계산한다.
= 루트(2-2)제곱 + 루트(2-1)제곱
= 루트 (0+1)
= 루트 1
= 1

나머지 거리도 같은 방법으로 계산할 수 있다.

넷플릭스 고객을 비교한다고 가정해보자.
과일처럼 고객을 그래프에 나타낼 수 있는 방법, 즉 각 고객의 좌표를 계산할 수 있는 방법을 찾아내어 그래프 상에 표현한다.

고객이 처음 넷플릭스에 등록할 때 여러가지 영화 장르에 대한 선호도를 평가하도록 한다.
|      | A | B | C |
|------|---|---|---|
| 코미디 | 3 | 4 | 2 |
| 액션  | 4 | 3 | 5 |
| 드라마 | 4 | 5 | 1 |
| 공포  | 1 | 1 | 3 |
| 로맨스 | 4 | 5 | 1 |

자몽 문제에서는 과일을 두개의 숫자로 나타냈던 것을 다섯 개의 숫자로 나타낸다.
이제는 2차원이 아닌 5차원 상에서 거리를 측정해야 한다.
하지만 거리 계산 공식은 동일하다.

~~~
루트(a1-a2)제곱 + 루트(b1-b2)제곱 + 루트(c1-c2)제곱 + 루트(d1-d2)제곱 + 루트(e1-e2)제곱
~~~

거리를 구하는 공식은 공간의 차원을 유연하게 바꿀 수 있다.
이때의 거리는 두 숫자 집합의 유사도, 즉 두 숫자 집합이 얼마나 비슷한지를 나타낸다.

A와 B의 유사도를 구하면 다음과 같다.
= 루트(3-4)제곱 + 루트(4-3)제곱 + 루트(4-5)제곱 + 루트(1-1)제곱 + 루트(4-5)제곱
= 루트 (1+1+1+0+1)
= 루트 4
= 2

거리가 가까우므로 취향이 비슷하다고 할 수 있다.
B가 어떤 영화를 좋아하면 A에게 추천하고, 반대로 A가 어떤 영화를 좋아하면 B에게 추천하면 된다.
그래서 넷플릭스를 이용하다보면 '더 많은 영화를 평가해주세요', '여러분이 더 많은 영화를 평가할 수도록 추천 영화가 더 정확해집니다'라는 공지를 보게 된다.
더 많은 영화를 평가할 수록 넷플릭스는 다른 고객과의 유사도를 더 정확하게 평가할 수 있기 때문이다.

### 회귀분석
어떤 영화에 대해 C가 어떤 평점을 줄지 예측하고 싶다면 어떻게 해야할까?
우선 C와 비슷한 5명의 데이터를 모은다.
꼭 5명일 필요는 없다. C와 유사한 2명 혹은 10,000명 일수도 있다.
그래서 알고리즘의 이름도 5NN이 아니라 KNN인 것이다.

KNN은 분류와 회귀 분석의 두 가지 기능이 있다.
* 분류 : 그룹으로 나누기
* 회귀 : (숫자로 된) 반응을 예측하기

회귀 분석은 다음과 같은 상황에 유용하게 사용된다.
베이커리에서 오늘은 빵을 몇개 만들어야 할지 예측하고 싶다.
분석에 사용할 특징 정보는 다음과 같다.

* 1점부터 5점까지 숫자로 표현한 날씨(1=날씨가 최악, 5=날씨가 최고)
* 주말 또는 휴일인지?(주말이나 휴일이면 1이고, 평일이면 0)
* 스포츠 경기가 있는지?(있으면 1, 없으면 0)

여러가지 다른 특징 값이 주어졌을 때 빵이 얼마나 팔렸는지 과거의 판매 정보를 통해 알고 있다고 하자.

| 빵 종류 | 날씨 | 평일 or 주말 | 스포츠 경기 유무 | 팔린 갯수 |
|-------|-----|------------|--------------|---------|
| A     | 5   | 1          | 0            | 300     |
| B     | 3   | 1          | 1            | 225     |
| C     | 1   | 1          | 0            | 75      |
| D     | 4   | 0          | 1            | 200     |
| E     | 4   | 0          | 0            | 150     |
| F     | 2   | 0          | 0            | 50      |

오늘은 날씨가 좋은 주말이다. 위의 데이터를 보았을 때 빵이 얼마나 팔릴까? (4, 1, 0)
각각의 데이터로부터 거리를 계산한다.

* A : 1 <--
* B : 2 <--
* C : 9
* D : 2 <--
* E : 1 <--
* F : 5

A, B, D, E가 가장 가깝다. 이 날들의 평균을 구하면 218.75가 된다. 
빵을 반올림하여 219개 만들면 된다.

### 좋은 특징 고르기
KNN을 사용할 때는 올바른 특징을 고르는 것이 중요하다.
올바른 특징이란 다음과 같다.

* 추천하고자 하는 영화와 직접 관련이 있는 특징
* 편향되지 않은 특징 (예를 들어 코미디 영화에 대한 평점만 있다거나 액션 영화에 대한 평점만 있는 경우)

하지만 평점이라는 것이 영화를 추천하는 가장 좋은 방법일까?
예를 들어, A라는 영화에 좋은 평점을 주었지만, B라는 영화를 더 자주 본다면?
좋은 특징을 고르는데 있어 이것이 정답이다라는 것은 없다.
여러가지 관점에서 살펴 보아야 한다.

## 머신러닝
머신러닝이란 컴퓨터를 더 영리하게 만드는 모든 것을 말한다.
추천 시스템도 머신러닝의 한가지이다.

### OCR
OCR은 광학적 문자인식(Optical Character Recognition)의 약자이다.
책 페이지를 사진으로 찍으면, 컴퓨터가 자동으로 그 사진 속으 글자를 읽어주는 것이다.
구글은 OCR을 사용해서 책을 디지털화 하였다.
OCR은 어떻게 동작하는 것일까?

예를 들어, 7과 같은 숫자 그림이 무슨 숫자인지 자동으로 알게하려면 어떻게 해야할지 생각해보자.
1. 여러가지 숫자 그림을 살펴보고 이 그림들의 특징을 뽑아낸다.
2. 새로운 그림이 주어지면 그 그림의 특징을 뽑아서 가장 가까운 것들을 살펴본다

이 문제는 오렌지와 자몽 문제와 같다.
보통 OCR 알고리즘은 직선, 점, 곡선 등을 찾아낸다.
그런 다음에 새로운 글자가 나타나면 그 글자에서 똑같은 특징을 뽑아낸다.
* 3 : 곡선 -> 점 -> 직선
* 7 : 직선 -> 점 -> 직선 -> 점 -> 직선

OCR에 사용되는 특징 추출은 오렌지와 자몽 문제보다 훨씬 복잡하지만, 아무리 복잡한 기술이라도 KNN과 같은 간단한 아이디어에 기반하고 있다는 점을 이해하는 것이 중요하다.

OCR의 첫번재 단계는 숫자 그림으로부터 특징을 추출하면서 모든 데이터를 살표보는 것이다.
이것을 트레이닝이라고 한다.
컴퓨터가 어떤 일을 하려면 반드시 트레이닝 단계를 거쳐야 한다.

### 스팸 필터 만들기
스팸필터는 나이브 베이즈 분류기라고 하는 간단한 알고리즘을 사용한다.
다음과 같은 데이터로 나이브 베이즈 분류기를 트레이닝 한다.

| 제목                                   | 스팸인가?   | 
|---------------------------------------|-----------|
| 패스워드를 재설정하세요                     | 스팸이 아니다 |
| 백만 달러를 벌어보세요                     | 스팸이다     |
| 패스워드를 보내주세요                      | 스팸이다     |
| 나이지리아의 왕자가 당신에게 천만불을 보냈습니다  | 스팸이다     |
| 생일 축하합니다                          | 스팸이 아니다  |

만약에 '백만 달러를 벌어보세요'라는 제목을 가진 이메일이 온다면 어떨까?
이 문장을 단어로 쪼갠다.
각 단어마다 그 단어가 스팸 메일에 나타날 확률을 구한다.

예를 들어, 가장 간단한 모형에서 '백만'이라는 단어가 스팸 메일에서만 발견된다고 해보자.
그러면 나이브 베이즈 분류기는 이 메일이 스팸 메일이라고 찾아낸다.
이 방법은 KNN알고리즘과 비슷하게 응용될 수 있다.

예를 들어, 과일을 분류할 때도 나이브 베이즈 분류기를 사용할 수 있다.
크고 붉은 과일이 있으면 그 과일이 자몽일 확률도 구할 수 있다.

### 주식시장 예측하기
머신러닝으로 하기 힘든 일이 있다.
내일 주식 시장이 오를지 내릴지를 맞추는 일이다.
주식 시장의 어떤 특징을 골라야할까?
미래를 예측하는 일 자체가 힘들고, 특히 많은 변수가 관련되어 있는 경우에는 사실상 예측이 불가능하다.

## Summary
* KNN은 k개의 가장 가까운 이웃 데이터를 이용하여 분류와 회귀 분석을 할 수 있다.
* 분류 = 그룹으로 나누는 작업
* 회귀 = 숫자로 된 반응을 예측
* 특징 추출은 (과일이나 고객과 같은) 항목을 비교 가능한 몇 개의 숫자로 만드는 일이다.
* 좋은 특징을 고르는 것은 성공적인 KNN 알고리즘을 만드는데 있어 중요한 부분이다.