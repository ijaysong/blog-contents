# 동적 프로그래밍

## 배낭 채우기 문제
4Kg의 짐을 넣을 수 있는 가방이 있다고 해보자.
가방에 넣을 물건의 가치를 최대치로 놓이려면 어떤 물건을 넣어야 할까.

|물건    | 가격   | 무게 |
|-------|-------|-----|
|스테레오 | 3,000 | 4kg |
|노트북  | 2,000 | 3kg |
|기타    | 1,500 | 1kg |

### 단순한 방법
가장 단순한 방법은 모든 물건의 조합을 시도해서 각 경우의 총 가치를 모두 구해본 다음, 가장 가치가 놓은 경우를 선택하는 것이다.

|No. | 물건                | 가치                |
|----|--------------------|--------------------|
|1   | 물건 없음            | 0                  |
|2   | 기타                | 1,500              |
|3   | 스테레오             | 3,000              |
|4   | 노트북              | 2,000              |
|5   | 기타, 스테레오        | (배낭에 들어가지 않음)  |
|6   | 기타, 노트북         | 3,500              |
|7   | 스테레오, 노트북      | (배낭에 들어가지 않음)  |
|8   | 기타, 스테레오, 노트북 |  (배낭에 들어가지 않음) |

이 방법은 가능한 방법이긴 하지만, 너무 느리다.
물건이 3개이면 계산해야 하는 경우의 수가 8개, 물건이 4개이면 16개.
물건을 추가할 때마다 경우의 수가 2배가 된다. 알고리즘 실행시간은 O(n제곱). 너무 느리다.

### 동적 프로그래밍
동적 프로그래밍은 하위 작은 문제들을 풀고, 이를 이용해서 더 큰 문제를 풀어나가는 방법이다.
모든 동적 프로그래밍 알고리즘은 격자(grid)로부터 시작한다.
* 격자의 행(row) : 물건
* 격자의 열(column) : 1~4kg까지 물건을 담을 수 있는 다른 크기의 배낭이다.

|       | 1 | 2 | 3 | 4 |
|-------|---|---|---|---|
|기타    |   |   |   |   |
|스테레오 |   |   |   |   |
|노트북  |   |   |   |   |

격자는 빈 상태에서 시작하고, 격자를 모두 채우면 문제에 대한 답이 나온다.

#### 기타를 표시하는 행
 첫번째 행은 기타만 선택해 표시하는 행이다.
 즉, 이 행에서는 기타만 배낭에 넣을 수 있다는 뜻이다.

첫번째 칸은 1kg까지 들어갈 수 있는 배낭을 뜻한다.
기타가 1kg이므로 이 간에 기타를 담을 수 있다. 전체 가치는 1,500달러이다.
|       | 1   | 2 | 3 | 4 |
|-------|-----|---|---|---|
|기타    |1,500|   |   |   |
|스테레오 |     |   |   |   |
|노트북  |     |   |   |   |

두번째 같은 2kg까지 담을 수 있는 배낭이다. 그러니 당연히 기타가 들어갈 수 있다.
나머지 칸에 대해서도 똑같이 진행한다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |     |     |     |     |
|노트북  |     |     |     |     |

배낭 안의 모든 물건의 총 가치를 최대화 하는 것이 목표이다.
현 시점에서 배낭에서 가질 수 있는 최대값은 1,500달러이다.

#### 스테레오를 표시하는 행
두번째 행은 스테리오나 기타 중에 선택해서 넣을 수 있다.
각 행에서 처음 행부터 그 행까지 있는 물건을 넣을 수 있다.

첫번째 칸, 즉 1kg 용량의 배낭부터 시작한다.
현재까지 1kg 배낭에 넣을 수 있는 물건의 최대치는 1,500달러이다.
스테레오도 넣어야 할까?
스테레오는 4kg이므로, 배낭에 들어가지 않는다. 그러니 1kg 배낭의 최대 가치는 여전히 1,500달러이다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|     |     |     |
|노트북  |     |     |     |     |

다음 두칸도 마찬가지 이다.
이 배낭들은 각각 2kg과 3kg짜리이다. 지금까지의 최대 가치는 둘다 1,500달려였다.
스테레오가 들어가지 않기 때문에 답은 그대로이다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|1,500|1,500|     |
|노트북  |     |     |     |     |

4kg이 들어가는 배낭은 어떨까? 이제 스테레오가 들어간다.
지금까지 최대 가치는 1,500달러였지만, 기타 대신 스테레오를 넣으면 최대 가치가 3,000달러가 된다.
4kg 배낭에 스테레오를 넣는 것으로 갱신한다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|1,500|1,500|3,000|
|노트북  |     |     |     |     |

#### 노트북을 표시하는 행
노트북을 표시하는 행에서도 같은 일을 해봅시다.
노트북은 3kg이니까 1kg나 2kg짜리 배낭에는 들어가지 않는다.
처음 두 칸의 값은 그대로 1,500달러이다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|1,500|1,500|3,000|
|노트북  |1,500|1,500|     |     |

3kg짜리 배낭의 경우, 지금까지의 답은 1,500달러였다.
하지만 기타 대신 노트북을 고르면 2,000달러가 되므로 새로운 최대 가치는 2,000달러이다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|1,500|1,500|3,000|
|노트북  |1,500|1,500|2,000|     |

4파운드의 경우, 재미있는 상황이 된다.
지금까지의 최대 가치는 3,000달러였다.
만약 배낭에 노트북만 넣는다면 단지 2,000달러 밖에 되지 않는다.
하지만 비어있는 1kg에 무언가를 넣는다면? (노트북이 들어가는 행의 1kg짜리 물건을!)
3,500달러가 된다.
* 노트북(2,000달러) + 기타(1,500) = 3,500달러

배낭에 공간이 남게 되었을때, 하위 문제에 대한 답을 사용하여 빈 공간의 가치가 최대가 되는 값을 찾아낼 수 있다.
이 경우, 노트북과 기타를 합쳐서 3,500달러가 되는 것을 선택한다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|1,500|1,500|3,000|
|노트북  |1,500|1,500|2,000|3,500|


=> 배낭 채우기 문제의 정답
: 배낭에 넣을 수 있는 물건의 가치는 3,500달러이고, 그 물건은 기타와 노트북이다.

지금까지는 공식을 사용하지 않고 배낭 채우기 문제를 풀었지만, 다음과 같은 공식으로도 풀이할 수 있다.

`CELL[i][j]의 최대값`
1. 지금까지 구한 CELL[i-1][j]의 값 중에서 가장 최대값
2. 또는, 현재 물건의 가치 + 남은 공간의 가치(CELL[i-1][j-물건의 가치])
 
 ### 배낭 채우기 문제 심화 풀이
 #### 1. 만약 물건이 추가된다면
 새로운 물건이 추가되면 문제를 처음부터 다시 풀어야 할까?
 동적 프로그래밍은 점진적으로 답을 수정해 나가는 방법이다.
 새로운 물건을 격자 행에 추가한다. 아이폰을 나타내는 행을 추가해보자.

|       | 1 | 2 | 3 | 4 |
|-------|---|---|---|---|
|기타    |   |   |   |   |
|스테레오 |   |   |   |   |
|노트북  |   |   |   |   |
|아이폰  |   |   |   |   |

아이폰은 1kg에 2,000달러의 가치가 있는 물건이다.
해당 내용을 격자에 반영해 보자.
아이폰은 1kg 배낭에 들어간다. 지금까지 최대가치는 1,500달러였지만, 2,000달러를 최대치로 반영한다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|1,500|1,500|3,000|
|노트북  |1,500|1,500|2,000|3,500|
|아이폰  |2,000|     |     |     |

다음 칸에는 아이폰과 기타가 들어간다.
3번째 칸에도 아이폰과 기타를 넣는 것이 최대이다. 

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|1,500|1,500|3,000|
|노트북  |1,500|1,500|2,000|3,500|
|아이폰  |2,000|3,500|3,500|     |

마지막 칸의 경우 재미있어진다.
지금까지의 최대가치는 3,500달러였다.대신에 아이폰을 넣는다면 3kg의 공간이 남는다.
이전에 풀었던 하위 문제에 의하면 3kg 공간이 2,000달러이고, 아이폰도 2,000달러이므로 총 가치는 4,000달러이다. 새로운 최대 가치를 반영한다.

|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|기타    |1,500|1,500|1,500|1,500|
|스테레오 |1,500|1,500|1,500|3,000|
|노트북  |1,500|1,500|2,000|3,500|
|아이폰  |2,000|3,500|3,500|4,000|

#### 2.만약 행의 순서가 바뀐다면
만약 행을 스테레오, 노트북, 기타의 순서대로 놓았다고 가정해보자.
|       | 1   | 2   | 3   | 4   |
|-------|-----|-----|-----|-----|
|스테레오 |0    |0    |0    |3,000|
|노트북  |0     |0    |2,000|3,000|
|기타    |1,500|1,500|2,000|3,500|

답이 바뀌지 않는다.
즉, 행의 순서에는 영향을 미치지 않는다.

#### 3. 더 작은 물건을 추가한다면
목걸이도 넣을 수 있다고 가정을 해보자.
목걸이의 무게는 0.5kg이고, 1,000달러의 가치가 있다.
4kg짜리 배낭에 목걸이를 넣는다고 하면, 3.5kg의 공간이 남는다.
이 공간에 들어갈 수 있는 최대 가치는 얼마일까? 지금은 알 수 없다.

지금까지는 모든 무게가 정수인 1kg, 2kg, 3kg, 4kg에 대해서만 계산했기 때문에,
새로 3.5kg의 배낭에 대한 최대가치도 구해야 한다.

목걸이를 담고 싶다면 다음과 같이 배낭의 무게를 세분화를 하여 격자를 구성해야 한다.

|       | 0.5 | 1  | 1.5 | 2 | 2.5 | 3 | 3.5 | 4 |
|-------|-----|----|-----|---|-----|----|-----|---|
|기타    |     |    |     |   |     |    |     |   |
|스테레오 |     |    |     |   |     |    |     |   |
|노트북  |     |    |     |   |     |    |     |   |
|아이폰  |     |    |     |   |     |    |     |   |

## 여행 일정 문제
런던으로 휴가를 떠난다고 해보자.
런던에 이틀동안 머물면서 하고 싶은 것을 가능한 많이 해보고 싶다.
모든 곳을 다 갈 수 없으니 가고 싶은 곳의 표를 만든다.

보고 싶은 곳마다 걸리는 시간과 얼마나 보고 싶은지 나타낸 점수를 적는다.
| 관광지         | 소요 시간 | 점수 |
|--------------|---------|-----|
| 웨스트민스터 사원 | 1/2일   | 7   |
| 글로브 극장     | 1/2일   | 6   |
| 국립 갤러리     | 1일     | 9   |
| 대영 박물관     | 2일     | 9   |
| 세인트 폴 대성당 | 1/2일   | 8   |

이 표를 바탕으로 어떤 곳을 돌아볼지 결정할 수 있을까?
배낭 채우기 문제와 같다.
배낭이라는 공간 대신 시간이 한정되어 있고, 스테레오나 노트북 대신 가고 싶은 곳이 있다.
이 문제를 풀이 위해선 우선 동적 프로그래밍을 위한 격자를 그린다.

|              | 1/2 | 1   | 1+1/2 | 2   |
|--------------|-----|-----|-------|-----|
| 웨스트민스터 사원 |     |     |       |     |
| 글로브 극장     |     |     |       |     |
| 국립 갤러리     |     |     |       |     |
| 대영 박물관     |     |     |       |     |
| 세인트 폴 대성당 |     |     |       |     |

격자를 채우면 다음과 같은 답이 된다.

|              | 1/2 | 1   | 1+1/2 | 2    |
|--------------|-----|-----|-------|------|
| 웨스트민스터 사원 | 7w  | 7w  | 7w    | 7w   |
| 글로브 극장     | 7w  | 13wg| 13wg  | 13wg |
| 국립 갤러리     | 7w  | 13wg| 16wn  | 22wgn|
| 대영 박물관     | 7w  | 13wg| 16wn  | 22wgn|
| 세인트 폴 대성당 | 8s  | 15ws| 21wgs | 24wns|

* w : 웨스트민스터 사원
* g : 글로브 극장
* n : 국립 갤러리
* g : 대영 박물관
* s : 세인트 폴 대성당

### 서로 의존적인 항목 다루기
이번에는 파리 여행도 가고 싶다.
그래서 표에 장소를 몇개 추가한다.
| 관광지         | 소요 시간 | 점수 |
|--------------|---------|-----|
| 에펠탑         | 1+1/2일 | 8   |
| 루브르 박물관    | 1+1/2일 | 9   |
| 노트르담 대성당  | 1+1/2일 | 7   |

소요시간에는 런던에서 파리로 가는 시간 0.5시간이 추가되어 있다.
일단 파리로 가면 각 관광지를 돌아보는데는 하루 밖에 걸리지 않는 것이다. 
(세 군데를 모두 돌면 3일+반나절)

이러한 경우는 등적 프로그래밍으로 어떻게 풀까?

이 문제는 풀수 없다.
동적 프로그래밍은 문제를 더 작은 하위 문제로 풀고, 이 하위 문제를 푼 결과를 이용해서 더 큰 문제를 푸는 방법이다.
하지만 동적 프로그래밍은 각 하위 문제들이 서로 관계가 없을 때,  즉 서로 의존하지 않는 경우에만 쓸 수 있다.
따라서 파리까지 고려하게 되면 동적 프로그래밍 알고리즘으로는 문제를 풀 수 없다.

## 최장 공통 부분 문자열
만약에 dictionary.com이라는 웹 서비스를 운여하고 있다고 가정해보자.
사용자가 단어를 입력하면 해당 단어에 대한 정의를 보여준다.
만약 사용자가 철자를 틀리면 원래 어떤 단어를 검색하고자 했는지 추측해야 한다.

예를 들어, fish라는 단어를 찾아보고 싶었는데, 실수로 hish라고 입력했다.
이 단어는 사전에는 없고, 대신 비슷한 단어들이 있는데 다음과 같다.
* fish
* vista

입력한 hish는 fish를 뜻하는 것일까, 아니면 vista를 뜻하는 것일까?

### 격자 만들기
격자를 만들기 전에 다음 항목에 대해 생각해보아야 한다.
* 각 칸에 넣을 숫자는 무엇인지
* 이 문제를 어떻게 하위 문제로 나눌 수 있는지
* 격자 축은 무엇인지

동적 프로그래밍에서는 무언가를 `최대화` 하는 것이 목표이다.
이 문제에서는 두 단어에서 공통적으로 가지는 가장 긴 부분 문자열, 즉 `최장 공통 부분 문자열`을 찾는 것이 목표이다.
hish와 fish 혹은 hish와 vista가 공통 부분 문자열을 가지고 있는지 계산해보자.

|   | h | i | s | h |
|---|---|---|---|---|
| f |   |   |   |   |
| i |   |   |   |   |
| s |   |   |   |   |
| h |   |   |   |   |

### 격자 채우기
행과 열의 글자를 비교하여 만약 글자가 다르면 값은 `0`으로 지정한다.
만약 글자가 같으면 값은 `좌측 상단 칸의 값 + 1`이 된다. 

격자에 값을 채우면 다음과 같다.

|   | h | i | s | h |
|---|---|---|---|---|
| f | 0 | 0 | 0 | 0 |
| i | 0 | 1 | 0 | 0 |
| s | 0 | 0 | 2 | 0 |
| h | 1 | 0 | 0 | 3 |

의사코드로 나타내면 다음과 같다.
~~~
if(wordA[i].equals(wordB[j])) {
    // 글자가 같으면
    cell[i][j] = cell[i-1][j-1] + 1;
} else {
    // 글자가 다르면
    cell[i][j] = 0;
}
~~~

hish와 vista의 경우, 다음과 같다.

|   | h | i | s | h |
|---|---|---|---|---|
| v | 0 | 0 | 0 | 0 |
| i | 0 | 1 | 0 | 0 |
| s | 0 | 0 | 2 | 0 |
| t | 0 | 0 | 0 | 0 |
| a | 0 | 0 | 0 | 0 |

여기에선 한가지 주의할 점이 있다.
이 문제의 경우, 마지막 칸이 최종 답이 아니다. (격자[5][4]: 답 아님)
배낭 채우기 문제에서는 마지막 칸이 최종 답이였지만, 최장 공통 부분 문자열 문제에서의 답은 격자 전체에서 가장 큰 숫자가 답이다. (격자[3][3]: 정답)

=> fish와 vista 중에서 어떤 것이 hish와 공통 부분 문자열이 가장 많은 단어인가 살펴보면 fish는 세 글자가 공통이고, vist는 2글자가 공통이므로 결과적으로 fish를 입력하고자 했음을 알 수 있다.

### 최장 공통 부분열
만약 실수로 fosh라고 입력했다고 해보자.
어떤 단어를 입력하려 했던 것일까? fish일까 fort일까?
격자로 나타내면 다음과 같다.

<fosh와 fish>
|   | f | o | s | h |
|---|---|---|---|---|
| f | 1 | 0 | 0 | 0 |
| i | 0 | 0 | 0 | 0 |
| s | 0 | 0 | 1 | 0 |
| h | 1 | 0 | 0 | 2 |

<fosh와 fort>
|   | f | o | s | h |
|---|---|---|---|---|
| f | 1 | 0 | 0 | 0 |
| o | 0 | 2 | 0 | 0 |
| r | 0 | 0 | 0 | 0 |
| t | 1 | 0 | 0 | 0 |

fish와 fort 모두 답이 2글자로 같다.
하지만 fosh가 fish에 더 가까운 단어이다.
즉, 두 단어에서 순서가 바뀌지 않고, 공통으로 들어간 글자의 개수를 최대화 하는 것이 옳다.
그렇다면 최장 공통 부분열을 어떻게 계산할까?

1. 윗쪽칸과 왼칸 중에서 글자가 같지 않으면, 둘 중 더 큰 값을 선택한다. (여기가 최장 공통 부분 문자열 문제와 다르다.)
2. 만약 글자가 같으면 이 값은 `좌측 상단 칸의 값 + 1`이다. (여기는 최장 공통 부분 문자열 문제와 같다.)

<fosh와 fish>
|   | f | o | s | h |
|---|---|---|---|---|
| f | 1 | 1 | 1 | 1 |
| i | 1 | 1 | 1 | 1 |
| s | 1 | 1 | 2 | 2 |
| h | 1 | 1 | 2 | 3 |

<fosh와 fort>
|   | f | o | s | h |
|---|---|---|---|---|
| f | 1 | 1 | 1 | 1 |
| o | 1 | 2 | 2 | 2 |
| r | 1 | 2 | 2 | 2 |
| t | 1 | 2 | 2 | 2 |

의사코드로 나타내면 다음과 같다.
~~~
if(wordA[i].equals(wordB[j])) {
    // 글자가 같으면
    cell[i][j] = cell[i-1][j-1] + 1;
} else {
    // 글자가 다르면
    cell[i][j] = Math.max(cell[i-1][j], cell[i][j-1]);
}
~~~

## Summary
* 동적 프로그래밍은 제한 조건이 있는 경우에 무언가를 최적화 할 때 유용하다.
* 동적 프로그래밍은 큰 문제를 작은 하위 문제로 나누어 푸는 방법이다.
* 동적 프로그래밍을 풀 때는 격자로 사용한다.
* 보통 격자의 한 칸에는 최적화하려는 값을 쓴다.
* 격자의 각 칸은 하위 문제를 뜻한다. 그러므로 원래의 문제를 어떻게 하위 문제로 나눌 수 있는지 생각해야 한다.
* 동적 프로그래밍의 해답을 계산해주는 쉬운 공식 같은 것은 없다.