# docker 설치하기
- 우분투
	- apt-get update
	- apt-get install docker.io
	- ln -sf /usr/bin/docker.id /usr/local/bin/docker

# docker 명령어
- docker search : 이미지 검색
	- docker search ubuntu

- docker pull : 이미지 받기
	- docker pull ubuntu:latest

- docker images : 이미지 목록 추출
	- docker images

- docker run <옵션> <이미지 이름> <실행할 파일>: 컨테이너 생성
	- docker run -i -t --name hello ubuntu /bin/bash
	- -i (interactive), -t (Pseudo-tty) Bash 셸에 입력 및 출력 할 수 있다.
	- --name : 컨테이너의 이름 지정

- 이제 호스트와 OS와 완전히 격리된 공간이 생성됨
	- Bash 셸에서 빠져 나올 때 : exit 

- docker ps : 컨테이너 목록 확인
	- docker ps -a
	- -a 옵션은 정지된 컨테이너까지 모두 출력, 사용하지 않으면 실행되고 있는 컨테이너만 출력

- docker start <컨테이너 이름> : 컨테이너 시작
	- docker start hello

- docker restart <컨테이너 이름> : 컨테이너 재시작
	- docker restart hello

- docker attach <컨테이너 이름> : 컨테이너에 접속하기
	- docker attach hello

- docker exec  <컨테이너 이름> <명령> <매개 변수> : 외부에서 컨테이너 안의 명령 실행
	- docker exec hello echo 'Hello World'

- docker stop  <컨테이너 이름> : 컨테이너 정지
	- docker stop hello

- docker rm  <컨테이너 이름> : 컨테이너 삭제
	- docker rm hello

- docker rmi  <컨테이너 이름>:<태그> : 이미지 삭제
	- docker rmi ubuntu:latest

	- docker images
