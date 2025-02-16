---
{"dg-publish":true,"permalink":"/공부/Git/git clone(네트워크 통신~로컬 파일 저장)/","dgPassFrontmatter":true}
---

```bash
git clone https://github.com/username/repository.git

```

이 명령어는 크게 3가지 역할을 수행한다

1. 원격 저장소와 연결
2. Git 데이터를 다운로드하여 로컬 저장소 생성
3. 작업 디렉토리에 코드 파일 배치
### 네트워크 요청
Git은 원격 저장소([[공부/Git/Github\|Github]], Gitlab, Bitbucket 등)과 네트워크를 통해 데이터를 가져온다

사용자가 *git clone* 명령을 실행하면 Git은 HTTP(S) 또는 SSH 프로토콜을 사용하여 원격 저장소에 접속한다

- HTTPS 방식(기본)
	- URL이 `https://`로 시작할 때 HTTP GET/POST 요청을 사용해 원격 저장소의 데이터를 다운로드
- SSH 방식
	- `git clone git@github.com:user/repo.git` 같은 방식은 SSH 프로토콜을 사용
	- 사용자는 사전에 SSH 키를 등록해야 하고, git은 이를 이용해 인증을 수행

###### 네트워크 계층에서 일어나는 일
4. [[공부/네트워크/DNS(Domain Name System)\|DNS(Domain Name System)]] 조회를 통해 github.com의 IP 주소를 수신
5. TCP 연결을 열고 원격 저장소에 요청 보냄
6. Git 서버(Github)는 클라이언트(Git)가 요청한 데이터를 압축하여 전송

### 서버에서 데이터를 받아오는 과정
Git 서버(Github)는 클라이언트(Git)가 요청한 데이터(저장소의 전체 이력 및 파일)을 패킷 단위로 전송
- Git은 [[공부/Git/Packfile\|Packfile]] 이라는 압축된  형태의 파일을 내려받음
- 클라이언트(Git)는 이 데이터를 로컬에 저장하고, 압축을 풀어 `.git/objects/` 폴더에 배치

###### HTTP 요청 과정 예시
```text
GET /user/repo.git/info/refs?service=git-upload-pack HTTP/1.1
Host: github.com
User-Agent: git/2.34.1

```
서버는 이를 처리하고, 최신 브랜치 및 커밋 정보를 반환한다

### 로컬 저장소(.git) 생성 및 파일 다운로드
원격 서버에서 데이터를 다운로드 후 다음을 수행

1. 로컬 저장소 초기화
	- `.git/` 디렉토리를 생성하여 Git 저장소로 설정
2. 브랜치 및 커밋 데이터 다운로드
	- 서버에서 가져온 packfile을 풀어서 `.git/objects/`에 저장
	- 커밋, 트리, 블롭 등 Git 내부 객체로 변환하여 저장
3. 현재 브랜치의 최신 상태를 체크아웃
	- HEAD를 원격 저장소의 기본 브랜치(main 또는 master)로 설정
	- git checkout을 실행하여 작업 디렉토리에 실제 파일을 배치

### 실제 로컬 파일 시스템 반영
다운로드한 데이터를 로컬 파일 시스템에서 볼 수 있도록 작업 디렉토리에 배치
###### 작업 디렉토리
```
repo/                 <- 프로젝트 폴더
│── .git/             <- Git 저장소 메타데이터
│── src/              <- 코드 파일들
│── README.md         <- 프로젝트 설명 파일
│── package.json      <- 예제 (Node.js 프로젝트일 경우)
│── ...               <- 기타 프로젝트 파일들

```
- .git/ 폴더 : Git의 내부 데이터가 저장됨(커밋, 브랜치, 히스토리 정보 등)
- HEAD파일 : 현재 체크아웃된 브랜치를 가리킴
- 실제 코드 파일들 : src/, README.md, package.json 같은 원격 저장소의 파일들이 로컬 디렉토리의 배치됨