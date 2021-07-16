## Docker

###### 우아한테크캠프 Pro 2기 4주차 미션은 ***그럴듯한 서비스***를 만드는 것! 개인적으로 가장 힘들었고 헤매고 어려웠던 미션이 아니었나 싶다.. (물론 아직 미션 Merge를 하지는 않았다,,)  인프라를 실제로 구축하고 어플리케이션을 배포하는 과정은 처음이기도 했고 네트워크 공부는 자세하게 한 경험이 없어서 더 어려웠던 것 같다.

> 아직 도커를 완벽히 숙지한 것이 아니라 공부 중이므로 틀린 정보가 있을 수도 있음,,

#### Docker(도커)란?

> 도커는 리눅스의 응용 프로그램들을 프로세스 격리 기술들을 사용해 컨테이너로 실행하고 관리하는 오픈 소스 프로젝트로 애플리케이션을 구축, 테스트 및 배포할 수 있는 소프트웨어 플랫폼이다. 
>
> Docker는 소프트웨어를 컨테이너라는 표준화된 유닛으로 패키징하며, 이 컨테이너에는 라이브러리, 시스템 도구, 코드, 런타임 등 소프트웨어를 실행하는 데 필요한 모든 것이 포함되어 있다.

###### Docker가 ___컨테이너 기반___으로 OS위에 Geust OS의 가상 OS를 띄우는 가상화 방식인 것 같다. 이번 미션에서는 Docker를 설치하고 nginx image를 설치하여 하나의 컨테이너로 실행해 웹 어플리케이션을 배포하고 실행하는 과정으로 진행하였고 이 과정에 맞추어서 Docker를 정리하려고 한다.



#### Docker의 요소

###### 먼저 Docker를 이해하기 위해선 (아직 다 이해 못 했지만) _Image_와 _Container_는 알고 갈 필요가 있다. 이 둘의 의미를 이해하지 못해서 많이 해맸던 것 같다.



##### Docker Container

> "컨테이너를 떠올리면 부둣가에 있는 컨테이너가 가장 먼저 떠오를 거에요"  - 우아한테크캠프Pro 씨유

###### 컨테이너는 부둣가에 있는 컨테이너를 떠올리면 어떤 의미인지는 대략적으로 다가갈 수 있을 것 같다.  독립적이지 않은 환경에서 동일한 Library나 설정파일을 참조하고 있는 각각의 Software에서는 서로 다른 조건을 필요로 할 때가 있다. 그 때마다 설정을 변경하면 타 Software에 영향을 줄 수 도 있고 비용도 추가되는데, 컨테이너는 이 점을 보완한 개념이라고 생각해도 될 것 같다.

###### 동일한 Library, 설정 파일 등의 Software 실행환경을 가지고 있는 컨테이너들이 **서로 격리되어** 각 컨테이너의 내부에서 실행되기 때문에 하나의 컨테이너에서 변경이 이루어져도 다른 컨테이너에는 영향을 주지 않기 때문에 독립적인 Software 실행환경을 제공한다.



##### Docker Image

###### 이미지는 계속 이야기하고 있는 Software 실행환경에 필요한 모든 내용들을 담고 있는 것을 이야기한다. 이미지는 read-only 상태로 변하지 않는 상태이다. 이미지는 다른 개발자가 올려놓은 이미지를 받을 수도 있고 내 실행환경을 이미지화할 수도 있다. 이 이미지를 실행시켜서 N개의 컨테이너를 생성하게 된다. 즉, ***컨테이는 실행환경들로 구성된 이미지를 기반***으로 실행된다.



###### 이 밖에도 이미지를 업로드하거나 다운로드하며 공유할 수 있는 레지스트리 등이 있는데 아직 Docker를 실습하기엔 Container와 Image를 이해하는 것으로 충분한 것 같다,,



#### Docker 설치

```bash
$ sudo apt-get update && \
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
sudo apt-key fingerprint 0EBFCD88 && \
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
sudo apt-get update && \
sudo apt-get install -y docker-ce && \
sudo usermod -aG docker ubuntu && \
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
sudo chmod +x /usr/local/bin/docker-compose && \
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```



* Docker 설치 후에 기본적으로 root권한이 필요하기때문에 root가 아닌 사용자가 sudo없이 사용하려면 해당 사용자를 docker그룹에 추가해도 된다.

```bash
$ sudo usermod -aG docker $USER # 현재 접속중인 사용자에게 권한주기
$ sudo usermod -aG docker your-user # your-user 사용자에게 권한주기
```



#### Docker Image 다운 및 Docker Container 실행

* 명령어가 이미지를 pull 해오는 명령어로 실행하면 이미지를 다운 받는다.

```bash
$ sudo docker pull unbuntu:latest
```

* 다운받은 이미지 목록을 확인할 수 있다.

```bash
$ sudo docker image
```

* Docker 실행 명령어
  * --name : 어떤 이름으로 컨테이너를 실행 할 것인지 지정

```bash
$ sudo docker run --name unbuntu unbuntu:latest
```

* 실행되고 있는 Docker bash 연결

```bash
$ docker exec -it unbuntu bash
```



##### Docker 실행 명령어

```bash
$ sudo docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```

* -d : detached mode
* -p : 호스트와 컨테이너의 포트를 연결 (port forwarding)  -p 80:80 
* -v : 호스트와 컨테이너의 디렉토리를 연결
* -e : 컨테이너 내에서 사용할 환경변수 설정
* –name : 컨테이너 이름 설정
* –rm : 프로세스 종료시 컨테이너 자동 제거
* -it : -i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션
* –link : 컨테이너 연결 



#### 실습

```bash
$ sudo docker run --name ubuntu ubuntu:latest bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
3ff22d22a855: Pull complete
e7cb79d19722: Pull complete
323d0d660b6a: Pull complete
b7f616834fd0: Pull complete
Digest: sha256:5d1d5407f353843ecf8b16524bc5565aa332e9e6a1297c73a92d3e754b8a636d
Status: Downloaded newer image for ubuntu:latest
root@b7345bbb0ec1:/#
```

* bash 접속까지 확인 되며 exit로 bash를 종료할 수 있다.
* exit로 bash를 종료할 뿐 Container가 종료되진 않는다.

##### 실행중인 Docker 목록

```bash
$ sudo docker ps
```

##### Docker 삭제

* 컨테이너 ID는 docker ps로 확인할 수 있고 위의 root@컨테이너 ID에 해당된다.

```bash
$ sudo docker stop [컨테이너 ID] && sudo docker rm [컨테이너 ID]
```

##### Docker 재실행

```bash
$ sudo docker restart [컨테이너 ID]
```

##### Docker 로그

* 컨테이너 실행 시 정상적으로 실행이 되지 않았다면 log를 확인할 수 있다.

```bash
$ sudo docker logs [컨테이너 ID]
```



#### Docker Image 생성

* ubuntu image로 테스트 컨테이너를 하나 생성

```bash
$ sudo docker run -i -t --name container_test ubuntu:latest
```

* 생성된 테스트 내부에 파일을 하나 생성

```bash
root#~~~~~~~~:/# echo test_first >> first
```

* 참고로 echo는 유닉스 계열 OS에서 문자열을 터미널에 출력해주는 명령어고 >> 파일명으로 파일을 생성할 수 있음.
* 컨테이너의 변경 사항을 적용(커밋)
  * docker commit <옵션> <컨테이너 이름, ID> <저장소 이름>/<이미지 이름>:<태그>
  * -a : 미지를 생성한 사람의 정보
  * -m : 커밋 메세지 
  * -p : 이미지를 생성하는 동안 컨테이너를 일시 정지할 지 여부

```bash
$ sudo docker commit \
	-a "tester" -m "first commit" \
	container_test \
	container_test:first
```

* 커밋한 이미지 확인

```bash
$ sudo docker images
```

* 이미지들사이에 추가된 Layer를 확인

```bash
$ sudo docker inspect ubuntu:latest | jq '.[].RootFS.Layers'
$ sudo docker inspect container_test:first | jq '.[].RootFS.Layers'

$ sudo docker inspect container_test:first | jq '.[].GraphDriver'
```

* 커밋 변경사항을 확인

```bash
$ cat /var/lib/docker/overlay2/[컨테이너ID]/diff
```





### 회고

###### Docker의 설치와 Image를 다운받아 Container를 실행하고 죽여보고 Image 생성하는 것까지 정리해보았다. 한번 정리해보니 좀 더 이해가 가는 것 같기도..? 다음은 nginx image를 받아서 java 웹 어플리케이션을 실행해보는 것 까지 정리해보겠다! Docker를 설치하고 nginx image를 설치하고를 이해가 안되니 실행이 잘 안돼서 Docker를 다 지우고 다시 설치하고 새로 서버만들어서 다시 설치하고를 조금 많이 반복한 것 같다..... 그래도 이제라도 어느정도는 이해가 되는 것 같아서 다행이다 nginx image 설치하고 어플리케이션까지 연결하는 과정을 정리하면 좀 더 이해가 가지 않을까..?

