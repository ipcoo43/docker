# Bash(Bourne-again Shell) 익히기

- ＞ : 출력 리다이렉션. 명령 실행의 표준 출력(stdout)을 파일로 저장, 장치도 파일로 처리하기 때문에 명령 실행 결과을 특정 장치로 보낼 수 있다.
	- 'hello' ＞ ./hello.txt

- ＜ : 입력 리다이렉션. 파일의 내용을 읽어 명령의 표준 입력(stdin)으로 사용
	- cat ＜ ./hello.txt

- ＞＞ : 명령 실행의 표준 출력(stdout)을 파일에 추가 한다. ＞는 이미 있는 파일에 내용을 덮어쓰지만, ＞＞는 파일 뒷 부분에 내용을 추가한다.
	- echo 'world' ＞＞ ./hello.txt

- 2＞ : 명령 실행의 표준 에러(stderr)를 파일로 저장
- 2＞＞ : 명령 실행의 표준 에러(stderr)를 파일에 추가 
- &＞ : 표준 출력과 표준 에러를 모두 파일로 저장
- 1＞&2 : 표준 출력을 표준 에러로 보낸다. echo 명령으로 문자열을 표준 출력으로 출력했지만 표준 에러로 보냈기 때문에 변수에는 문자열이 들어가지 않는다.
	- hello = $(echo "Hello World" 1>&2)
	- echo $hello

- 2＞&2 : 표준 에러를 표준 출력으로 보낸다. abcd라는 명령은 없으므로 에러가 발생하지만 에러를 표준 출력으로 보낸 뒤 다시 /dev/null로 보냈기 때문에 아무것도 출력되지 않는다.
	abcd ＞ /dev/num  2＞&2

- │ : 파이프. 명령 실행의 표준 출력을 다른 명령의 표준 입력으로 보낸다. 즉 첫 번째 명령의 출력 값을 두 번째 명령에서 처리 한다.
	- ls -al │ grep .txt

- $ : Bash의 변수 이다. 값을 저장할 때는 $를 붙이지 않고, 변수를 가져다 쓸 때만 $를 붙인다.
	- $ hello = 'Hello World'
	- $ echo $hello

- $() : 명령 실행 결과을 변수화 한다. 명령 실행 결과를 변수에 저장하거나 다른 명령의 배개 변수로 넘겨줄 때 사용한다. 또는 문자열안에 명령의 싱행 결과를 넣을 때 사용 한다.
	- docker rm $(docker ps -aq)
	- echo $(date)

- `` : $()와 마찬가지로 명령 실행 결과를 변수화 한다.
	- docker rm `docker ps -aq`
	- echo `date`

- && : 한 줄에서 명령을 여러 개 실행한다. 단 앞에 있는 명령이 에어 없이 실생되어야 뒤에 오는 명령이 실행된다.
	- make && make install

- ; : 한 줄에서 명령을 여러 개 실행한다. 앞에 있는 명령이 실패를 해도 뒤에 오는 명령이 실행된다.
	- false; echo "Hello"

- ${} : 변수 치환이다. 
	- str = 'world'
	- echo 'Hello ${str}'
	- hello =
	- hello=${hello-'abcd'}
	- echo $hello

- {1..10} : 연속된 숫자 표현 한다.{시작 숫자.. 끝 숫자}
	- echo {1..10}

- {문자열1, 문자열2} : {}안에 문자열을 여러 개 지정하여 명령 실행 횟수를 줄인다.
	- cp ./{hello.txt, world.txt} hello-dir/

- if : 변수와 변수끼리 또는 문자열과 비교할 때 사용 한다.
	- if [ $a -eq $b]; then
	-    echo $a
	- fi
	- -eq:같다, -ne:같지 않다, -gt:초과, -ge:이상, -lt:미만, -le:이하
	- =,==:같다, !=:같지 않다, -z:문자열이 Null 일때, -n:문자열이 Null 아닐 때

- for : 변수 안에 있는 값을 반복하거나 범위를 지정하여 반복 할 수 있다.
	- for i in %(ls)
	- do
	-   echo $i
	- done
	- for (( i=0; i<10; i++))
	- do
	-   echo $i
	- done
	- num=(1,2,3)
	- for i in ${num[@]}
	- do
	-   echo $i
	- done

- while : while 반복문
	- while :
	- do
	-  echo 'Hello World'
	-  sleep 1;
	- done

- ＜＜＜ : 문자열을 명령(프로세스)의 표준 입력으로 보낸다.
	- cat ＜＜＜ "User name is $USER"

- ＜＜EOF : 여러 줄의 문자열을 명령(프로세스)의 표준 입력으로 보낸다.
	- cat > ./hello.txt ＜＜EOF
	- Hello World
	- Host name is $(hostname)
	- EOF

- export <변수>=<값> : 설정한 값을 환경 변수로 만든다.
	- export HELLO = world

- printf : 지정한 형식대로 값을 출력한다. 파이프와 연동하여 명령에 값을 입력하는 효과를 낼 수 있다.
	- printf 80\\nexampleuser\\ny | example-confing