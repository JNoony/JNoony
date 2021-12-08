**여기는 온갖 연습하는 Git**

<<<<<<< HEAD
**** 여러브랜치 pull/push연습****
=======
>>>>>>> 55ceb8a5fd3e68ea01af0926453e8506d5bd679f
--rebase 사용
1. 먼저 master 브랜치로 넘어오기
git branch
git checkout master
git pull upstream master

2. 최신화 할 브랜치로 넘어가서 rebase사용하기
git checkout 브랜치명
git rebase master
git checkout master
git merge 브랜치명 --ff

* rebase사용에서 에러 발생
````
error: cannot rebase: You have unstaged changes.
error: Please commit or stash them.
````


* git status로 확인해보니 아래와 같은 에러발생
````
On branch branch01
Your branch is up to date with 'origin/branch01'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
````

* git commit -a "브랜치 최신화용" 을 실행햇는데 새로운 에러 발생
````
Another git process seems to be running in this repository, e.g.
an editor opened by 'git commit'. Please make sure all processes
are terminated then try again. If it still fails, a git process
may have crashed in this repository earlier:
remove the file manually to continue.
````
.git폴더 안에 있는 index.lock파일을 지워주면 된다.

* git stash
* git rebase main
* git pull
* git stash apply

근데 이사이에 .. 내가 작업한게 다 날라가고.. 작업하기 전 github에 올라가 있는 코드랑 만 병합되서..
다시 복원

````
git reflog       ---> git 작업한 리스트 확인
git reset --hard 깃트리아이디
`````

* git pull
* git stash apply

하니까 작업한거까지 복원되었고 합쳐졌다 생각했는데... 아니였다..

다시 해보자...


##정리해보면

$ git checkout [base브랜치]      -> 항상 최신화 되어있는 브랜치인지 확인 및 넘어가기
$ git fetch                -> FETCH_HEAD에 담기
$ git pull origin [base브랜치]   -> head에 담을 브랜치명 명시

새브랜치로 넘어와서

$ git checkout [브랜치]                  -> 최신화할 브랜치로 넘어가기 
$ git stash                              -> 새브랜치 작업내용 저장
$ git commit -am "stash 목록저장용"
$ git reset --hard origin/[base브랜치]   -> fetch로 받은 내용으로 돌리기
$ git stash apply                        -> apply로 머지할 내용 확인할것

