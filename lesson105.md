# build로 이미지 생성하기
- Dockerfile을 작성하였으면 이미지를 생성한다.
- docker build <옵션> <Dockerfile 경로>. --tag 이미지이름과 태그 설정
	- docker build -- tag hello:0.1 .
	- docker images
	- docker run --name hello-nginx -d -p 80:80 -v /root/data:/data hello:0.1
		- -d : 컨테이너를 백그라운드로 실행
		- -p 80:80 : 호스트의 80 포트와 컨테이너 80 포트를 연결하고 외부에 노출 한다. 이렇게 설정 한 뒤 http://<호스트 IP>:80에 접속하면 컨테이너의 80번 포트로 접속된다.
		- -v /root/data:/data : 호스트 /root/data 디렉토리를 컨테이너 /data 디렉토리에 연결 한다. /root/data 디렉터리에 파일을 넣으면 컨테이너에서 해당 파일을 읽을 수 있다.
	- docker ps
	- 웹 브라우저 실행하고 http://<호스트 IP>:80으로 접속한다.