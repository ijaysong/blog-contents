생활 코딩, 지옥에서 온 Git을 수강하고...

# 버전관리의 본질
## Mac에서 Git 설치유무 확인
~~~bash
// Git 설치유무 확인
git
~~~

## 저장소 만들기
~~~bash
// 원하는 위치에 디렉토리(워크스페이스)를 만들기
mkdir {저장소 이름}

// 해당 디렉토리 안으로 이동
cd {저장소 이름}

// 현재 디렉토리를 사용하겠다고 Git에 알려줌
git init 
~~~
git init 실행 후 생성되는 .git 파일은 여러 버전 정보를 담고 있음.

## git이 관리할 대상으로 파일 등록
~~~bash
// 파일을 생성
vim {파일명.확장자}

// git이 파일을 추적하도록 명령한다.
git add {파일명.확장자}

// 커밋
git commit

// 프로젝트 폴더의 상태를 확인한다.
git status

// 깃 로그를 확인
git log
~~~

## 버전만들기
버전이란 작업이 완결된 상태라 할 수 있다.  
이미 커밋이 된 파일을 수정할 때도 아래의 명령어를 수행하여 커밋을 해야한다. (staging의 개념)  
선택적으로 파일을 버전에 포함시키기 위함이다.  
~~~bash
git add {파일명.확장자}
~~~

## 변경사항 확인하기
~~~bash
// 버전 간의 차이점을 로그로 출력하고 싶을 때
git log -p

// 버전 간의 차이점을 비교할 때
git diff {버전 id}..{버전 id2}

// git add하기 전과 add한 후의 파일 내용을 비교할 때
git diff
~~~

git diff는 커밋 전에 변경한 소스 코드를 재검토 하기에 좋은 커맨드이다.

## 과거의 버전으로 돌아가기
~~~bash
git reset --hard {버전 id}
~~~
reset : 버전 id로 돌아가는 명령, 로컬에 있는 파일에 대해서만 수행해야 됨
revert : 버너 id의 커밋을 취소한 내용을 새로운 버전으로 만드는 명령

## 명령의 빈도와 메뉴얼 보는 방법
~~~bash
// commit 명령어에 대한 메뉴얼 확인한다
git commit --help

// add 명령어의 staging을 자동으로 수행하며 커밋한다
git commit -a

// 커밋 메세지를 지정하여 커밋을 수행
git commit -m "{커밋 메세지}"

// -a와 -m 옵션을 동시에 수행
// staging을 자동으로 수행하며 커밋 메세지를 지정하여 커밋한다
git commit -am "{커밋 메세지}"
~~~

# git의 원리
git 내부적으로 어떤 일이 일어나는지 살펴본다.

## git add의 원리
git은 add를 하면 index와 objects(객체)가 생성된다.
* index : 각각의 파일명과 인덱스가 적혀있다.
* objects/{인덱스} : add한 파일의 내용이 저장된다.

git은 파일을 저장할 때 파일 이름이 달라도 같은 내용을 가지면 같은 인덱스를 가진다. 
만개의 파일을 저장하기 위해 많은 데이터가 필요한데, 해당 파일들이 같은 내용이라면 같은 오브젝트를 가리키므로 git은 매우 효율적으로 중복 데이터를 저장할 수 있다.

## objects 파일명의 원리
git은 내용을 기반으로파일 이름이 정해지는 매커니즘을 가지고 있다. (내용이 같으면 파일의 이름이 같음) 
sha1 이라는 해쉬 알고리즘을 통해서 이름을 결정한다.

예를 들어, hello 를 sha1으로 변환해본다면 다음과 같다.
~~~
hello -sha1-> aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
~~~

sha1으로 변환된 이름의 첫번째 두자리(aa)는 디렉토리로 생성되며, 나머지는 파일 이름으로 지정된다.

~~~
objects/aa/f4c61ddcc5e8a2dabede0f3b482cd9aea9434d
~~~

## commit의 원리
~~~bash
git commit
~~~

커밋도 내부적으로는 objects 파일 안에 저장된다.
tree, parent, 누가 저장했는지, 내용 등이 저장된다.
blob은 파일의 내용을 담는다.
tree 구조로 이전에 커밋한 내용과 새롭게 커밋한 내용들이 담긴다.

## status의 원리
~~~bash
git status
~~~
objects 파일 안의 tree와 인덱스 파일이 일치한다면, git status를 실행했을 때 커밋할 사항이 없다고 알려준다.
스테이징 되었고 커밋할 파일에 대해선, index에서 가리키고 있는 파일과 objects 파일이 연결되었으므로 index에 add 되어 커밋할 파일이 있음을 파악한다.
인덱스 파일에 등록된 파일이 local repository에 등록된다. = working directory의 파일을 git add 하여 staging area에 올라간다. (용어가 다양) 

# git의 혁신 - branch

## branch 만들기
어떤 기능을 추가할 때 branch를 생성하여 관리한다.

~~~bash
// 브랜치의 목록을 볼 때
git branch

// 브랜치를 생성할 때 
git branch {새로운 브랜치 이름}

// 브랜치를 삭제할 때
git branch -d

// 병합하지 않은 브랜치를 강제 삭제할 때 
git branch -D

// 브랜치를 전환(체크아웃)할 때
git checkout {전환하려는 브랜치 이름}

// 브랜치를 생성하고 전환까지 할 때 
git checkout -b {생성하고 전환할 브랜치 이름}
~~~

## branch 정보확인
~~~bash
// 브랜치 간에 비교할 
// 어떤 파일이 포함되어 있고 아닌지 보여줌
git log {비교할 브랜치 명 1}..{비교할 브랜치 명 2}

// 브랜치 간의 코드를 비교 할 때 
git diff {비교할 브랜치 명 1}..{비교할 브랜치 명 2}

// 로그에 모든 브랜치를 표시하고, 그래프로 표현하고, 브랜치 명을 표시하고, 한줄로 표시할 때 
git log --branches --graph --decorate --oneline 
~~~
