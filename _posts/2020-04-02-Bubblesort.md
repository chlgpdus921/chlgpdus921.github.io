---
title:  "[SORT] Bubble Sort (버블 소트)"
excerpt: "Bubble sort 개념 및 시간복잡도"
permalink: /algorithm/sort/bubble
comments: true

categories:
  - Algorithm
tags: 
  - bublle sort
  - sort
  - Alogorithm
last_modified_at:  2019-04-02 16:56:00 +0000
---

### Goal

> - 정렬 알고리즘 중 Bubble Sort 에 대해 알기
> - Bubble Sort의 장· 단점 
> - 시간 복잡도 이해하기 
> - 자바로 구현할 줄 알기



## Bubble Sort (버블 소트) 알고리즘

두개의 값을 계속 비교해 나아가면서 값을 정렬시키는 알고리즘이다. 

아래 예시를 통해 이해해 보자 

#### PASS 1  -  왼쪽 값과 오른쪽 값을 비교한다. 

#### 			  -  왼쪽 값이 오른쪽 값보다 더 크다면, 두 개의 값을 바꾼다. 

![](https://chlgpdus921.github.io/assets/images/bubblesort/그림1.png)








#### PASS 2  다시 배열의 처음으로 가서 이를 계속 반복한다. 

![](https://chlgpdus921.github.io/assets/images/bubblesort/그림2.png)





---

## Bubble Sort (버블 소트) 의 장 · 단점

- 장점 :
  - 구현이 단순하다. 

- 단점 :
  - 가장 왼쪽에서 가장 오른쪽으로 이동하기 위해서는 배열의 모든 요소들과 교환이 이루어져야한다. 
  - 교환하는 것보다 이동 작업이 더 많기 때문에 거의 쓰이지 않는다. 

---

## Bubble Sort (버블 소트) 의 시간복잡도

### Bubble Sort  :   O(n^2) 

- 데이터 개수 n 개일 때.
  - 전체 합 :  (n-1) + (n-2) + (n-3) + ..... + 2 + 1 =>  n(n-1) / 2*



#### 결과 :  

#### - 데이터가 n 개일 때 걸리는 시간 복잡도는 O(n^2) 입니다. 



---

### Bubble Sort (버블 소트)  JAVA 구현

```java
public class BubbleSort {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();

		int n = Integer.valueOf(br.readLine());
		int[] arr = new int[n];
		for (int i = 0; i < n; i++) {
			arr[i] = Integer.valueOf(br.readLine());
		}

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n - 1 - i; j++) {
				if (arr[j] > arr[j + 1]) {
					int temp = arr[j];
					arr[j] = arr[j + 1];
					arr[j + 1] = temp;
				}
			}
			sb.append("PASS " + (i + 1) + " : ");
			for (int k = 0; k < n; k++) {
				sb.append(arr[k] + " ");
			}
			sb.append("\n");
		}
		for (int i = 0; i < n; i++) {
			sb.append(arr[i] + " ");
		}
		System.out.println(sb);
	}
}
```


#### 윗 예시를 코드를 통해 똑같이 적용.

#### n = 6,  array = [5, 10, 8, 6, 1, 3]

![](https://chlgpdus921.github.io/assets/images/bubblesort/result.PNG)



