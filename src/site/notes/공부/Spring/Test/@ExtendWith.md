---
{"dg-publish":true,"permalink":"/공부/Spring/Test/@ExtendWith/","dgPassFrontmatter":true}
---

Junit5의 Test에서 사용
옵션으로 @ExtendWith(SpringExtension.class)와 @ExtendWith(MockitoExtension.class)가 많이 쓰인다

SpringExtension을 이용하면 Spring TestContext Framework와 Junit5를 통합하여 사용하게 되고, MockitoExtension을 이용하면 [[공부/Spring/Test/Mockito\|Mockito]]와 관련된 MockContext 기반에서 진행이 가능하다