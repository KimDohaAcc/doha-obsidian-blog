---
{"dg-publish":true,"permalink":"//java/string-builder/","dgPassFrontmatter":true}
---


String : **변경 불가능한** 문자열 생성(불변 객체)
만일 더하기 연산을 한다면 새로운 String이 생성된다
-> 메모리 할당과 메모리 해제를 발생시키며 성능적으로 좋지 않음

StringBuilder : **변경 가능**한 문자열을 만들어 주기 때문에 다양한 작업을 할 수 있다. 더하기 연산 시 새로운 객체를 생성하는 것이 아니라 **기존의 데이터에 더하는 방식을 사용하기 때문에** 속도도 빠르고 상대적으로 부하가 적다
-> 따라서 긴 문자열을 더하는 상황이 발생한다면 StringBuilder를 적극적으로 사용하기!

#### 주요 메소드
append() : 문자열 추가
insert()
replace()
substring()
deleteCharAt()
delete()
reverse() : 해당 문자를 전체 뒤집기
setCharAt()
trimToSize() : 문자열이 저장된 char[] 배열 사이즈를 현재 문자열 기리와 동일하게 조정