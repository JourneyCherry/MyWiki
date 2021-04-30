Git Wiki
=============

>**<h2>작성규칙</h2>**
>   + GUI와 CUI 둘다 가능한 기능은 둘다 명시를 해준다.   
>   + CUI로 할 경우, 기본적으로 해당 디렉토리에서 진행됨을 전제로 하며, git bash로 실행하는 것을 전제로 한다.   

<br>

목차   
[1. Visual Studio Code에서 Github와 연동하는 법](#1-visual-studio-code에서-github와-연동하는-법)   
[2. Unity에서 Github와 연동하는 법](#2-unity에서-github와-연동하는-법)   
[3. .gitignore 적용하기](#3-gitignore-적용하기)   
[4. 자동으로 Issue Closing 시키기](#4-자동으로-issue-closing-시키기)   

<br><br>
- - -

### 1. Visual Studio Code에서 Github와 연동하는 법

1. 깃(https://www.git-scm.com/downloads) 설치 후, 로컬 repository 생성
2. CHANGES 항목에 있는 내용 Commit(Changes항목에서 + 아이콘 클릭하여 Staged Changes에 추가 후,   
   상단의 +모양 아이콘 클릭하여 Commit. 커밋 메모 남기기 가능)
4. 터미널에서 다음 명령어 입력(...는 github의 repository 링크 주소.)
>    
    git remote add origin ...
    git pull origin master --allow-unrelated-histories
>fatal: couldn't find remote ref master 가 뜰 수 있으나 무시하면 됨.
    
    
4. 로그인 한 뒤(로그인 창이 알아서 뜬다.), 다음 명령어로 push 하기
>
    git push -u origin master
5. 완료

출처 : https://webnautes.tistory.com/1422

<br><br>
* * *

### 2. Unity에서 Github와 연동하는 법

1. Github Desktop(https://desktop.github.com/) 설치 후, 로컬 repository 생성(open local repository -> create new local repository메뉴 누르기)
2. 자동 commit 되어 있으므로 git bash 열어서 해당 디렉토리로 간 뒤, 다음 명령어 입력([위](#1-visual-studio-code에서-github와-연동하는-법)와 같다.)
>    
    git remote add origin ...
    git pull origin master --allow-unrelated-histories
    git push -u origin master
    
3. 완료.
>
    참고 : 이 이후로 기타 repository는 Github Desktop으로 관리하는게 좋다.(Visual Studio는 자체 repo 관리 기능이 있으니 제외)

### 3. .gitignore 적용하기
<h6> 이미 Commit 된 파일을 .gitignore에 추가하였으나 적용되지 않을 경우 사용.</h6>

1. .gitignore 파일에 적용할 파일 작성
2. 다음 명령어 수행
>
    git rm -r --cached .
    git add .
    git commit -m "Apply .gitignore"
    git push
>
3. 완료

출처 : https://cjh5414.github.io/gitignore-update/

<br><br>
* * *

### 4. 자동으로 Issue Closing 시키기

<br>

Github에서는 Branch Merge 시, Description에 Issue를 특정 단어와 함께 언급하면 자동으로 Issue를 닫아준다.
<h6>* 단, master branch에 바로 commit을 하는 경우는 제외한다. 그 경우, Issue페이지에서 해당 commit에서 언급이 있었다라고만 하고 closing은 되지 않는다.</h6>

<br>

> <br>
>
>+ 로컬에서 먼저 Branch를 만드는 경우<br>
>
>    1. 로컬에서 Branch를 생성한 뒤, 해당 branch로 이동한다.
>
>            git branch NewBranchName master
>            git checkout NewBranchName
>        또는
>
>            git checkout -b NewBranchName
>
>    2. Remote Repository에 적절히 commit을 한 뒤
>
>           git checkout NewBranchName
>           git commit
>
>    3. branch를 push 한다
>
>            git push --set-upstream origin NewBranchName
>
>    4. 웹사이트에 접속하여 pull request를 생성한다.(Github Desktop에서 create pull request(Ctrl + R)을 해도 웹페이지가 뜬다.)
>
>    5. 웹사이트에서 Merge를 진행한 뒤, 원격지에서 branch가 삭제되면, local에서도 해당 branch를 삭제한다.(이부분은 확인 필요)
>
><br>

<br>

><br>
>
>+ 원격지에서 먼저 Branch를 생성할 경우(보통은 이러지 않는다.)
>
>    1. 원격지에서 branch를 생성한다.(웹에서)
>    2. 원격지 branch를 확인한 뒤(-r은 원격지 branch만, -a는 원격지/로컬 모든 branch)
>            
>            git branch -r
>
>    3. 원격지 branch를 생성한다.(로컬에도 생성되는지는 확인 필요)
>
>            git checkout -t origin/NewBrandName
>
>    4. 이후, 일반적인 push를 하고,
>
>            git push origin NewBranchName
>
>    5. 웹사이트에서 접속하여 pull request를 생성한다.(Github Desktop에서 create pull request(Ctrl + R)을 해도 웹페이지가 뜬다.)
>
>    6. 웹사이트에서 Merge를 진행한 뒤, 원격지에서 branch가 삭제되면, local에서도 해당 branch를 삭제한다.
>
><br>

<br>

Branch 內의 commit message나 pull request의 description에 해당 Issue(#~~~)가 종료 관련 키워드와 함께 포함되어 있으면<br>
Merge를 할 때, 자동으로 해당 Issue를 Closing을 한다.

<br>

><br>
>
>+ 종료 키워드
>
>        close
>        closes
>        closed
>        fix
>        fixes
>        fixed
>        resolve
>        resolves
>        resolved
>  
><br>

<br><br>
* * *