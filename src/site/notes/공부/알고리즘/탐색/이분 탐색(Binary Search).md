---
{"dg-publish":true,"permalink":"////binary-search/","dgPassFrontmatter":true}
---


---
{"dg-publish":true,"permalink":"/공부/알고리즘/탐색/이분 탐색(Binary Search)/","dgPassFrontmatter":true}
---

![binary-and-linear-search-animations.gif](/img/user/첨부파일/binary-and-linear-search-animations.gif)

up down 게임 같이 답을 찾는 탐색법

==이진 탐색==이라고도 한다

**정렬되어 있는** 리스트에서 탐색 범위를 **절반씩 좁혀가며** 데이터를 탐색하는 방법

이진 탐색의 조건 : 데이터가 정렬 되어있어야 한다!

변수 3개(start, end, mid)를 사용하여 찾으려는 데이터와 중간 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는다

단계마다 탐색 범위를 반으로 줄이기 떄문에 시간 복잡도는 **O(logN)** 이다


#### 예제 코드
````java
int binarySearch1(int key, int low, int high) {  
    int mid;  
  
    if(low <= high) {  
       mid = (low + high) / 2;  
  
       if(key == arr[mid]) { // 탐색 성공   
		return mid;  
       } else if(key < arr[mid]) {  
          // 왼쪽 부분 arr[0]부터 arr[mid-1]에서의 탐색   
		return binarySearch1(key ,low, mid-1);  
       } else {  
          // 오른쪽 부분 - arr[mid+1]부터 arr[high]에서의 탐색   
		return binarySearch1(key, mid+1, high);  
       }  
    }  
  
    return -1; // 탐색 실패
}
````