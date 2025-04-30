# 도커
### 도커(Docker)
- Go언어로 작성된 리눅스 컨테이너 기반의 오픈소스 가상화 플랫폼
- 어떤 프로그램을 외부 환경과 격리시켜 구동할 수 있게 해주는 소프트웨어

### 컨테이너(Container)
![container](/DevOps_CICD/img/docker_container.png)
- OS상에 논리적인 영역(컨테이너)을 구축하고, 어플리케이션이 작동하는데 필요한 요소들을 모아 별도의 서버처럼 동작하는 것


> [!NOTE] VM과 다른점?
> ![vm](/DevOps_CICD/img/docker_vm.png)
> VM은 실제로 운영체제를 설치하는 개념, 도커는 운영체제가 가지고있는 주요 기술들을 일부분 가져다가 OS처럼 보여지게끔 환경을 세팅해서 어플리케이션이 돌아가도록 해주는 것

### 도커 구성 요소
![component](/DevOps_CICD/img/docker_component.png)
- Docker Client
  - 명령어(docker run, docker build)를 입력하는 터미널 프로그램
- DOCKER_HOST
  - 도커가 띄워져 있는 서버
  - 컨테이너와 이미지를 관리함
- Docker Daemon
  - 백그라운드에서 도커 컨테이너들을 관리하는 서버 프로세스
  - 이미지, 컨테이너, 네트워크 등 도커 오브젝트들을 관리 함
- Registry
  - 외부 이미지 저장소
  - 다른 사람들이 공유한 이미지를 내부 로컬의 도커 호스트에 pull 할 수 있음
- Dockerfile
  - 이미지를 만들기 위한 스크립트 파일
- Docker Image
  - 애플리케이션과 그 환경을 담은 정적인 파일
  - 컨테이너를 만들기 위한 청사진
  - 이미지를 기반으로 컨테이너를 생성하여 실행












https://aws.amazon.com/ko/docker/ <br>
https://docs.docker.com/get-started/introduction/