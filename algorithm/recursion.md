# `재귀`
창고를 뒤지다가 자물쇠가 걸려있는 다이어리를 발견했다.
초등학생 때 썼던 다이어리로, 열쇠는 다른 상자에 넣어서 보관하고 있었다.
큰 상자 속에는 작은 상자들이 있고, 그 작은 상자들 안에는 더 작은 상자들이 있다.
열쇠는 그 상자 속 어딘가에 있다. 열쇠를 찾기 위한 알고리즘은 어떻게 될까?

## `첫번째 방법`
1. 내부를 확인할 상자를 쌓아놓는다.
2. 상자를 하나씩 집어서 내부를 살핀다
3. 만약에 안에 작은 상자가 또 있다면 꺼내어 나중에 확인할 상자 더미에 놓는다.
4. 만약 열쇠가 있으면 작업 종료
5. 반복한다.

## `두번째 방법`
1. 상자 안을 확인한다.
2. 만약에 작은 상자가 또 들어있다면 1단계로 간다.
3. 만약에 열쇠를 발견하면 작업 종료

첫번째 방법은 While문을 사용한다.
상자더미가 남아있을 때 까지 확인하는 것이다.

<첫번째 방법의 의사코드(Pseudocode)>  
***의사코드(Pseudocode): 문제와 풀이 방법을 간단한 코드 형태로 표현한 것***
~~~
public void lookingForKey() {
    List<Box> boxPile = new ArrayList<>();

    while(boxPile.length() > 0) {
        for(Box box : boxPile) {
            if(box.existBox()) boxPile.add(box);
            else if(box.existKey()) System.out.println("열쇠 찾음");
        }
    }
}
~~~

두번째 방법은 재귀를 사용한다.
재귀란, `자기 자신을 호출`하는 문제해결 알고리즘이다.
~~~
public void lookingForKey(Box box) {
    for(Item item : box) {
        if(item.isBox) lookingForKey(item);
        else if(item.isKey) System.out.println("열쇠 찾음");
    }
}
~~~

재귀는 풀이를 더 명확하게 만들어준다.
성능이 더 나아지는 것은 아니고, 오히려 반복문이 성능이 더 좋은 경우가 많다.
