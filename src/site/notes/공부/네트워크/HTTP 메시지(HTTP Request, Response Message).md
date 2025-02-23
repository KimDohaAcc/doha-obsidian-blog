---
{"dg-publish":true,"permalink":"/공부/네트워크/HTTP 메시지(HTTP Request, Response Message)/","dgPassFrontmatter":true}
---


# Request Message

![Pasted image 20240902141338.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240902141338.png)

HTTP Request Message는 공백 라인을 제외하고 Start Line, Headers, Body로 나눠진다

#### Start Line

HTTP method
Request target
HTTP version
으로 이루어진다

#### Headers

Request에 대한 추가 정보를 담고 있다
Host : 요청하려는 서버 호스트 이름과 포트 번호
Accept : 처리 가능한 미디어 타입
등을 포함하고 있다

#### Body

전송하는 데이터를 담고 있는 부분

```
{
    "test_id": "tmp_123",
    "order_id": "001"
}

```

![Pasted image 20240902141839.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240902141839.png)

# Response Message

공백 라인을 제외하고 Status Line, Headers, Body 3가지 부분으로 나눠진다

#### Status Line

HTTP version
Status Code
Status Text

로 이루어진다

#### Headers, Body

Request와 거의 동일하다