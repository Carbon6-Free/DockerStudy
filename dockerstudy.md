# 먼저 docker 설치

맥북 m칩 사용중이면 apple silicon으로 다운로드
https://docs.docker.com/desktop/install/mac-install/

# 3.
이미지를 실행하는 것 - 컨데이너
이미지도 여러개의 컨테이너 가질 수 있음
도커에서 이미지를 받는 것 - pull  
https://docs.docker.com/reference/cli/docker/image/pull/ 
이미지를 실행시키는 것 - run
컨테이너 안에 포함된 실행되도록 조치된 프로그램 사용

hub.docker 

containers에서 카테고리를 통해 컨테이너 고를 수 있음
ex. 아파치 웹 서버 (httpd) https://hub.docker.com/_/httpd
docker pull httpd 를 통해 다운 가능

docs.docker.com 설명서
reference에서 CLI

docker images 로 다운되어있는지 확인

# 4.
![image](https://github.com/Carbon6-Free/DockerStudy/assets/101008357/bd299a41-a95c-48cf-852e-d4c5280608ed)

run을 클릭시 이미지 -> 컨테이너 
(이름 지정을 알아보기 쉽게하기)
logs, inspect, stats
stop을 할 수 있고, delete 삭제 할 수 있음

docker run httpd
docker run --name ws2 httpd
새로운 컨테이너 생성 ws2로 나옴
![image](https://github.com/Carbon6-Free/DockerStudy/assets/101008357/99e1f6f6-9a61-4f2a-b01e-99b9821aa6a6)


docker ps로 실행 컨테이너 확인 가능

docekr stop ws2

docker ps -a 
all이라는 것으로 stop했다고 삭제된 건 아니고 -a에서는 보임

docker start ws2

logs가 보이지 않음 
docker logs

삭제 = docker rm 
(실행 중인거 삭제 안 돼서, 멈추고 rm)
(docker rm --force 파일명 하면 멈추지 않고 삭제 가능)

docker rmi httpd
한다면 이미지가 삭제된다.
![image](https://github.com/Carbon6-Free/DockerStudy/assets/101008357/a2806da7-66bf-4dbe-bb19-e71789b6b4b9)
위 사진과 같이 터미널에서 명령어로 실행시킬 수 있다.


# 5.
네트워크

web server
browser

port 80 기본?적으로 많이 사용?  

docker host와 container port가 연결되어있어야함
ex. docker run -p 80:80 httpd
   포트:컨테이너
ex. 8000으로 바뀐다면  
   docker run -p 8000:80 httpd  

docker pull httpd
ws2
local 8080 port 80

----
option 보기

docker ps
8080->80

docker run --name ws3 -p 8081:80 httpd
(port 8081임.)

# 6.
명령어 실행

index.html을 변경해서 나의 웹을 만들기

#pwd

#ls -al
파일 안에 있는 것들
command 실행시키고 싶은 것

docker exec ws3 pwd
         ls
docker exec ws3 /bin/sh (sh 창구와 같은 역할)
-it를 넣으면 ws3 앞에 넣으면 실행 유지

docker ps

연결을 끊기 
#exit

nano 에디터 

설치 후 
nano index.html 하면 수정 할 수 있는 상태

# 7.
호스트와 컨테이너의 파일시스템 연결

컨테이너가 사라진다면 문제가 생길 수 있음
그래서 둘을 연결하고 반영된다면..?
사라져도 host에 그대로 남아있을 수 있음
ver관리도 쉬움

host에서 파일 수정 관리 편함

## 맥으로 진행
문서에 docker폴더 만들고 vscode로 열어서 index.html파일 만들어 아래의 명령어 실행
명령어: docker run -p 8888:80 -v /Users/ohseungyeon/Documents/docker:/usr/local/apache2/htdocs/ httpd
![image](https://github.com/Carbon6-Free/DockerStudy/assets/101008357/885f600e-a3c0-413d-8e2f-e370fc28792f)
<img width="1470" alt="image" src="https://github.com/Carbon6-Free/DockerStudy/assets/101008357/c7699ad1-1cff-4418-8fd8-9e286af48247">

