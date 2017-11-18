MAUM 플랫폼

개요

대화 서비스 플랫폼
대화 서비스 개발 플랫폼
설치 유형 : AWS 또는 푸른 하늘의 구내 또는 SaaS.
개발 환경

섬기는 사람
C ++
프로토콜들
grpc 기반 인터페이스
관리 콘솔 웹
각도 2
앵귤러 2 재질
관리 콘솔 나머지
nodejs 6.10 이상
grpc 노드
루프백 3
웹 프록시 서버
nginx 1.11 이상
웹
websocket을 사용하는 nodejs
짓다

개요

CMake (2.8.12), 3.1 이상이 더 나은 선택입니다.
완전 지원을위한 GCC 4.8.2 c ++ - 11, 문제점 # 18, 18보기
위의 nodejs 6.10.0
점검

git clone git@github.com : mindslab-ai / maum.git
외부 의존성

빌드 시간 종속성 만 보여줍니다. 모든 필수 패키지는에 의해 설치됩니다 prerequisite.sh.

다음 패키지 종속성은이 프로젝트 관점만을 보여줍니다. 다음 명령을 직접 사용하지 마십시오.

우분투 외부 의존성

sudo apt-get install -y \
  gcc-4.8g ++ - 4.8g ++ \
  make cmake \
  autoconf automake libtool \
  파이썬 - 파이썬 파이썬 - dev에 \
  openmpi-common \
  libboost-all-dev \
  libcurl4-openssl-dev \
  libsqlite3-dev \
  libmysqlclient-dev \
  libuv-dev libssl-dev \
  libarchive13 libarchive-dev \
  libatlas-base-dev libatlas-dev \
  docker.io \
  압축을 풀다
  nginx \
  ffmpeg
sudo ldconfig
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
CentOS 또는 REDHAT 외부 의존성

sudo yum -y install epel-release
sudo yum -y groupinstall ' 개발 도구 '
sudo yum -y install \
  gcc gcc-c ++ \
  autoconf automake libtool make \
  cmake cmake3 \
  glibc-devel.x86_64 \
  java-1.8.0-openjdk-devel.x86_64 \
  python-devel.x86_64 \
  flex-devel..x86_64 \
  부스트 - devel.x86_64 \
  libcurl-devel.x86_64 \
  sqlite-devel.x86_64 \
  mysql-community-devel.x86_64 \
  openssl-devel.x86_64 \
  libarchive-devel.x86_64 \
  atlas-devel.x86_64 \
  lapack-devel.x86_64 \
  libuv-devel.x86_64 \
  httpd nginx \
  policycoreutils-python

## TODO (정 호킴) 도커 설치

# PIP 및 패키지 설치 
컬을 " https://bootstrap.pypa.io/get-pip.py " -o " get-pip.py "
sudo python get-pip.py
rm get-pip.py
# npm 
curl - silent --location https://rpm.nodesource.com/setup_6.x | sudo bash -
sudo yum install -y nodejs
외부 파이썬 패키지

sudo pip install --upgrade pip
sudo pip install - upgrade virtualenv
sudo pip install boto3 grpcio == 1.0.1 요청 numpy theano gensim
외부 노드 패키지

sudo npm install -g @ angular / cli @ 1.0.0
내부 의존성

다음 의존성은 서브 모듈에 의해 관리됩니다. (참조 git submodule)

libminds
protobuf 3.2
grpc 1.1.3
마음가짐
마음 - 따
hazelcast-cpp-client
(카산드라) cpp-driver
위의 protobuf, grpc, hazelcast-cpp-client, cassandra-cpp-driver는 OS 패키지 시스템으로 아직 관리되지 않습니다. git 서브 모듈을 통해 로컬에서 관리합니다.

사용하는 방법 build.sh

모든 하위 빌드 작업.
libminds : protobuf, libminds, grpc
libdb : hazelcast-cpp-client, cassadra-cpp-driver
stt : minds-stt
따 : 마음 - 타
maum : maum 서버, 웹 콘솔, 웹 레스트
web-had은 자동으로 생성되지 않습니다.
빌드 모드
필요한 작업을 빌드합니다.
모든 내장 출력을 대상 디렉토리에 설치합니다. 기본 대상 디렉토리는 ~/minds입니다.
대상 디렉토리에 필요한 모든 자원을 설치합니다.
./build.sh ~ / 마음 전체
./build.sh ~ / minds maum
./build.sh ~ / minds libminds stt
배포 모드
배포 빌드를위한 임시 디렉토리를 만듭니다.
필수 패키지를 빌드합니다.
stt, ta 자원을 제외한 모든 바이너리와 자원을 설치합니다.
소스 루트 디렉토리에 .tar.gz파일을 생성 합니다 out.
./build.sh tar
./build.sh tar ta-only
./build.sh tar stt-only
다른 통신
./build.sh clean-deploy
./build.sh clean-cache
내부 build.sh

~ / .minds-build
cache:이 디렉토리에는 몇 가지 미리 만들어진 결과가 있습니다. protobuf, grpc, hazelcast-cpp-client, cassandra-cpp-driver에 대한 이전 외부 빌드 출력을 컴파일러 버전으로 캐시합니다.
*.done: prerequisite.sh가 모든 종속성을 성공적으로 설치하면,이 파일은 해당 스크립트에 대해 주어진 sha1 해시로 생성됩니다.
build-debug: cmake개발 모드에서이 디렉토리를 만듭니다.
build-deploy-debug: cmake배포 모드에 대해이 디렉토리를 만듭니다.
생성 된 tar 파일의 버전 번호가 있습니다 git describe.
인사

위의 2.8.12를 사용하십시오.
centos에서는 사용 cmake3하지 마십시오 cmake.
다음 옵션을 사용합니다.

DCMAKE_INSTALL_PREFIX = $ {MINDS_ROOT}
DCMAKE_BUILD_TYPE = 디버그
DCMAKE_CXX_COMPILER : FILEPATH = / usr / bin / g ++ - 4.8
DCMAKE_C_COMPILER : FILEPATH = / usr / bin / gcc-4.8
centos에서 /usr/bin/g++버전은 4.8.5입니다.

특별 옵션을위한 맞춤 빌드.

Maum은 특별한 출력을 만들기 위해 몇 가지 전처리기를 가지고 있습니다.

오디오 파일 저장 용

mkdir ~ / git / maum / build-debug-record
 cd  ~ / git / maum / build-debug-record
cmake \
  -DCMAKE_INSTALL_PREFIX = $ {MINDS_ROOT} \
  -DCMAKE_BUILD_TYPE = 디버그 \
  -DCMAKE_CXX_COMPILER : FILEPATH = / usr / bin / g ++ - 4.8 \
  -DCMAKE_C_COMPILER : FILEPATH = / usr / bin / gcc-4.8 \
  -DDEFINE_RECORD_AUDIO = ON \
  ..
용도 alias.root

설정 --global --add alias.root를 이눔 ' ! pwd을 ' 
-C 수 있도록 $ ( 자식 루트 ) / 빌드 디버그를 설치
CLion은 디버그 빌드 디렉토리를 만듭니다. 그걸 써.
고토 Settings > Build, Execution, Deployment > CMake설정한다.
cmake 옵션을 추가하십시오.
  -DCMAKE_INSTALL_PREFIX = $ {MINDS_ROOT}
  -DCMAKE_CXX_COMPILER : FILEPATH = / usr / bin / g ++ - 4.8
  -DCMAKE_C_COMPILER : FILEPATH = / usr / bin / gcc-4.8
-C $ ( git root ) / cmake-build-debug install을 만든다.
개발 도구, 테스트

개발 ~/minds시 기본 설치 디렉토리입니다. 빌드 된 바이너리와 라이브러리를 처리하는 것이 더 편리합니다.

설정

export MINDS_ROOT = ~ / minds
 export LD_LIBRARY_PATH = $ LD_LIBRARY_PATH : $ {MINDS_ROOT} / lib
 export PATH = $ PATH : $ {MINDS_ROOT} / bin :
CDPATH = ~ / minds : ~ / git / maum : .. :. # maum 경로는 개인 설정으로 변경할 수 있습니다.
cd logs # ~ / minds / logs에서 
빠져 나옵니다. cd bin
용도 mindset

사고 방식 발전기
사고 방식
항상 모든 구성 파일을 생성합니다.

시스템 사용

서버를 실행할 스크립트

sudo $ {MINDS_ROOT} / bin / mindset systemd

sudo sytemctl daemon-reload
sudo systemctl start minds.target
sudo systemctl list-units 마음 *
sudo systemctl restart minds.target
sudo systemctl stop minds.target
sudo systemctl enable minds.target
sudo systemctl disable minds.target
Docker 수동 시작

도커 설치

sudo apt-get install docker.io
sudo usermod -aG docker $USER
Hazelcast 고정 컨테이너

sudo apt-get install openjdk-8-jdk
도커가 헤이즐 캐스팅 / 헤이즐 캐스팅
도커 실행 -p 5701 : 5701 -ti hazelcast / hazelcast
카산드라 도커 컨테이너

테스트 -d $ {MINDS_ROOT} / db | mkdir -p   $ {MINDS_ROOT} / db
도커 실행 - 이름 cassandra \
 -p 9042 : 9042 \
 -v $ {MINDS_ROOT} / db : / var / lib / cassandra \
 -d cassandra : 최신
대화 상자 에이전트 테스트를위한 파이썬 라이브러리 의존성.

sudo pip 설치 pymysql
