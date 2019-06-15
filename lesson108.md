# Docker 컨테이너 연결하기
- Docker로 이미지 생성 할 때 프로그램별로 이미지 생성
- 프로그램별로 이미지 생성하고 컨테이너에 접속 한다.
- 웹서버와 DB 연결하여 데이터 주고 받기
- Docker 컨테이너끼리 연결할 때는 docker run 명령에서 --link 옵션 사용. 먼저 DB 이미지를 컨테이너로 실행한다. 
- MongoDB를 사용 (docker run 명령은 로컬에 이미지가 없으면 자동으로 이미지를 받아 온다)
	- docker run --name db -d mongo
	- DB 컨테이너 이름은 db로 설정
- 이제 web 컨테이너를 생성하면서 db 컨테이너와 연결. 웹 서버로 사용할 컨테이너는 nginx 이미지로 생성
	- docker run --name web -d -p 80:80 --link db:db nginx
	- --link <컨테이너 이름>:<별칭>
	- docker ps
-  web 컨테이너 안에서 db:27017 주소로 db 컨테이너의 MongoDB에 접속
	- mongodb://db:27017/exampledb
	- 컨테이너 안에서 다른 컨테이너에 접속할 때는 <별칭>:<포트 번호> 형식

- 별칭과 IP 주소
	- cat `sudo docker inspect -f "{{ .HostsPath }}" web`

# 네트워크를 생성하고 컨테이너를 연결시키면 해당 네트워크 안에 속한 컨테이너끼리는 서로 접속
- docker network create 명령으로 hello-network를 생성합니다.
	- docker network create hello-network
- DB 컨테이너를 생성하면서 hello-network에 연결
	- docker run --name db -d --network hello-network mongo
- web 컨테이너를 생성하면서 hello-network에 연결
	- docker run --name web -d -p 80:80 --network hello-network nginx
- web 컨테이너에서 Bash 셸을 실행
	- docker exec -it web bash
- ping을 실행
	- ping db