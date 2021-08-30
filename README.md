# dockerfile-example

도커는 명령어, Bash를 통해서 설정이 가능하지만
동시에 ```dockerfile```을 통해서 특정 이미지를 다운하고 설정을 완료해서 이미지화 할 수 있다.

이곳은 그 ```dockerfile```의 예시 파일들을 업로드를 하기 위해서 만든 레포이다.

# Dockerfile Command

### 설명

```docker file```에서는 여러가지 명령어 옵션이 존재한다.
형식은 
<옵션> <명령어>
위와 같은 간단한 형식을 가지고 있다.
이때 특정 명령어는 두가지 방법을 통해서 사용이 가능하다.

첫번째는 ```exec``` 방식
``` 
RUN ["/bin/bash", "-c", "echo hello > test.html"] 
```
두번째는 ```Shell``` 방식
``` 
RUN apt-get install update 
```

두가지 방법이 모두 사용이 가능한 옵션의 체크 표시를 해두겠다.

-------

### 0. FROM
이게 없으면 작동이 되지 않는다.
그냥 기본 베이스가 되는 ```Docker Iamage```가 뭔지 선언하는 부분이다.

```
FROM ubuntu:latest
```
위 와 같이 Docker처럼 선언하면 된다.

--------

### 1. RUN

- [x] exec, shell
RUN은 명령어를 실행할 수 있게 해주는 옵션이다.
패키지를 ```install```하거나 ```echo```를 통해서 상태를 보여주는 등의 셋팅을 할 수도 있다.

```
RUN ["/bin/bash", "-c", "echo hello > test.html"]
```

```
RUN apt-get install update
RUN apt-get install httpd -y
```

------

### 2. EXPOSE
- [x] exec, shell
```EXPOSE```는 포트와 호스트를 연결할 때 사용이 된다.
즉 포트포워딩이라고 생각하면된다.

```
EXPOSE 80
EXPOSE 3306
```


``` 
EXPOSE 80 3306 
```
위와 같이 한줄로 사용할 수도 있다.

----------

### 3. ADD

```ADD```는 현재 자신의 PC혹은 노트북에 있는 File을 컨테이너 상에 원하는 디렉토리로 이동시켜주는 것 이다.
그말은 즉, 굳이 컨테이너로 접속해서 파일을 생성할 필요없이 호스트상에 있는 File을 업로드할 수 있다는 것 이다.

```
ADD index.html /usr/local/apache2/htdocs/
```
----------


### 4. COPY

```COPY```는 바로위에서 설명한 ADD와 비슷한 역할을 하지만
단순히 복사기능만을 가지고 있고 ADD는 원격의 파일을 다운로드 할 수 있다는 장점이 있다.

``` 
COPY index.html /usr/local/apache2/htdocs/
```
-----------

### 5. VOLUME

```VOLUME```은 자신의 저장공간과 마운트를 하는 옵션이다.
간단히 말해서 PC에서 작업한 내용을 일일히 복사해줄 필요없이 마운트를 해두면 HOST의 특정 경로에 있는 File을 가지고서
작동을 한다고 생각하면 된다.

```
VOLUME /usr/local/apache2/htdocs/
```

해당 방식으로 사용을 할 경우 경로는 ```/var/lib/docker/volumes/```에 저장이 된다.

---------------

### 6. CMD
- [x] exec, shell
단 한번만 사용할 수 있으며 컨테이너 실행 시 매번 해당 명령을 실행을 한다.
후술할 ```ENTRYPOINT```와 기능은 비슷하다.

``` 
CMD apachectl -D FOREGROUND
```
```
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]
```
--------------


### 7. ENTRYPOINT

기존의 ```CMD``` 명령어와 같은 역할을 맡고있고
차이점이 있다면 ```CMD```는 ```docker run```에서 수정이 가능하지만 ```ENTRYPOINT```는 수정이 불가능하다.
즉 유동적이지는 않다는 말이고 꼭 최초에 실행해야만 하는 명령어가 있을때 주로 사용된다.

```
ENTRYPOINT python3 /newpy/pythonfile/main.py
```

------------

### 8. WORKDIR

이 컨테이너가 어디서 일을 수행할지 정해주는 것 이다.
대표적으로 ```apache```의 경우 ```/var/www/html/```으로 해주면 편하다.

```
WORKDIR /var/www/html/
```

----------
# 출처

https://blog.d0ngd0nge.xyz/docker-dockerfile-write/

해당 사이트를 참고 하였습니다. 
작성자분께 좋은 정보 알려주셔서 감사하다는 말 올립니다.





