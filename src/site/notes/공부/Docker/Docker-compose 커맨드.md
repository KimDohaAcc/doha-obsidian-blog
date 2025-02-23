---
{"dg-publish":true,"permalink":"//docker/docker-compose/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/Docker/Docker-compose 커맨드/","dgPassFrontmatter":true}
---

version : docker compose 버전(3, 3.9 이렇게 씀)
-> 원래 최상단에 쓰이던 건데 **이제 필요 없다고 함! (docker 2.25 이상부터)**

services: 서비스를 Docker Engine으로 불러오는데, 관리 명칭을 jenkins로 함
container name : 컨테이너 네임
image : 이미지 사용할 거
user : 작성 안 하면 디폴트는 jenkins로 잡힘. jenkins는 mkdir 권한이 있는 계정으로 설정해줘야 함. "${UID} : ${GID}" workspace에서 빌드를 할 때 mkdir 을 해서 jar 파일을 만들 수 있어야 하는데 root 권한이 없으면 mkdir 을 못해서 파일을 못 만든다. 그렇기 때문에 user를 mkdir 권한이 있는 계정으로 줘야 한다!
restart : 재시작 조건
ports : 외부 리눅스 방화벽에 공유할 포트 : 내부 포트 (방화벽 열려 있어야 연결 되나?)
volumes : container 내부 파일 외부 공유 설정 ex) jenkins_home : /home/ubuntu/jenkins -> 리눅스 디렉토리 마운트가 일어남. jenkins_home 디렉토리 내용이  /home/ubuntu/jenkins 에 그대로 들어감
-> 남발하면 보안상 좋지 않다. 환경변수나 특정 파일들을 넣어주고  마운트해서 적용할 수 있음
networks : 도커 네트워크를 쓰겠다고 명시
external : 앞어 networks 를 쓴다고 했으면 external : true 라고 했을 때 기존에 만든 dockernetwork를 그대로 쓴다는 의미 .만약 false 가 되면 네트워크가 하나 만들어짐

| Depth | Command        | 의미 설명                                                            |
| ----- | -------------- | ---------------------------------------------------------------- |
| 0     | version: ‘3’   | Docker-compose 3으로 만들어진 문서라는 의미, version: ‘3.9’ 등으로 사용 가능.       |
| 0     | services:      | 이하 Service ‘목록’이 나올 것임을 명시                                       |
| 2     | jenkins        | Service를 Docker Engine으로 불러오는데, 관리명칭을 ‘Jenkins’로 함               |
| 4     | build          | ‘Jenkins’ Service의 build 조건임을 명시                                 |
| 4     | container_name | Depth 2의 ‘Jenkins’를 실제 Docker Engine에서 관리하기 위한 이름을 명시            |
| 4     | image          | Docker Hub에서 가져올 이미지 이름                                          |
| 4     | user           | Service에서 사용할 계정정보                                               |
| 4     | restart        | Docker Container 재시작 조건                                          |
| 4     | ports          | 외부 리눅스 방화벽에 공유할 Port와 Docker Container 내부 Port번호 명시              |
| 4     | environment    | Docker Container에서 사용하는 환경변수임을 명시                                |
| 4     | volumes        | 외부 리눅스 디렉토리에 Docker Container 내부의 디렉토리를 공유함을 명시                  |
| 4     | networks       | Docker Network 관련 정보임을 명시                                        |
| 4     | network_param  | Depth 4 network에서 사용할 network의 이름을 작성하며, -로 시작함                  |
| 4     | external       | Docker network에서 미리 만들어 놓은 Bridge를 재사용한다는 의미(같은 네트워크 대역을 쓴다는 선언) |
#### Docker 네트워크
백엔드에서 db로 접근할 때 도메인:3306으로 mysql 가려면 nginx 거쳐서 방화벽 열려 있는 3306으로 들어가서 mysql로 가야했음
도커 네트워크를 사용하면 EC2 내부에서 이동할 수 있다! -> 보안적으로 유리하고 안정적임
적극적으로 써라~
같은 네트워크 대역대를 쓴다는 선언이다