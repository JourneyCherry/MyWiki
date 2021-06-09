상위문서 : [메인페이지](./README.md)<br>

<br>

Blender Wiki
=============

## 목차
[1. Unity로 Export시 유의점](#1-unity로-export시-유의점)<br>
[2. .fbx 파일 Export시 유의점](#2-fbx-파일-export시-유의점)<br>

<br><br>

* * *
### [1.](#목차) Unity로 Export시 유의점

Blender와 Unity의 좌표계가 다르기 때문에 이를 고려해야 한다.(자세한 내용은 [일반 그래픽스 문서](./GeneralGraphics.md) 참고)
* Blender는 Z축이 위아래
* Unity는 Y축이 위아래

따라서 .fbx로 추출 시, 다음 두가지 방법 중 하나를 선택해서 적용해야 한다.

* 미리 X축을 기준으로 90˚ 회전시킨 뒤 Export하기.
    1. 오브젝트를 X축 기준으로 -90˚ 회전
    2. Apply Rotation
    3. 다시 X축 기준으로 90˚ 회전
    4. Export
* Export할 때, Apply Transform 항목을 체크한 뒤, Export
    * 해당 방법은 Experimental Method이므로 주의가 필요하다.


<br><br>
- - -

### [2.](#목차) .fbx 파일 Export시 유의점

FBX 파일은 Material Node 中 절차적 노드(Procedural Node)는 지원하지 않는다.<br>
```예 : MixRGB```

따라서 FBX 파일로 Export 시, 절차 노드를 사용하고 있다면 별도의 Texture Bake 작업을 통하여 Shader만 사용할 수 있도록 해야 한다.

**작업 방법**

1. 오브젝트의 UV Map을 먼저 정렬한다.
2. Shader Editor를 열고 Image Texture를 생성한다.
3. 생성된 Image Texture에 New를 누르고 이름, 크기를 고른다.(크기는 적절히 크게 한다.)
4. Image Editor를 열고 ```3.```에서 생성한 Image를 불러온다.
5. Shader Editor에서 ```2.```에서 생성한 Image Texture를 선택하고 우측 메뉴의 Render Properties로 들어간다.
6. Render Engine을 Cycle로 변경.(Device는 편한대로 설정한다.)
7. Sampling 항목에서 Render 값을 적절히 높인다.(약 32)
8. Bake 항목에서 Bake Type을 Diffuse로 설정하고, Bake-Influence 항목의 Contributions를 Color만 선택하고 나머지는 선택해제 한다.
9. Bake 버튼을 누르고 렌더링이 완료될때 까지 기다린다.
10. ```2. ~ 9.```까지 동일하게 진행하되, Image를 생성할 때 Alpha를 체크 해제 하고, Bake Type을 Normal로 변경하여 Normal Map을 렌더링 한다.
11. Image Editor에서 ```9.```와 ```10.```에서 만든 이미지를 별도의 파일로 저장한다.
12. Shader Editor에서 Principled BSDF 셰이더와 Material Output을 새로 생성하고, 방금 Bake한 Image들을 Principled BSDF 셰이더를 통해 Material Output에 연결한다.
13. 현재 오브젝트를 백업해둔 뒤, 기존에 있던 Node들을 모두 지우고 FBX 파일로 Export 한다.(Export할 때, Texture파일의 경로를 어떻게 설정할것인가를 잘 봐야 한다.)

출처 : https://www.youtube.com/watch?v=x4mySebugl0