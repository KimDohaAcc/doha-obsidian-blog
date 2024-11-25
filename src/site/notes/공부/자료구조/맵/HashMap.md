---
{"dg-publish":true,"permalink":"/공부/자료구조/맵/HashMap/","dgPassFrontmatter":true}
---


[[공부/자료구조/맵/Map\|Map]] 인터페이스를 구현한 대표적인 컬렉션
이름 그대로 [[공부/SW/해싱(Hashing)\|해싱(Hashing)]] 을 사용하기 때문에 ==많은 양의 데이터를 검색하는 데 있어서 뛰어난 성능==을 보인다

HashMap은 [[공부/SW/해시 함수\|해시 함수]]를 통해 key와 value가 저장되는 위치를 결정하므로, 사용자는 그 위치를 알 수 엇고 삽입되는 순서와 들어 있는 위치 또한 관계가 없다(삽입한 순서에 따라 정렬되지 않는다!)

#### 구성
HashMap은 내부적으로 Entry<K,V>[] Entry Array로 구성되어 있다. 즉 ==Array의 index==를 hash 함수를 통해 계산한다

![Pasted image 20240302181830.png](/img/user/첨부파일/Pasted image 20240302181830.png)

이처럼 Entry로 저장이 되는데, 내부적인 해시값에 의해 어떤 bucket에 담길지 결정된다
#### 시간복잡도
입력과 삭제에 대해 시간복잡도가 O(1)이다

#### 선언
HashMap은 저장공간보다 값이 추가로 들어오면 List 와 같이 저장공간을 추가로 늘리지만, List와 다르게 한 칸이 아니라 **약 두 배로 늘리기 때문에** 여기서 과부하가 많이 발생한다. 따라서 초기에 저장할 데이터 개수를 알고 있다면 초기 용량을 지정해주는 것이 좋다
```java
HashMap<String,String> map = new HashMap<>(10);//초기 용량(capacity)지정
```

#### 활용
##### entrySet() 활용
```java
for(Map.Entry<Integer,String> entry : hm.entrySet()) {
    System.out.println("Key :" + entry.getKey() + " Value :" + entry.getValue());
}//출력결과
//Key :1 Value :One
//Key :2 Value :Two
//Key :3 Value :Three
//Key :4 Value :Four
```

##### keySet() 활용
```java
//keySet() 활용
for (int i : hm.keySet()) {
    System.out.println("Key :" + i + " Value :" + hm.get(i));
}//출력결과
//Key :1 Value :One
//Key :2 Value :Two
//Key :3 Value :Three
//Key :4 Value :Four
```

##### 전체 출력
반복문 대신 Iterator를 사용할 수 있다

```java
Iterator<Integer> keys = map.keySet().iterator();
while(keys.hasNext()){
    int key = keys.next();
    System.out.println("[Key]:" + key + " [Value]:" +  map.get(key));
}
//[Key]:1 [Value]:사과
//[Key]:2 [Value]:바나나
//[Key]:3 [Value]:포도
```

##### getOrDefault()
key와 defaultValue를 파라미터로 받는 메소드로, 지정된 key에 매핑된 value가 없거나 null이면 defaultValue를 기본값으로 HashMap에 key를 새로 만든다

```java
hm.put("파인애플", hm.getOrDefault("파인애플",0)+1);
System.out.println(hm.get("파인애플")); // 출력결과 : 1
```