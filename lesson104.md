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
