---
{"dg-publish":true,"permalink":"//aws/ec-2/","dgPassFrontmatter":true}
---


#### 인스턴스 생성
네트워크 설정 HTTP, HTTPS 트래픽 허용
키페어 생성
인스턴스 시작

###### 인바운드 규칙 편집
8080, 80 포트 열어주기

#### 배포
git bash 이용해 접속(우분투)
`ssh -i 키페어의 위치 ubuntu@인스턴스 ip`
질문 나오면 yes 해주기

````
sudo apt-get update
sudo apt-get install openjdk-11-jdk -> 버전 맞게 설치
java -version
````

###### FileZilla 를 사용해서 배포 파일 업로드 하기
프로토콜 : SFTP
호스트 : 인스턴스 ip 붙여넣기
포트 : 22
사용자 : ubuntu
키 파일 : 키파일 넣어주기
왼쪽에 있는 우분투 서버에 .jar 파일 드래그해서 업로드

###### 80포트로 오는 요청을 8080 포트로 전달하게 하는 포트포워딩
`sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080`

###### 서비스 시작
`java -jar JAR파일명.jar`
서비스 끌 때는 ctrl + c

###### 원격 접속 끊어도 서버가 계속 돌게 하기
`nohup java -jar JAR파일명.jar &`

###### 서버 강제 종료
프로세스 번호를 보는 명령어
`ps -ef | grep java`

프로세스 끄기
`kill -9 [pid값]`