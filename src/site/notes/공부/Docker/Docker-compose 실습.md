---
{"dg-publish":true,"permalink":"//docker/docker-compose/","dgPassFrontmatter":true}
---


```shell
curl -fsSL https://get.docker.com -o dockerSetter.sh
# https://get.docker.com에 있는 shell 스크립트 파일을 dockerSetter.sh 파일에 출력
chmod 711 dockerSetter.sh # 권한 부여
.dockerSetter.sh # 실행
docker -v && docker compose version # 도커와 컴포즈 버전 출력

# 방화벽 설정 ubuntu firewall
sudo ufw status # 상태 확인
sudo ufw enable # 꺼져 있으면 활성화
sudo ufw allow 22 && sudo ufw all 443 # 닫혀 있으면 열기 22랑 443은 무조건 등록을 해야함 항상
sudo shutdown -r now # 재시작. 이미 활성화 되어있으면 할 필요 없다

# 도커 네트워크
sudo docker network create -d bridge test-net # 생성
sudo docker network list

touch docker-compose.yml # 빈 파일 만들기
vi docker-compose.yml # 쓰기 모드
sudo docker compose -f ./docker-compose.yml up -d # 이 버전을 더 권장하고 있다
# 또는
sudo docker compose up -d

sudo docker ps -a # 컨테이너 상태 확인
```

ufw에 22, 80, 443만 열어놓는 걸 권장한다
데이터가 왔다갔다 할 때 해킹에 취약해짐
그러니까 최소한만 열어놓고 docker network 쓰자