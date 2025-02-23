---
{"dg-publish":true,"permalink":"////tree-map/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/SW/자료구조/맵/TreeMap/","dgPassFrontmatter":true}
---

[[공부/자료구조/트리/이진 트리(Binary Tree)\|이진 트리]]를 기반으로 한 Map 컬렉션

객체를 저장하면 자동으로 정렬되며, **키는 저장과 동시에 자동으로 오름차순 정렬**된다

>[!tip]
>- 숫자(Integer, Double) 타입일 경우에는 값으로 정렬하고
>- 문자열(String) 타입일 경우에는 유니코드로 정렬한다.

TreeMap은 SortedMap 인터페이스를 구현하고 있어, 데이터를 저장할 때 즉시 정렬하기에 **HashMap보다 오래 걸린다**

하지만 정렬된 상태롤 Map을 유지해야 하거나, 정렬된 데이터를 조회해야 한다면 효율적이다

TreeMap은 내부에 [[공부/자료구조/트리/레드-블랙 트리(Red-Black Tree)\|레드-블랙 트리(Red-Black Tree)]] 자료구조를 이용하고 있다

#### 활용

##### 최대, 최소
항상 정렬이 되어있기 때문에 최솟값, 최댓값을 바로 가져오는 메소드를 지원한다

```java
System.out.println(map.firstEntry());//최소 Entry 출력 : 1=사과
System.out.println(map.firstKey());//최소 Key 출력 : 1
System.out.println(map.lastEntry());//최대 Entry 출력: 3=수박
System.out.println(map.lastKey());//최대 Key 출력 : 3
```

##### 정렬 순서 변경
NavigableMap을 상속 받았기에 오름차순과 내림차순으로 번갈아가며 정렬 순서를 바꾸는 **descendingMap()** 메소드를 제공한다.

```java
NavigableMap<Integer, String> desc = tMap.descendingMap();
```

Comparator를 생성자의 매개값으로 넣어서 정렬하는 것도 가능하다

```java
TreeMap<K ,V> treeMap = new TreeMap<K, V>(new Comparator<Fruit> {
    @Override
    public int compare(Fruit o1, Fruit o2) {
        if (o1.price < o2.price) return 1;
        else if (o1.price == o2.price) return 0;
        else return -1;
    });
```