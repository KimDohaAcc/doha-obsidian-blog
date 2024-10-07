---
{"dg-publish":true,"permalink":"/공부/알고리즘/LIS(Longest Increasing Subsequence) 알고리즘/","dgPassFrontmatter":true}
---

==최장 증가 부분 수열==을 구하는 알고리즘

{ 6, **2**, **5**, 1, **7**, 4, **8**, 3} 이라는 배열이 있다면, LIS는 {2, 5, 7, 8} 이 된다.

#### DP LIS

>[!note]
>시간복잡도 : **O(N^2)**
>정확한 원소 구하기 **가능**

일반적으로 LIS는 [[공부/알고리즘/DP(Dynamic Programming)\|DP(Dynamic Programming)]]를 사용해서 구한다
외부 반복문으로 N개의 수열을 순서대로 돌면서,
내부 반복문으로 0~i-1까지 확인하며 dp를 갱신하는 방식이다

```java
for (int k = 0; k < n; k++){
	length[k] = 1;
    for (int i = 0; i < k; i++){
        if(arr[i] < arr[k]){
            length[k] = max(length[k], length[i] + 1);
        }
    }
}
```

이렇게 알고리즘을 구성했을 때 시간복잡도는 *O(N^2)* 이 된다
N의 크기가 작은 LIS 문제에 사용할 수 있다

#### 이분탐색 LIS

>[!note]
>시간복잡도 : **O(Nlog(N))**
>정확한 원소 구하기 **불가능** -> 길이 파악 O

시간복잡도를 개선하기 위해 이분탐색으로 LIS를 찾을 수 있다
![Pasted image 20240927141648.png](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/Pasted%20image%2020240927141648.png)

```java
int[] nums = {2, 1, 3, 5, 4};
int[] lis = new int[N];
int length = 0;

for(int i = 0; i < N; i ++) {
	int num = nums[i]
	int pos = binarySearch(num, 0, length, lis);
	lis[pos] = num;

	if (pos == length) length ++;
}

System.out.println(length);


// binarySearch
public static int binarySearch(int num, int start, int end, int[] lis) {
	while (start < end) {
		int mid = start + (end - start) / 2;

		// 타깃이 기준보다 크다면
		if (lis[mid] < num) start = mid = 1;
		// 타깃이 기준보다 작거나 같다면
		else end = mid;
	}

	return end;
}
```

이렇게 알고리즘을 구성했을 때 시간복잡도는 *O(nlogn)* 이다
시간복잡도 측면에서 이점이 있지만, DP 풀이와 다르게 ==정확한 LIS 원소를 구할 수 없다==

###### 왜 정확한 원소를 찾을 수 없어요?

왜냐하면 이분 탐색 시 LIS 배열을 *덮어쓰는 방식*으로 갱신하기 때문이다

가령 `[1, 3, 5, 7, 9, 2, 4]` 배열이 있다고 해보자
이 수열에서 최장 증가 부분 수열은 `1, 3, 5, 7, 9`이다

원소 5개를 탐색했다면,
`| 1 | 3 | 5 | 7 | 9 |`
LIS 배열에는 이렇게 저장되었을 것이다

이 다음 `2`를 탐색한다면
`| 1 | 2 | 5 | 7 | 9 |`
이렇게 갱신되며,

마지막 원소인 `4`를 탐색하고 나면
`| 1 | 2 | 4 | 7 | 9 |`
최종적으로 LIS 배열은 이렇게 구성되어 있다

기존의 `1, 3, 5, 7, 9` 5개의 최장 증가 수열을 `1, 2, 4`가 넘지 못해서
최장 수열의 길이는 정확하게 5로 구할 수 있지만, 탐색 시 배열이 갱신되어 정확한 원소가 아니게 된다

==따라서 O(NlogN) 시간복잡도를 가지면서도 정확한 원소를 구하기 위해서는 다른 방법이 필요하다==

#### DP + 이분탐색 LIS

>[!note]
>시간복잡도 : **O(Nlog(N))**
>정확한 원소 구하기 **가능**

두 방식의 장점을 합쳐놓았다고 생각하면 된다

```java
int[] dp = new int[N];  
int[] lis = new int[N];  

int length = 0;  
for (int i = 0; i < N; i++) {  
	int num = nums[i];  
	int pos = binarySearch(lis, 0, length, num);  
	lis[pos] = num;  
	dp[i] = pos;  

	if (pos == length) length++;  
}  

System.out.println(length);  

int[] res = new int[length];  
length--;  
for (int i = N - 1; i >= 0; i--) {  
	if (dp[i] == length) {  
		res[length] = nums[i];  
		length--;  
	}  
}  

for (int num : res) {  
	System.out.print(num + " ");  
}  


// binarySearch
public static int binarySearch(int[] lis, int start, int end, int target) {  
    while (start < end) {  
        int mid = start + (end - start) / 2;  
  
        if (lis[mid] < target) start = mid + 1;  
        else end = mid;  
    }  
  
    return start;  
}
```

똑같이 이분탐색을 수행하지만, *메모이제이션*을 활용해 dp 배열에 **해당 숫자의 이분 탐색 결과를 저장**하는 것에서 차이가 있다

가령 `1, 3, 5, 7, 9, 2, 4` 수열이 있다고 하자
이분탐색을 진행하며 *현재 LIS 배열 어느 자리에 들어가야 하는지* 를 dp 배열에 저장하면

  `1, 3, 5, 7, 9, 2, 4`
`[0, 1, 2, 3, 4, 1, 2]`

dp 배열은 이렇게 구성될 것이다

이 다음 할 일은 간단하다
length에는 가장 긴 수열의 길이(=5)가 저장되어 있다
반복문을 통해 수열을 맨 뒤에서부터 탐색하며 length - 1(=4)를 찾아낸다

길이가 4가 된 지점은 `nums[dp[4가 저장된 idx]] = 9`이다
`9`를 찾았다면 길이 변수에 저장된 값을 -1한다

그후 길이가 3이 된 지점은 숫자 `7`이다
`7`을 찾았다면 길이 변수에 저장된 값은 -1 하고 이를 끝까지 반복한다면
`9, 7, 5, 3, 1`을 순서대로 찾게 된다

이를 역순으로 출력하면 정확한 수열을 구할 수 있다
