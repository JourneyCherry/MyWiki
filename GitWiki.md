Git Wiki
=============

목차   
[1. Visual Studio Code에서 Github와 연동하는 법](#1-visual-studio-code에서-github와-연동하는-법)   
[2. Unity에서 Github와 연동하는 법](#2-unity에서-github와-연동하는-법)   
[3. .gitignore 적용하기](#3-.gitignore-적용하기)   

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
* * *
