# Docker 개인 저장소 구축하기
- 기존 실행되고 있는 Docker 데몬 정지하고 
	- service docker stop
- --insecure-registry옵션 사용하여 Docker 데몬 실행
	- docker -d --insecure-registry localhost:5000
- Docker 데몬을 직접 실행하지 않고 서비스 형태로 실행
	- /etc/init.d/docker
		- DOCKER_OPTS=--insecure-registry localhost:5000
	- /etc/init.d/docker 파일을 수정했으면 Docker 서비스를 재시작
		- sudo service docker restart

- 로컬에 이미지 데이터 저장
	- Docker 레리지트리 이미지를 받는다
		- docker pull registry:latest
	- registry:latest 이미지를 컨테이너로 실행 한다.
		- docker run -d -p 5000:5000 --name hello-registry -v /tmp/registry:/tmp/registry registry
		- 이렇게 실행하면 이미지 파일은 호스트의 /tmp/registry 디렉터리에 저장된다.

- push 명령으로 이미지 올리기
	- docker tag hello:0.1 localhost:5000/hello:0.1
	- docker push localhost:5000/hello:0.1

- 태그를 생성하는 명령 
	- docker tag <이미지 이름>:<태그> <Docker 레지스트리 URL>/<이미지 이름>:<태그>
- 이미지를 올리는 명령
	- docker push <Docker 레지스트리 URL>/<이미지 이름>:<태그>

- docker tag : 개인 저장소에 이미지를 올릴 때는 태그를 먼저 생성해야 한다.
- docker push : 개인 저장소에 이미지 올린다.
- 이제 다른 서버에서 개인 저장소(Docker 레지스트리 서버)에 접속하여 이미지를 받아올 수 있다
	- docker pull 192.168.0.39:5000/hello:0.1
	- docker images
	- 개인 저장소에서 192.168.0.39:5000/hello 이미지 받는다

- 이미지 삭제
	- docker rmi 192.168.0.39:5000/hello:0.1