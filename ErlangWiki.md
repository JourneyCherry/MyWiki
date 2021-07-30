상위문서 : [메인페이지](./README.md)<br>

<br>

# Erlang Wiki
==============

## 목차

[1. OTP 사용 시 주의점](#1. OTP 사용 시 주의점)<br>
  [1. OTP 내에서 다른 Application 중단 시키기](#OTP 내에서 다른 Application 중단 시키기)<br>
  

* * *

### [1.](#목차) OTP 사용 시 주의점

##### [1.](#목차) OTP 내에서 다른 Application 중단 시키기

일반적으로 의존성에 의해 사용되는 OTP들은 종료를 하지 않는다. 대표적인 경우가 ```Mnesia```인데 보통  OTP를 종료하기 위해 ```init:stop/0```을 호출하면 Application Controller가 알아서 차례대로 종료를 시키므로 굳이 일부러 ```gen_server:terminate/2```에서 ```mnesia:stop/0```을 호출할 필요는 없다. 그렇게 호출하면 Application Controller가 기존의 Server를 종료시키느라 바빠서 Mnesia를 종료시키지 못해 Deadlock에 빠지게 된다.<br>
만약 굳이 ```gen_server:terminate/2```에서 ```mnesia:stop/0```을 호출하고 싶다면 비동기적으로 처리하는 것이 좋다. 대표적인 방법으론 ```timer:apply_after/3```을 사용하여 일정시간 이후(즉, 기존 Application이 종료 된 이후)에 ```mnesia:stop/0```을 호출하도록 하는 것이며, 비동기적으로 처리되므로 Application Controller가 Deadlock에 빠지는 경우를 벗어나게 된다. Child Process를 호출하는 것은 좋지 않은데, 자식 Process 또한 부모 Process가 죽으면 같이 죽기 때문에 ```mnesia:stop/0```을 수행하지 못할 수 있기 때문이다.<br>
마찬가지 이유로 Application 간 동기적(Synchronously) 상호 호출(```gen_server:call/2```)도 Deadlock을 부를 수 있다.
