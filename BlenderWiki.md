상위문서 : [메인페이지](./README.md)<br>

<br>

Blender Wiki
=============

## 목차
[1. Unity로 Export시 유의점](#1-unity로-export시-유의점)

<br><br>

* * *
### [1.](#목차) Unity로 Export시 유의점

Blender와 Unity의 좌표계가 다르기 때문에 이를 고려해야 한다.
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