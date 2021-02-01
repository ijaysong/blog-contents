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

## branch 병합 (merge)
~~~bash
// A 브랜치로 B 브랜치를 병합할 때 (A ← B)
// 먼저 A 브랜치로 체크아웃 한다.
git checkout A
// B 브랜치를 병합한다
git merge B
~~~
위와 같은 경우에는 A를 부모로 하여 B 브랜치가 합쳐진다.

## branch 수련
### fast-forward
A 브랜치로 B 브랜치를 병합한다고 해보자.(A ← B)

`fast-forward`는 영어로 빨리 감기이다.
git에서 fast-forward는 다음과 같은 상황을 뜻한다.
A 브랜치보다 B 브랜치가 작업을 추가로 수행했을 때, 추가로 수행한 내용에 맞춰서 A 브랜치를 빨리감아 B브랜치와 병합한다.
커밋을 생성하지 않는다는 특징이 있다.

### recursive strategy
B 브랜치를 머지한 A 브랜치로 C 브랜치를 병합한다고 해보자. (A <- C)

`recursive strategy` 는 직역하자면 재귀적인 전략을 뜻한다.
A 브랜치와 C 브랜치는 공통의 작업을 수행하다가 두 갈래로 나뉘었다.
마지막으로 수행한 공통 작업을 Common Ancestor라고 한다.
Common Ancestor 포인트에서 A 브랜치와 C 브랜치는 각각 추가로 더 작업을 수행하였다.
이 두 브랜치가 합쳐지면서 하나의 커밋을 생성한다.
이를 merge commit이라 한다.
(머지 시, 커밋이 수행되는 점이 fast-forward와 다른 점이다.)

## branch 병합 시 충돌해결
같은 파일 내에서 다른 line을 수정했다고 했을 때, merge를 하면 해당 내용이 합쳐진 상태로 병합된다.
하지만 같은 파일 내에서 같은 위치의 내용을 수정했을 때 문제가 된다. (충돌 발생)

~~~bash
git status
~~~
git의 상태를 파악하여 충돌이 일어난 파일을 찾을 수 있다.

~~~bash
function b() {
} 
<<<<<<< HEAD
function a(master) {
=======
function a(exp) {
>>>>>>> exp
}
function c() {
}
~~~
충돌이 발생한 파일을 수정하면 된다.
'<<<<<<< HEAD' 부터 '=======' 사이의 구간이 현재 체크 아웃된 파일의 내용이고 '=======' 부터 '>>>>>>> exp' 사이의 구간이 병합하려는 대상인 exp 브랜치의 코드 내용이다.
두개의 코드를 병합하고 특수기호들을 제거하면 된다.
작업이 끝나면 파일을 저장한다.

~~~bash
git add {충돌된 파일 이름}
~~~
충돌 작업이 끝났다는 것을 깃에게 알려준다.

~~~bash
git commit
~~~
커밋을 하면 병합이 수행된다.

## stash
stash는 감추다, 숨겨주다 라는 뜻을 가지고 있다.
stash란 파일의 변경 내용을 일시적으로 기록해두는 영역이다.
stash를 사용하여 작업 트리와 인덱스 내에서 아직 커밋하지 않는 변경을 일시적으로 저장해 둘 수 있다.
stash에 저장된 변경 내용은 나중에 다시 불러와 원래 브랜치나 다른 브랜치에 커밋할 수 있다.

ex) 이전 브랜치에서 커밋하지 않는 변경 내용을 커밋하거나, stash를 이용해 일시적으로 변경 내용을 다른 곳에 저장하여 충돌을 피하게 할때 사용 됨.
다른 브랜치로 checkout을 해야 하는데 아직 현재 브랜치에서 작업이 끝나지 않은 경우는 커밋을 하기가 애매하다.
이런 경우 stash를 이용하면 작업중이던 파일을 임시로 저장해두고 현재 브랜치의 상태를 마지막 커밋의 상태로 초기화 할 수 있다. 
그 후에 다른 브랜치로 이동하고 작업을 끝낸 후에 작업 중이던 브랜치로 복귀한 후에 이전에 작업하던 내용을 복원할 수 있다. 

~~~bash
// staging에 올라간 파일을 stash한다.
git stash

// stash 이력을 출력한다. (최근에 stash한 파일이 위에 올라간다.)
git stash list

// stash에 올라가 있는 파일을 불러온다. (list의 윗쪽부터 하나씩)
git stash apply

// stash에 올라가 있는 파일을 삭제한다. (list의 윗쪽부터 하나씩)
git stash drop

// stash에 올라가 있는 파일을 불러오며, list에서 삭제한다.
git stash apply; git stash drop;
// 다음과 같이 쓸 수도 있다.
git stash pop
~~~

## SourceTree에 표시되는 커밋 위치에 대해서

- origin/master : 원격 저장소 'origin' 브랜치인 'master'의 위치를 나타내고 있다,
- origin/HEAD : 원격 저장소 'origin'을 복제해 올 때 다운로드 되는 커밋의 위치를 나타내고 있습니다. 일반적으로 'origin/master'와 동일한 위치를 가리킵니다.
- master : 로컬 저장소 브랜치인 'master'의 위치를 나타내고 있습니다.

## branch의 종류

### 메인 브랜치 (Main branch)

'master' 브랜치와 'develop' 브랜치, 이 두 종류의 브랜치를 보통 메인 브랜치로 사용한다.

- master : 'master' 브랜치에서는 배포 가능한 상태만을 관리한다. 커밋할 때에는 태그를 사용하여 배포 번호를 기록한다.
- develop : 'develop' 브랜치는 앞서 설명한 통합 브랜치의 역할을 하며, 평소에는 이 브랜치를 기반으로 개발을 진행한다.

### 피처 브랜치 (Feature branch) 또는 토픽 브랜치 (Topic branch)

피처 브랜치는 토픽 브랜치의 역할을 담당한다.
새로운 기능 개발 및 버그 수정이 필요할 때에 'develop' 브랜치로부터 분기한다.
피처 브랜치에서의 작업은 기본적으로 공유할 필요가 없기 때문에 원격으로는 관리하지 않는다.
개발이 완료되면 'develop' 브랜치로 병합하여 다른 사람들과 공유한다.

### 릴리스 브랜치 (Release branch)

릴리즈 브랜치에서는 버그를 수정하거나 새로운 기능을 포함한 상태로 모든 기능이 정상적으로 동작하는지 확인한다.
릴리즈 브랜치의 이름은 관례적으로 브랜치 이름 앞에 'release-'를 붙인다.
이때, 다음 번 릴리즈를 위한 개발 작업은 'develop' 브랜치에서 계속 진행해 가면 된다.

릴리즈 브랜치에서는 릴리즈를 위한 최종적인 버그 수정 등의 개발을 수행한다.
모든 준비를 마치고 배포 가능한 사애가 되면 'master' 브랜치로 병합시키고, 병합한 커밋에 릴리즈 번호 태그를 추가한다.

릴리즈 브랜치에서 기능을 점검하며 발견한 버그 수정 사항은 'develop' 브랜치에도 적용해 주어야 한다.
그러므로 배포 완료 후 'develop' 브랜치에 대해서도 병합 작업을 수행한다.

### 핫픽스 브랜치 (Hotfix branch)

배포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우, 'master' 브랜치에서 분기하는 브랜치이다.
관례적으로 브랜치 이름 앞에 'hotfix-'를 붙인다.

ex)
'develop' 브랜치에서 개발을 한창 진행하고 있는 도중에 이전에 배포한 소스코드에 아주 큰 버그가 발견 된 경우!
문제가 되는 부분을 빠르게 수정해서 안정적으로 다시 배포해야 한다.
'develop' 브랜치에서 문제가 되는 부분을 수정하여 배포 가능한 버전을 만들기에는 시간도 많이 소요되고 안정성을 보장하기도 어렵다.
그렇기 때문에 바로 배포가 가능한 'master' 브랜치에서 직접 브랜치를 만들어 필요한 부분 만을 수정한 후 다시 'master' 브랜치에 병합하여 이를 배포한다.

이때 만든 핫픽스 브랜치에서의 변경 사항은 'develop' 브랜치에도 병합하여 문제가 되는 부분을 처리해 주어야 한다.

# git의 원리

## branch의 원리 
깃은 head라는 파일을 가지고 있다.
head 파일은 master 파일을 가리키며, master 파일은 최신의 커밋 파일을 가리킨다.
그렇기 때문에 git log를 입력했을 때 내용이 출력될 수 있는 것이다.
~~~
./git/refs/heads/master
~~~

브랜치(exp)를 생성하면 다음과 같이 파일이 생성된다.
~~~
.git/refs/heads/exp
~~~

## reset과 checkout의 원리
reset이란 지정한 커밋 id의 상태로 돌아가기 위한 git 커맨드이며,
해당 브랜치가 가리키고 있는 최신 로그 파일을 커밋 id 상태로 바꾸는 것을 의미한다.
~~~
git reset --hard {커밋 id}
~~~

ORIG_HEAD라는 파일은 기존에 수행한 최신 커밋 id를 가지고 있다. 
그러므로 방금 실행한 reset을 취소하고 원래 커밋으로 돌아가고 싶을 때 커밋 id 대신 ORIG_HEAD를 지정할 수 있다.
~~~
git reset --hard ORIG_HEAD
~~~

## reset으로 알아보는 working copy, index, repository
git reset 옵션에 따라서 리셋되는 범위가 다르다.
해당 내용은 다음과 같다.

|working directory,  working tree,  working copy| index,  staging area,  cache | repository,  history,  tree|
|-----|-----|-----|
|||git reset --soft |
||git reset --mixed|git reset --mixed|
|git reset --hard|git reset --hard|git reset --hard|

~~~
git reset --soft
git reset --mixed
git reset --hard
~~~

## 3 way merge
| case 분류 |Me (현재 브랜치) | Base | Other(다른 사람의 브랜치) | 2 way merge | 3 way merge |
|---|---|---|---|---|---|
|ohter만 내용이 다른 경우 | A | A |   |  conflict 발생시킴 |
|모두 내용이 같은 경우 | B | B | B | B | B |  |
|모두 내용이 다른 경우 | 1 | C | 2 | conflict 발생시킴 | conflict 발생시킴 |
|me만 내용이 다른 경우 |   | D | D | conflict 발생시킴 |  |

* 2 way merge
- 병합하고자 하는 두 브랜치를 비교하여 병합하는 것 (Me, Other 브랜치)
- 내용이 다른면 conflict를 발생시켜 내용을 조정하고자 함.

* 3 way merge
- base를 기준으로 두 브랜치를 비교하여 병합하는 것
- 내용이 다르다면 base로부터 수정한 것으로 이해해 수정된 내용을 병합 시 반영한다. 

# 원격 저장소
로컬 저장소와 대비되는 개념

## 원격저장소의 기초
~~~
// 원격저장소 생성
git init --bare remote

// 로컬 저장소에 원격 저장소를 add한다.
git remote add origin /home/git/git/remote

// 로컬저장소와 원격저장소를 연결
git push —set-upstream origin master
~~~
bare 옵션은 작업은 할 수 없고 저장소로서의 역할만 수행한다.
수정이 불가능하며 원격 저장소를 만들 때 사용하는 옵션이다.

원격 저장소 추가 시, 
origin 뒤에 저렇게 주소를 쓰면, origin을 저 주소의 별명으로 쓰겠음을 나타낸다.

현재 master브랜치를 push할 때 origin의 master브랜치로 푸쉬한다.

## Github

### 원격 저장소를 지역 저장소로 복제 (Github)
~~~
// git의 소스코드를 지역저장소로 가져오기
git clone https://github.com/git/git.git {저장하고자 하는 디렉토리 명}

// 로그를 거꾸로 출력하기
git log --reverse

// git의 특정 커밋으로 체크아웃하기
git checkout {커밋 ID : e83c5163316f89bfbde7d9ab23ca2e25604af290}
~~~

Fork : 해당 프로젝트를 가져와서 내 저장소에 그대로 가져와서 소스코드 수정 등 라이선스에 맞춰서 마음껏 사용할 수 있는 것 (프로젝트 복제)

github의 git 프로젝트의 첫 로그를 찍어보니 Linux의 창시자 'Linus Torvalds'가 첫 커밋을 했음을 확인했다. (리눅스 버전관리가 어려워 깃을 직접 만들게 되었다고!)
그의 첫 커밋 메세지는...

`Initial revision of "git", the information manager from hell`

### 원격 저장소 만들기(Github)
~~~
// 로컬 저장소에 원격 저장소 연결하기
git remote add origin https://github.com/ijsong/git-flow.git

// 현재 연결된 원격 저장소가 무엇인지 알려줌
git remote

// 원격저장소 보기
git remote -v

// 원격 저장소 삭제하기
git remote remove origin

// 앞으로 현재 브랜치를 원격저장소 origin의 master에 동기화하겠다
git push -u origin master

// 현재 디렉토리로 해당 원격저장소를 복제(클론)함.
git clone https://github.com/ijaysong/git-flow.git .
~~~

1)
로컬에 원격 저장소를 연결하는 커맨드를 해석해보자면, 
git : 내 로컬 저장소 깃에
remote : 원격저장소를
add : 더하겠다, 연결하겠다
origin : 원격 저장소 path의 별칭 (원격 저장소 path가 너무 기니까 이름을 지정해준 것임)
https://github.com/ejsong/git-flow.git : 해당 url의 원격저장소를

별칭으로 다른 것을 지정할 수도 있지만, 
기본 브랜치가 master인것 처럼 기본 원격 브랜치는 origin이다.

2)
현재 브랜치를 원격저장소 origin의 master에 동기화하는 커맨드를 해석해보자면,
git : 로컬로부터 
push : 푸쉬하겠다. 동기화하겠다.
-u : 푸쉬하면 origin의 master 브랜치에 자동으로 푸쉬도록 자동화 하겠다.
origin : origin이라는 원격저장소의
master : origin 원격저장소의 master 브랜치에

동기화 했기 때문에 다음부터는 `git push` 만 해도 됨.

### 원격 저장소와 지역 저장소의 동기화 방법 (Github)
~~~
원격 저장소를 두개로 복제
git clone https://www.github.com/ijaysong/git-flow.git git_home
git clone https://www.github.com/ijaysong/git-flow.git git_office

// 이전 커밋의 메세지 변경 
git commit --amend 

// 내려받아 최신화
git pull
~~~

동일한 원격 저장소를 두대의 컴퓨터로 작업한다고 생각해보자. (home, office)
다음과 같은 방법으로 무리 없이 소스 코드를 공유하며 개발할 수 있다.

1) git_home에서 작업을 하고 commit -> push 한다.
2) git_office에서 작업 내용을 pull 받는다.
3) git_office에서 새롭게 작업한 내용을 commit -> push 한다.
4) git_home에서 작업 내용을 pull 받는다.
5) 위의 내용 반복

### 로그인 없이 원격 저장소 이용하기 (Github)
SSH (Secure Shell)을 이용해 원격 저장소에 접근하는 방법에 대한 것이다.

git에서 Web Url로 리포지토리를 클론해오면 매번 로그인 정보를 입력해야 하는 불편함이 있다. (Clone with HTTPS)
ssh 통신 방법을 이용하면 할 때마다 로그인을 하지 않아도 되는 장점이 있다. (Clone with SSH)

~~~
// ssh 키 생성
ssh -keygen
~~~

ssh 키를 생성하면 다음 두개의 파일이 생성된다.
id_rsa : private key
id_rsa.pub : public key

id_rsa(private key)는 내 컴퓨터에 저장이 되고, 
id_rsa.pub(public key)는 접속하고자 하는 리모트 컴퓨터에 넣어주면 됨.
그러면 로컬 컴퓨터가 퍼블릭키를 가지고 있는 컴퓨터에 자동 로그인 한다.

프라이빗 키는 외부에 절대 노출되면 안된다!

그렇다면 어떻게 퍼블릭 키를 리모트 컴퓨터에 저장할 것인가? github에서 서비스를 제공하고 있기 때문에 방법은 쉬움.
깃헙 settings 메뉴 -> SSH and GPG keys : 공개키를 저장할 수 있음
New SSH key 클릭 -> title:지역저장소의 이름 입력, key : 카피한 내용을 붙여넣기함

id_rsa.pub(public key)와 id_rsa(private)는 한 쌍이다.
id_rsa(private)를 가지고 있는 사람은 id_rsa.pub(public key)가 있는 원격 저장소에 접속할 수 있도록 되어 있기 때문에 로그인이 없이 접속할 수 있는 것이다.

## 원격 저장소의 원리
원격저장소를 연결시키면 config 파일 내부에서 변경이 발생한다.
원격 저장소에 대한 내용과 브랜치에 연결된 원격 저장소에 대한 내용이 추가된다.

upstream branch : 직역하자면 상류 브랜치, 로컬 입장에서 원격저장소를 뜻한다.
~~~
git push --set-upstream origin master
~~~
해당 커맨드를 해석해보자면
git push : 푸쉬를 할 것이다.
--set-upstream : upstream을 셋팅하는 (원격저장소를 셋팅하는)
origin : origin에 해당되는
master : master 브랜치를

## 태그(tag)

태그란 커밋을 참조하기 쉽도록 이름을 붙이는 것을 말한다.
한번 붙인 태그는 브랜치처럼 위치가 이동하지 않고 고정된다.
특정 커밋으로 돌아가고 싶다거나 할때 해당 지점을 표시할 때에도 사용된다.
git에서는 이하 두가지의 태그를 사용할 수 있다.

- 일반 태그(Lightweight tag)

* 이름만 붙일 수 있다.

- 주석 태그(Annotated tag)

* 더 많은 정보를 담는 태그이다.
* 이름을 붙일 수 있다.
* 태그에 대한 설명도 포함할 수 있다.
* 서명도 넣을 수 있다.
* 해당 태그를 만든 사람의 이름, 이메일, 태그를 만든 날짜 정보도 포함시킬 수 있다.

### 태그 추가하기

~~~
// 태그 추가
git tag {태그 이름}

// 현재 'HEAD'가 가리키고 있는 커밋에 'apple'이라는 태그 추가
git tag apple

// 태그 목록 보기
git tag

// 태그 정보를 포함한 이력 확인
git log -decorate

// 태그 원격저장소로 푸쉬하기
git push --tags
~~~

### 주석 달린 태그를 추가하기

~~~
// 주석이 달린 태그 추가
git tag -a {태그명}

// 현재 'HEAD'가 가리키고 있는 커밋에 'banana'라는 주석이 달린 태그를 추가
git tag -am "first commit" apple
git tag -am "누구나 쉽게 이해할 수 있는 Git 입문" banana

// 태그 목록과 주석 목록 확인
git tag -n
~~~

태그 목록과 주석 목록 확인을 위해 `git tag -n`을 실행하면 다음과 같은 결과가 표시된다.
~~~
OUTPUT:
apple first commit
banana 누구나 쉽게 이해할 수 있는 Git 입문
~~~

### 태그 삭제하기
~~~
// 태그 삭제
git tag -d {태그명}
~~~

## pull과 fetch의 차이점

~~~
// pull 받기
git pull

// fetch 하기
git fetch

// 로컬 브랜치의 HEAD와 원격저장소의 master의 내용을 비교한다
git diff HEAD origin/master

// 원격저장소의 내용을 로컬에 병합한다
git merge origin/master
~~~

- pull
  원격 저장소의 내용을 가져와 로컬의 브랜치와 병합한다.

- fetch
  원격저장소의 내용을 가져오기만 하고, 로컬과 병합하지 않는다.
  원격저장소와 로컬의 상황을 각각 분리하여 알 수 있다.
  그러므로 origin/master(원격저장소의 master 브랜치)가 로컬 master를 앞서는 현상이 나타난다.
  원격저장소로부터 필요한 파일을 다운 받고 끝나기 때문에 꼭 merge를 해주어야 한다.
  신중하게 병합하고자 할 때 사용할 수 있다.

fetch 후 merge 를 수행하면, pull 명령을 실행했을 때와 같은 이력이 만들어진다.
사실 pull 이라는 것은 내부적으로 보면 fetch + merge 이다.

## 커밋 변경하기

### 이전에 작성한 커밋 수정하기

누락된 파일을 새로 추가하거나,
기존의 파일을 업데이트 하거나,
이전 커밋의 메세지를 변경하고 싶을 때 사용한다.

~~~
// 이전에 작성한 커밋 수정하기
git commit --amend
~~~

### 이전에 작성한 커밋 지우기

특정 커밋의 상태로 돌아갈 수 있다.
예를 들어,
A -> B(지우고 싶은 커밋) -> C -> D(B를 지운 커밋)
라는 흐름의 커밋이 있다고 해보자.
B를 지워 커밋 A 상태로 돌아갈 수 있는 새로운 커밋 D를 만들 수 있다.

~~~
// master/HEAD의 커밋을 취소할 때
git revert HEAD

// 특정 커밋을 되돌릴 때
git revert {커밋 id}
~~~

### 커밋을 버리고 특정 버전으로 다시 되돌아가기

reset 명령어를 사용하면 더 이상 필요 없어진 커밋을 버릴 수 있다.
명령어 실행 시 어떤 모드로 실행할지 지정하여, HEAD 위치와 인덱스, 작업 트리 내용을 함께 되돌릴지 여부를 선택할 수 있다.
기본적으로 mixed가 지정되며 soft, hard 중에서 선택할 수 있다.

- soft : 커밋만 되돌리고 싶을 때
- mixed : 변경한 인덱스의 상태를 원래대로 되돌리고 싶을 때
- hard : 최근의 커밋을 완전히 버리고 이전 상태로 되돌리고 싶을 때

| 모드 명 | HEAD의 위치 | 인덱스    | 작업트리  |
| ------- | ----------- | --------- | --------- |
| soft    | 변경함      | 변경 안함 | 변경 안함 |
| mixed   | 변경함      | 변경함    | 변경 안함 |
| hard    | 변경함      | 변경함    | 변경함    |

~~~
// HEAD 커밋 되돌리기
git reset HEAD
~~~

reset 전의 커밋은 `ORIG_HEAD`라는 이름으로 참조할 수 있다.
실수로 reset을 한 경우에는 ORIG_HEAD를 reset하여 reset 실행 전 상태로 되돌릴 수 있다.

~~~
git reset --hard ORIG_HEAD
~~~

### 다른 브랜치로부터 특정 커밋을 가져와서 내 브랜치에 넣기

cherry-pick을 이용하면 다른 브랜치에서 지정한 커밋을 복사하여 현재 브랜치로 가져올 수 있다.
특정 브랜치에 잘못 추가한 커밋을 올바른 브랜치로 옮기려 하거나,
다른 브랜치의 커밋을 현재 브랜치에도 추가하고 싶을 때 사용할 수 있다.
예를 들어,
master 브랜치 : A -> B
tmp 브랜치 : C -> D

master 브랜치에 tmp 브랜치의 커밋 C를 가져오고 싶다고 해보자.
그렇다면 먼저 master로 체크아웃을 하고
커밋을 꺼내 master에 추가한다.

~~~
// master로 체크아웃
git checkout master

// 옮기고 싶은 커밋을 체리픽
git cherry-pick {커밋 id}
~~~

### 커밋 이력 편집하기

rebase 명령어에 i 옵션을 지정하면 커밋을 다시 쓰거나 다른 커밋과 바꿔넣을 수 있으며,
특정 위치의 커밋을 삭제하거나 여러 커밋을 하나로 통합하는 작업을 할 수 있다.
push 하기 전에 이전 커밋 내용을 정리 하고자 할 때나
그룹으로 묶을 수 있는 커밋들을 알기 쉽게 하나로 통합하려고 할 때나
이전 커밋에 누락된 파일들을 나중에 추가하고자 할 때 사용할 수 있다.

예를 들어 다음과 같은 흐름이 가능하다.

#### rebase -i로 커밋 모두 통합하기

다음과 같은 흐름으로 커밋을 통합해본다고 하자.
A -> B -> C -> D
A -> B -> C+D

```
// 커밋 통합하기
git rebase -i HEAD--
git rebase -i {커밋 id}
```

위에 있는 커맨드를 실행하면 텍스트 에디터가 열리고, HEAD에서 HEAD~~까지 커밋이 다음과 같이 표시된다.

```
pick 9a54fd4 C
pick 0d4a808 D

# Rebase 326fc9f..0d4a808 onto d286baa
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```

두번째 줄의 pick 문자를 `squash`로 변경하고 저장 종료한다.
이를 통해 두개의 커밋이 하나의 커밋으로 통합된다.
