상위문서 : [메인페이지](./README.md)<br>

<br>

Unity Wiki
=============

목차
[1. Component의 Life-Cycle](#1-component의-life-cycle)

<br><br>

* * *
### **1. Component의 Life-Cycle**

|Name|Called Only Once|Description|
|:---:|:---:|---|
|Awake|O|Component가 속한 Object가 가장 처음 Enable되었을 때 호출된다.<br>AddComponent로 추가되더라도 Object가 active상태가 아니면 호출되지 않는다.<br>Enable된 Object에 AddComponent로 추가될 때에는 호출된다.|
|OnEnable|X|Component의 상태가 Disable에서 Enable로 바뀌었을 때 호출된다.<br>Object와 Component 모두 Enable이어야 호출된다.|
|Start|O|Component가  Object가 그려지는 가장 첫 Update바로 직전에 호출된다.|
|FixedUpdate|X|고정된 시간차로 불려지는 Update.<br>해당 시간차는 Edit -> Project Settings -> Time -> Fixed Timestep 항목을 따른다.<br>*Update*보다 빨리 호출될지 늦게 호출될지는 랜덤하다.<br>주로 물리 연산에 사용된다.|
|Update|X|화면에 그려지는 프레임마다 호출되는 Update.<br>Fps 값은 Application.targetFrameRate 값으로 조절한다.(Default는 -1)|
|LateUpdate|X|모든 Object의 Update가 호출된 뒤 호출되는 Update.<br>주로 3인칭 카메라 조절에 사용한다.|
|OnDisable|X|Component의 상태가 Enable에서 Disable로 바뀌었을 때.<br>Object와 Component 둘 중 하나라도 Disable되면 호출된다.|
|OnDestroy|O|Object나 Component가 제거될 때 호출된다.<br>호출 시점은 해당 Object의 모든 Update가 끝난 뒤이다.<br>즉, Object.Destroy()가 호출된 시점에서 가장 빠른 Update가 끝나고 OnDestroy가 호출된 뒤,<br>Object가 삭제되므로 Object.Destroy()를 호출한 시점에서는 Object는 아직 살아있게 된다.|