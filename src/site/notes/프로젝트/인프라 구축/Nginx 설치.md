---
{"dg-publish":true,"permalink":"///nginx/","dgPassFrontmatter":true}
---



## NginX 설치 (Docker)

### NginX 이미지 받기

docker의 pull 명령을 통해 최신 latest 버전의 nginx 이미지를 다운로드 한다

```bash
sudo docker pull nginx:latest
```

### NginX 컨테이너 실행

- nginx 컨테이너를 명령어를 통해 서비스를 띄운다
  
    - `run` : 이미지를 가지고 컨테이너를 만들고 컨테이너 실행
    - `-d` : 컨테이너를 만들고 백그라운드에서 계속 구동하게 하는 옵션 (데몬)
    - `--restart always` : 컨테이너가 모종의 이유로 종료되더라도 자동으로 재시작하는 옵션
    - `-e TZ=Asia/Seoul` : 환경변수 설정 (컨테이너 내부 시간대를 Asia/Seoul로 지정)
    - `--name` : 컨테이너 이름 지정 (미지정시 무작위로 이름 지정)
    - `-p` : host:container 포트를 연결

```bash
docker run -d --restart always -p 80:80 -p 443:443 -e TZ=Asia/Seoul --name nginx -u root nginx:latest
```

nginx 종료

```bash
docker stop nginx
docker rm nginx
```

### NginX 접속

```bash
docker exec -it nginx /bin/bash
```

## SSL 설정 (CertBot)

### CertBot 다운로드

- snap을 이용해서 다운로드 한다

```bash
sudo snap install --classic certbot
```

### SSL 인증서 발급

 -d : 등록할 도메인 Host 주소를 입력한다

```bash
sudo certbot --nginx -d 도메인 주소
```
