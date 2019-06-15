# Docker 살펴보기
- 이미지와 컨테이너 정보 조회 방법, 컨테이너에서 파일 꺼내는 방법, 변경파일 확인 방법, 변경 사항 이미지 저장 방법을 알아 본다

- history <이미지 이름>:<태그>: 이미지 히스트리 살펴보기
	- docker history hello:0.1

- cp <컨테이너 이름>:<경로> <호스트 경로> : 파일 꺼내기
	- docker cp hello-nginx:/etc/nginx/nginx.conf ./
	- 현재 디렉토리에 nginx.conf 파일이 복사되었다.

- commit <옵션> <컨테이너 이름> <이미지 이름>:<태그> : 컨테이너의 변경사항을 이미지로 생성
	- docker commit -a "Foo Bar <foo@bar.com>" -m "add hello.txt" hello-nginx hello:0.2
	- -a "Foo Bar <foo@bar.com>"과 -m "add hello.txt" 옵션으로 커밋한 사용자와 로그 메시지를 설정합니다. 
	- hello-nginx 컨테이너를 hello:0.2 이미지로 생성 한다.

- docker images

- diff <컨테이너 이름> : 컨테이너에서 변경된 파일 확인하기
	- docker diff hello-nginx
	- A는 추가된 파일, C는 변경된 파일, D는 삭제된 파일

- inspect <이미지 또는 컨테이너 이름> : 세부 정보 확인하기
	- docker inspect hello-nginx