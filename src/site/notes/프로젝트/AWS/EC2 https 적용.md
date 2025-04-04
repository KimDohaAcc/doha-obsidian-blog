---
{"dg-publish":true,"permalink":"/프로젝트/AWS/EC2 https 적용/","dgPassFrontmatter":true}
---


EC2 인스턴스  개설 
도메인 구매(gabia에서 사도 되고 AWS에서 구매해도 됨)
#### Route 53
인증서를 발급하기 앞서 Route53에 내가 도메인 소유자임을 인증

###### 호스팅 영역 생성
도메인 이름 : 구매한 도메인명 -> 나머지 default로 도메인 생성

###### 네임서버
생성한 호스팅 영역을 클릭하면 레코드가 총 4개 있는데
가비아의 도메인 네임서버를 방금 생성한 도메인 영역의 것으로 바꿔줘야 함
가비아 - 도메인 관리 - 네임서버 설정 - 호스트 명을 라우팅 대상에 모두 넣어주기 - 소유자 인증

#### ACM 인증서 발급
Certificate Manager - 인증서 요청 - 퍼블릭 인증서 요청 - 구매한 도메인 입력
검증 방법 - DNS 검증
키 알고리즘 - RSA 2048
인증서를 요청하고 나면 아직 검증 되지 않아서 검증 대기중 / 아니요 / 부적격 이 나오게 됨

도메인 - Route53에서  DNS 레코드 생성 - 도메인을 체크

시간이 지나면 인증서 상태가 발급됨으롤 변경됨(20분~2시간 정도 걸림)

###### 보안그룹 설정
인바운드 규칙 편집 - 8080, 443 포트에 대해 IPv4, IPv6을 모두 등록
###### 대상 그룹 설정
타깃 그룹 생성 - 인스턴스 - 타깃 그룹 이름 설정 - HTTP 프로토콜 8080 포트 - VPC는 EC2와 동일하게 설정

###### 타깃 등록
사용할 인스턴스 체크 - 타깃이 추가되면 타깃 그룹 생성

#### 로드밸런서 설정
로드밸런서 : 클라이언트와 서버 그룹 사이에 위치해 서버에 가해지는 트래픽을 여러 대의 서버에 고르게 분배하여 특정 서버의 부하를 덜어준다. 이 문제를 해결하기 위해 스케일 업과 스케일 아웃 방식 중 한 가지를 사용해 해결

스케일 업 : 기존 서버 성능을 향상시키는 방법
스케일 아웃 : 트래픽이나 작업을 여러 대의 컴퓨터나 서버에 분산시켜 처리하는 방법

EC2의 로드밸런서는 타깃 그룹을 생성하여 들어오는 요청을 알고리즘에 따라 각 타깃 그룹에 분산시켜 보낸다(HTTP 요청 -> HTTPS 로 리다이렉션)

###### 로드밸런서 생성
ALB - 로드밸런서 이름 - EC2의 VPC 선택 - 맵핑 : 해당되는 지역으로 최소 2개 이상 선택 - 보안그룹은 EC2와 동일하게 선택 
HTTP 8080 과 HTTPS 443 의 리스너를 생성
Default SSL/TLS 인증 - 생성한 ACM 인증서 적용 - 로드밸런서 생성하기

#### 도메인 레코드 생성
###### Route53 레코드 생성
레코드 이름 설정 안 해도 됨 - 별칭 체크 - 트래픽 라우팅 대상을 위에서 생성한 로드밸런서로 지정 - 레코드 생성

#### 로드밸런서 리스너 규칙 추가
###### 443 포트
연결 대상 : 도메인 서버로 설정
###### 8080 포트
호스트 헤더에 도메인 주소를 입력하고 리디렉션 대상으로 HTTPS 443 을 넣어줌 - 영구 이동

###### 헬스 체크
응답을 200으로 보내는 API를 만들어 주소를 넣어주기