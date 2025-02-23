---
{"dg-publish":true,"permalink":"///ubuntu/","dgPassFrontmatter":true}
---


### 서버 시간을 한국 표준시로 변경 (UTC+9)

 AWS의 Ubuntu는 기본적으로 UTC+0으로 설정되어 있기 때문에, 한국 시간으로 맞춰주자

```bash
sudo timedatectl set-timezone Asia/Seoul
```

### 미러 서버를 카카오 서버로 변경(선택)

기본 서버는 .ubuntu.com 이라는 해외 서버이다
해외망, 해외 서버를 사용하게 되면 패키지를 갱신/다운로드를 하는 속도가 매우 느리기 때문에, 카카오 서버(타 서버를 사용해도 무관하다)로 미러 서버를 변경하면 빠르다(AWS EC2, AWS Lightsail에서 사용 가능)
다만, kakao 서버와 ubuntu 서버의 패키지 업데이트 수준이 동일하지 않을 수도 있다.

```bash
sudo sed -i 's/ap-northeast-2.ec2.archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list
```

#### 패키지 목록 업데이트 및 패키지 업데이트

패키지를 다운받는 미러서버가 변경되었기 때문에 update를 진행한다
미러서버의 패키지 목록이 갱신되었다면 패키지를 최신 버전으로 upgrade 하기

```bash
sudo apt-get -y update && sudo apt-get -y upgrade
```

- 패키지 목록 업데이트 도중 다음과 같은 화면이 나오면 **ENTER** 키를 누른다
    
    ```
    What do you want to do about modified configuration file sshd_config?
    ```
    
### Swap 영역 할당

- 용량 확인

```jsx
free -h
```

- 스왑 영역 할당

```bash
sudo fallocate -l 4G(임의로 할당) /swapfile
```

- swapfile 권한 수정

```bash
sudo chmod 600 /swapfile
```

- swapfile 생성

```bash
sudo mkswap /swapfile
```

- swapfile 활성화

```bash
sudo swapon /swapfile
```

- 시스템이 재부팅 되어도 swap 유지할 수 있도록 설정

```bash
sudo echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

- swap 영역이 할당 되었는지 확인

```bash
free -h
```