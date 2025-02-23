---
{"dg-publish":true,"permalink":"///jenkins/","dgPassFrontmatter":true}
---


## Jenkins 설치 (Docker)

### Jenkins 이미지 받기

docker의 pull 명령을 통해 최신 LTS 버전의 jenkins 이미지를 다운로드 한다
- Java 8, 11

```bash
docker pull jenkins/jenkins:lts
```

- Java 17

```bash
docker pull jenkins/jenkins:jdk17
```

### Jenkins 컨테이너 실행

- Jenkins 컨테이너를 명령어를 통해 서비스를 띄운다
    - `sudo` : 관리자 권한으로 명령어를 실행한다
    - `-d` : 컨테이너를 **데몬**으로 띄운다
    - `--restart always` : 컨테이너가 모종의 이유로 종료되더라도 자동으로 재시작하는 옵션
    - `-e TZ=Asia/Seoul` : 환경변수 설정 (컨테이너 내부 시간대를 Asia/Seoul로 지정)
    - `-p 8080:8080` : 컨테이너 외부와 내부 포트에 대해 **포워딩** 한다
        - 왼쪽 : Host Port
        - 오른쪽 : Container Port
    - `-v /etc/localtime:/etc/localtime:ro` : Host OS의 localtime을 컨테이너의 localtime과 동기화
    - `-v /jenkins:/var/jenkins_home` : 도커 컨테이너의 데이터는 컨테이너가 종료되면 사라지기 때문에, **볼륨 마운트** 옵션을 이용하여 Jenkins 컨테이너의 /var/jenkins_home 디렉토리를 Host OS의 /jenkins와 연결하여 데이터를 유지한다
    - `--name jenkins` : 도커 컨테이너의 이름을 설정하는 옵션
    - `-u root` : 컨테이너가 실행될 리눅스 사용자 계정 지정 (root)

- Java 8, 11

```bash
docker run -d --restart always --env JENKINS_OPTS=--httpPort=8080 -v /etc/localtime:/etc/localtime:ro -e TZ=Asia/Seoul -p 8080:8080 -v /jenkins:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v /usr/local/bin/docker-compose:/usr/local/bin/docker-compose --name jenkins -u root jenkins/jenkins:lts
```

- Java 17

```bash
docker run -d --restart always --env JENKINS_OPTS=--httpPort=8080 -v /etc/localtime:/etc/localtime:ro -e TZ=Asia/Seoul -p 8080:8080 -v /jenkins:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v /usr/local/bin/docker-compose:/usr/local/bin/docker-compose --name jenkins -u root jenkins/jenkins:jdk17
```

Jenkins 종료

```bash
docker stop jenkins
docker rm jenkins
```

정상적으로 컨테이너가 실행되었는지 확인하기 위해, netstat 명령어를 활용하여 포트가 개방되어 있는지 확인한다

```bash
netstat -nltp
```
### Jenkins 접속

다음 명령어를 활용하여 컨테이너의 bash 쉘에 접속한다

```bash
docker exec -it jenkins /bin/bash
```

해당하는 디렉토리로 이동한다

```bash
cd /var/jenkins_home/secrets
```

cat 명령어를 이용하여 초기 비밀번호를 확인한다. 이후 exit을 하여 컨테이너의 bash 쉘에서 나가 Host OS의 쉘로 복귀한다. 방금 확인한 관리자 비밀번호를 웹에 입력한다.

```bash
cat initialAdminPassword
```

## Jenkins 내부에 Docker 패키지 설치

### Jenkins 컨테이너 접속

```bash
docker exec -it jenkins /bin/bash
```

### Docker Repository 등록 및 docker-ce 패키지 설치

- AMD64 환경

```bash
apt-get update && apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common && curl -fsSL <https://download.docker.com/linux/$>(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && add-apt-repository "deb [arch=amd64] <https://download.docker.com/linux/$>(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable" && apt-get update && apt-get -y install docker-ce
```

- ARM64 환경

```bash
apt-get update && apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common && curl -fsSL <https://download.docker.com/linux/$>(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && add-apt-repository "deb [arch=arm64] <https://download.docker.com/linux/$>(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable" && apt-get update && apt-get -y install docker-ce
```

### Docker Jenkins에서 Host Docker 접근권한 부여

```bash
groupadd -f docker
```

```bash
usermod -aG docker jenkins
```

```bash
chown root:docker /var/run/docker.sock
```

## Jenkins 내부에 Docker-Compose 설치

### Jenkins 컨테이너 접속

```bash
docker exec -it jenkins /bin/bash
```

### Docker Compose 다운로드

curl 명령을 이용하여 docker-compose 패키지를 /usr/local/bin/docker-compose 디렉토리에 다운로드 한다

```bash
curl -L "<https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$>(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### /usr/local/bin/docker-compose 권한 변경

chmod를 이용하여 /usr/local/bin/docker-compose 디렉토리에 대해 jenkins 사용자에게 실행 권한을 추가시킨다

```bash
chmod +x /usr/local/bin/docker-compose
```

## Jenkins 파이프라인 설정 (공통)

### 플러그인 설치 목록

```bash
# ssh 커맨드 입력에 사용
SSH Agent

# docker 이미지 생성에 사용
Docker
Docker Commons
Docker Pipeline
Docker API

# 웹훅을 통해 브랜치 merge request 이벤트 발생시 Jenkins 자동 빌드에 사용
Generic Webhook Trigger

# 타사 레포지토리 이용시 사용 (GitLab, Github 등)
GitLab
GitLab API
GitLab Authentication
GitHub Authentication

# Node.js 빌드시 사용
NodeJS
```

## Jenkins 파이프라인 설정

### Pipeline script 작성 예시

```bash
pipeline {
    agent any
    
    environment {
        imageName = "계정/이미지 이름"
        registryCredential = 'Credential 이름'
        dockerImage = ''
        
        releaseServerAccount = 'ubuntu'
        releaseServerUri = '서버 uri'
        releasePort = '포트 번호'
    }

    stages {
        stage('Git Clone') {
            steps {
                git branch: '브랜치 이름',
                    credentialsId: 'Credential 이름',
                    url: '<https://서버 uri>'
            }
        }
        stage('Jar Build') {
            steps {
                dir ('디렉토리 명') {
                    sh 'chmod +x ./gradlew'
                    sh './gradlew clean bootJar'
                    // sh './gradlew build'
                }
            }
        }
        stage('Image Build & DockerHub Push') {
            steps {
                dir('디렉토리 명') {
                    script {
                        docker.withRegistry('', registryCredential) {
                            sh "docker buildx create --use --name mybuilder"
                            sh "docker buildx build --platform linux/amd64,linux/arm64 -t $imageName:$BUILD_NUMBER --push ."
                            sh "docker buildx build --platform linux/amd64,linux/arm64 -t $imageName:latest --push ."
                        }
                    }
                }
            }
        }
        stage('Before Service Stop') {
            steps {
                sshagent(credentials: ['Credential 이름']) {
                    sh '''
                    if test "`ssh -o StrictHostKeyChecking=no $releaseServerAccount@$releaseServerUri "docker ps -aq --filter ancestor=$imageName:latest"`"; then
                    ssh -o StrictHostKeyChecking=no $releaseServerAccount@$releaseServerUri "docker stop $(docker ps -aq --filter ancestor=$imageName:latest)"
                    ssh -o StrictHostKeyChecking=no $releaseServerAccount@$releaseServerUri "docker rm -f $(docker ps -aq --filter ancestor=$imageName:latest)"
                    ssh -o StrictHostKeyChecking=no $releaseServerAccount@$releaseServerUri "docker rmi $imageName:latest"
                    fi
                    '''
                }
            }
        }
        stage('DockerHub Pull') {
            steps {
                sshagent(credentials: ['Credential 이름']) {
                    sh "ssh -o StrictHostKeyChecking=no $releaseServerAccount@$releaseServerUri 'sudo docker pull $imageName:latest'"
                }
            }
        }
        stage('Service Start') {
            steps {
                sshagent(credentials: ['Credential 이름']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no $releaseServerAccount@$releaseServerUri "sudo docker run -i -e TZ=Asia/Seoul -e "SPRING_PROFILES_ACTIVE=prod" --name 컨테이너 명 -p $releasePort:$releasePort -d $imageName:latest"
                    '''
                }
            }
        }
    }
}
```

### Dockerfile 작성예시

```bash
FROM docker
COPY --from=docker/buildx-bin:latest /buildx /usr/libexec/docker/cli-plugins/docker-buildx

FROM openjdk:17-jdk
EXPOSE 443
ADD ./build/libs/doha-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```
