---
{"dg-publish":true,"permalink":"//spring/annotation/message-mapping/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/Spring/Annotation/@MessageMapping/","dgPassFrontmatter":true}
---

[[공부/SW/웹소켓/Websocket\|Websocket]] 엔드포인트에서 클라이언트로부터 오는 메시지를 처리하는 어노테이션
[[공부/SW/웹소켓/STOMP(Simple Text Oriented Messaging Protocol)\|STOMP(Simple Text Oriented Messaging Protocol)]]를 지원하는데 사용되며, 해당 메소드가 메세지를 처리하게 설정한다

[[공부/Spring/Annotation/@SendTo\|@SendTo]] 어노테이션은 클라이언트에 응답을 보낼 대상 토픽을 지정한다

````java
@Controller
public class WebSocketController { 

	@MessageMapping("/hello") 
	@SendTo("/topic/greetings") 
	public Greeting handleHelloMessage(HelloMessage message) { 
	// 클라이언트로부터 받은 메시지를 처리하고 응답을 생성
	return new Greeting("Hello, " + message.getName() + "!"); 
	} 
}
```