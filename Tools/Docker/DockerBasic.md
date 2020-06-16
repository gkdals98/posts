## Docker 명령어 및 Docker File 만들기
당면 목표는 Docker File로 현 작업에 필요한 Docker Image를 생성하는 것. 그 중 첫 문서는 도커의 기본 명령어들을 다룬다.

## 간단한 요약
+ tar파일, images, 컨테이너, 세 개를 관리하면 된다.
+ tar파일 상태의 image는 서버에 로드하기위한 세이브 파일로 생각하면 된다. tar로 묶어 저장하고, load하고싶은 서버로 옮긴다.
+ image 상태는 서버에 로드된 상태로 기동은 안된 docker라 생각하면 편하다.
+ 컨테이너는 image가 실제 기동된 것을 의미한다. 컨테이너가 기동된 상태에선 exec을 통해 해당 docker로 접속할 수 있다.

## 조회
#### docker images
+ 관리 중인 docker image들을 보는 명령어
+ 아래와 같은 형태로 docker image의 리스트를 출력한다.
```
[root@local:/root] docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mic_ems00_aside     20200424            c013dacd4fe1        3 days ago          378 MB
[root@local:/root]
```
+ Image를 제어할 땐 일반적으로 REPOSITORY와 TAG로 대상지정을 하는 듯.
+ Image를 대상으론 save를 통한 tar파일화, run을 통한 기동 등을 할 수 있으며 save된 tar를 image로 load할 수 있다.

#### docker ps
+ 현재 기동 중인 docker 컨테이너들을 보는 명령어
```
[root@local:/root] docker ps
CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS               NAMES
96a31bc2d13b        mic_ems00_aside:20200424    "/bin/bash"              3 days ago          Up 3 days                               MIC_EMS00Aside_DEV
[root@local:/root]
```
+ 기동 중인 docker 프로세스를 대상으론 exec으로 접속하거나 stop으로 기동을 정지하거나 inspect로 상세 사항을 읽을 수 있다.

#### docker inspect
+ 기동중인 docker image에 대한 상세를 볼 수 있다.
+ 우선 설명을 볼 컨테이너를 지정하기 위해 하기와 같이 docker ps 명령어로 기동 중인 컨테이너를 확인한다.
```
[root@local:/root] docker ps
CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS               NAMES
96a31bc2d13b        mic_ems00_aside:20200424    "/bin/bash"              3 days ago          Up 3 days                               MIC_EMS00Aside_DEV
[root@local:/root]
```
+ 아래와 같이 IMAGE를 지정해 inpect 명령을 수행한다.
```
[root@local:/root] docker inspect mic_ems00_aside:20200424
[
    {
        "Id": "sha256:c013dacd4fe1c41805b650741ec1609aa69ef5fe41030dafc63547c178acc9d4",
        "RepoTags": [
				~~~~ 중략 ~~~~~
				"RootFS": {
					"Type": "layers",
					"Layers": [
							"sha256:dda6e8dfdcf7a918d1fd7038a2a6de43f78c194c0bb220ea086af6c414254f4b",
							"sha256:86888f0aea6df7a7a4ae5595c505b0abccc1002f717efa5be32fa0337099bf1d",
							"sha256:633b6749aa50486d8c7473bb55d851d524388440f626adb7d537c67a2162d725",
							"sha256:48ae513e984d05b396e16cdfe671e13d847ff56c56e92d22bba6b732ace4fdd1",
							"sha256:7825bd2e763e68d457150f2f2b9ff68a3e0da8dfeefd79ce86bdaf2aea80c0ea",
							"sha256:e7f65520a46c29d4d3c96f1ef79ecaef9273962e15a321ad1c343326e518fa63"
					]
			}
		}
]
[root@local:/root]
```

## Image 관리
#### docker commit
+ 현재 구동 중인 도커 컨테이너의 상태를 이미지화 하기 위한 명령어.
#### docker save
+ 도커 이미지를 tar 파일로 저장하기 위한 명령어.
+ ```-o``` 옵션은 tar파일의 이름을 지정하기 위해 사용된다.
```
[root@obxepc-Svr-host00b:/root]$ docker save -o src_ems00b.tar svr_ems00_bside:20190220
```
#### docker load
+ tar파일로 저장된 이미지를 서버에 로드하기 위한 명령어
+ ```-i```옵션은 load할 파일 명을 명시하기 위해 사용된다.
```
[root@obxepc-Svr-host00b:/root]$ docker load -i src_ems00b.tar
```
#### docker run
+ load된 이미지를 실제로 실행시키는 명령어. 여기서 옵션이 상당히 많아진다.

## 구동 중인 Docker의 관리

#### docker exec
+ 구동중인 도커에 접속하기 위한 명령어.
```

```
#### docker stop

#### docker restart

## Docker image의 생성

#### docker build
