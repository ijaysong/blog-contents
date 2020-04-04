# 스택/큐

1.  스택  
쌓여진 그릇같은 형태.  
가장 나중에 들어온 것이 가장 먼저 나간다.(후입선출 : LIFO, Last In First Out)

```
// 스택이 비어있는지 확인한다.
empty() : boolean  

// 스택의 맨윗부분에 있는 데이터를 삭제하지 않고 해당 데이터만 반환한다.  
peek() : data type of Stack array

// 등록 : 스택의 맨윗부분에 데이터를 추가한다.
push(data): void

// 삭제 : 스택의 맨윗부분에 있는 데이터를 삭제하며 해당 데이터를 반환한다.  
pop() : data type of Stack array

// 검색 : 해당 데이터가 스택에서 어느 위치에 있는지 반환한다. (1-based)  
search(data):int
```

2.  큐  
맛집에 들어가기 위해서 길게 줄을 서있는 형태.  
가장 나중에 들어온 것이 가장 나중에 나간다.(후입후출 : LILO, Last In Last Out)
    
```
// 등록 : 스택에 공간이 있어 등록할 수 있었다면, true 반환. 등록 못했을 시 IllegalStateException 발생.
add(data) : boolean

// 검색 : 큐의 맨 앞에 있는 값을 검색만 하고 삭제하진 않는다.  
element() : data type of Queue Array

// 등록 : 큐에 해당 값을 등록한다.  
offer(data) : boolean

// 큐의 맨 앞에 있는 값을 반환하며 삭제한다. 큐가 비어있을 시, null이 반환된다.  
peek() : data type of Queue Array

// 삭제 : 큐의 맨 앞에 있는 데이터를 삭제하며 반환한다. 데이터가 없으면, null을 반환한다.  
poll() : data type of Queue Array

// 삭제 : 큐의 맨 앞에 있는 데이터를 삭제하며 반환한다.  
remove() : data type of Queue Array
```
