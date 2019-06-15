# Dockerfile 작성하기
- Docker 이미지 설정 파일 이다.
- Dockerfile에 설정된 내용대로 이미지를 생성한다.

- Dockerfile
	- mkdir example
	- cd example
	- vi Dockerfile
		```
		FROM ubuntu:16:04
		MAINTAINER Foo Bar <foo@bar.com>
		RUN apt-get update
		RUN apt-get install -y nginx
		RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
		RUN chown -R www-data:www-data /var/lib/nginx
		VOLUME ["/data", "/etc/nginx/site-enabe", "/var/log/nginx"]
		WORKDIR /etc/mginx
		CMD ["nginx"]
		EXPOSE 80
		EXPOSE 443
		```
		```
		FROM : 어떤 이미지를 기반으로 할지 설정 한다. <이미지 이름>:<태그>
		MAINTAINER : 메인테이너 정보
		RUN : 셸 스크립트 혹은 명령을 실행
			- 이미지 생성 중에는 사용자 입력을 받을 수 없으므로 apt-get install -y 옵션 사용
			- 나머지는 nginx 설정 이다.
		VOLUME: 호스트와 공유할 디렉터리 목록이다.
			- docker run 명령에서 -v 옵션으로 설정 할 수 있다.
			- 예) -v /root/data:/data는 호스트의 /root/data 디렉터릴를 Docker 컨테이너의 /data 디렉터리와 연결
		CMD : 컨테이너가 시작되었을 때 실행할 실행 파일 또는 셸 스크립트
		WORKDIR : 컨테이너가 시작되었을 때 실행할 실행 파일 또는 셸 스크립트
		EXPOSE : 호스트와 연결할 포트 번호


		```
