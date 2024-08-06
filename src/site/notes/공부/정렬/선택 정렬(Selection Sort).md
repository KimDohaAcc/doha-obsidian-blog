---
{"dg-publish":true,"permalink":"/공부/정렬/선택 정렬(Selection Sort)/","dgPassFrontmatter":true}
---

![image 2.gif](/img/user/%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC/image%202.gif)
배열에서 가장 작은 값을 찾아 첫 번째 원소와 교환한 후, 그 다음으로 작은 값을 두 번째 원소와 교환하는, ==n번째 작은 값을 찾아 n번째 원소와 교환==하는 방식의 정렬

불안정 정렬로 분리된다

#### 시간 복잡도
최선, 평균, 최악 모두 **O(N^2)** 이다
배열이 정렬되어 있더라도 확인하기 때문이다

#### 공간 복잡도
주어진 배열 외에 다른 공간이 필요하지 않으므로 **O(N)** 이다

#### 코드
```java
import java.util.Arrays;

// 선택 정렬
public class SelectionSort {

    public static void main(String[] args) {
        int[] number = {15,3,23,64,77,46,42,174,68,78,91,5,76,310,84,342,176,120,33,41};

        // swap 할 공간
        int temp;

        for (int i = 0; i < number.length-1; i++) {			// 1
            int indexMin = i;
            for (int j = i+1; j < number.length; j++) {		// 2
                // > 내림차순, < 오름차순
                if(number[j] < number[indexMin]) {			// 3
                    indexMin = j;
                }
            }
            
            // 4
            temp = number[indexMin];
            number[indexMin] = number[i];
            number[i] = temp;
        }

        System.out.println(Arrays.toString(number));
    }
}
```