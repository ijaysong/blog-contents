## 1. Git 원격 리포지토리를 만든다.

+버튼 누르고 New repository 선택  
Repository name 지정 후, Create Repository 버튼 클릭 -> Git 리포지토리가 생성된다.


## 2.Git 원격 리포지토리와 로컬 리포지토리를 연결한다.

Window OS라면 CMD창을, Mac OS라면 Terminal 창을 연다.  
연결하고자 하는 로컬 workspace로 이동한다. ex) cd /move/to/your/worksapce  
다음과 같은 커맨드를 작성한다.

* git init : 내 workspace 안에 .git 폴더가 없다면, git init을 통해서 생성한다.
* git remote add origin [repository주소] : 로컬 리포지토리에 Git 원격 리포지토리를 origin이라는 이름으로 추가한다.

깃헙에서 리포지토리를 생성하면 아래와 같이 커맨드라인이 표시되므로 참고할 것


## 3. SourceTree와 Git 리포지토리 연결하기

로컬 > 새로 만들기 > 로컬 저장소 추가하기에서 로컬 리포지토리를 추가한다.  
SourceTree를 통해 깃에 Commit 할 수 있게 된다.

