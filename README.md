# MyWiki
내맘대로 하는 위키.

목록   
[1. Git](./GitWiki.md)<br>
[2. VS Code](./VSCodeWiki.md)<br>
[3. Unity](./UnityWiki.md)<br>
[4. Blender](./BlenderWiki.md)<br>
[5. 그래픽 일반](./GeneralGraphics.md)<br>

<br><br>

### 1. Jekyll 설치하는 방법

1. Ruby 설치
    * Windows : [윈도우 인스톨러](https://rubyinstaller.org/downloads/) 다운로드 후 설치(```ridk install``` 절차 수행 필요)
2. jekyll과 bundler 설치
    ```
    gem install jekyll bundler
    ```
3. 설치 여부 확인
    ```
    jekyll -v
    ```

### 2. Jekyll 환경 구성

1. Console에서 대상 폴더로 이동
2. 새로운 사이트 생성
    ```
    jekyll new BlogName
    ```
3. 생성된 디렉토리로 이동
    ```
    cd BlogName
    ```
4. 사이트 빌드 및 실행
    ```
    bundle exec jekyll serve
    ```
    * 실행 시, ```'require': cannot load such file -- webrick (LoadError)```와 함께 실행되지 않는다면 webrick도 설치
        ```
        bundle add webrick
        ```
        이러는 이유는 ruby 3.0.0부터 gem에서 본래 기본 포함이었던 webrick이 빠졌기 때문.
        <h6> 출처 : https://junho85.pe.kr/1850 </h6>
5. http://localhost:4000 에 접속