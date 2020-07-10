---
title:  "[SORT] Insertion Sort (삽입 정렬)"
excerpt: "Insertion sort 특징 및 시간복잡도"
permalink: /algorithm/sort/insertion
comments: true

categories:
  - Algorithm
tags: 
  - Sort
toc: true
toc_sticky: true
last_modified_at:  2020-04-02 20:00:00 +0000
---

## Goal

> - 정렬 알고리즘 중 Insertion Sort 에 대해 알기
> - Insertion Sort의 장· 단점 
> - 시간 복잡도 이해하기 
> - 자바로 구현할 줄 알기



## Insertion Sort (삽입 정렬) 알고리즘

" 순서대로 뽑고, 적당한 위치에 삽입"

배열의 모든 요소를 왼쪽의 모든 요소들과 비교하여 지정 자리에 자료를 삽입하면서 정렬하는 알고리즘.



아래 예시를 통해 이해해 보자. 

- 두번째 data 부터 시작할 것

   

### PASS 1  -  왼쪽 값과 오른쪽 값을 비교한다. 

- 왼쪽 데이터 값과 오른쪽 데이터 값(처음 상태: 두번 째 data 값)을 비교한다.
- 왼쪽 데이터 값이 더 크다면, 오른쪽 값과 비교한다. 
- 왼쪽 데이터 값이 존재하지 않을 때까지, 비교 후 삽입 반복
- 왼쪽에 데이터가 더이상 존재하지 않는다면, 현재 상태(kEY값)를 오른쪽으로 이동시킨다.

![](https://chlgpdus921.github.io/assets/images/insertionsort/그림1.png)








### PASS 2  현재 상태(KEY)가 배열의 끝에 도달할 때까지 PASS1를 반복한다. 





---

## Insertion Sort (삽입 정렬) 의 장 · 단점

- 장점 :
  - 안정적인 정렬 방법이다.
- 제자리 정렬(in-place sort) 이다. 
    -  주어진 자료 공간 이외의 공간을 사용하지 않고 정렬하는 것
  - 데이터 수가 적을 수록 유리하다.
  - 데이터가 정렬이 되어있을수록 더 효율적이다.
  - Selection Sort (선택 정렬) , Bubble Sort (버블 정렬) 보다 효율이 높다. 
  
- 단점 :
  - 데이터 상태와  데이터 크기에 따라 성능의 편차가 심하다. 

---

## Insertion Sort (삽입 정렬) 의 시간복잡도

- 최선의 경우 (Best) - 자료가 정렬되어 있을 때 

  - 비교 횟수
    - 이동 없이 1번의 비교만 이루어진다.  (ex 2,3,5,7 - 정렬되어 있는 상태일 때)
    - n-1 번 비교	
  - **O(n)**

- 최악의 경우 (Worst) - 자료가 역순일 때 

  - 비교 횟수 & 교환 횟수

    - 각 반복마다 계속해서 비교하고 교환해야 한다.  (ex 4,3,2,1)
    - (n-1) + (n-2) + (n-3) + ... + 2 + 1 = n(n-1)/2 

  - **O(n^2)**

    

---

## Insertion Sort (삽입 정렬) JAVA 구현

```java
public class InsertionSort {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();

		int n = Integer.valueOf(br.readLine());
		int[] arr = new int[n];
		for (int i = 0; i < n; i++) {
			arr[i] = Integer.valueOf(br.readLine());
		}

		for (int i = 1; i < n; i++) {
			// 현재 key 값과 key 위치 저장
			int key = arr[i];
			int keyIndex = i;
			for (int j = i - 1; j >= 0 && arr[j] > key; j--) {
				// 현재 key 값으로부터 왼쪽에 있는 모든 값들과 비교
				// 정렬이 안되어 있을 경우, arr[j]를 arr[j+1] (오른쪽)로 밀기
				arr[j + 1] = arr[j];
				keyIndex = j;

			}
			// 한 턴(pass)가 끝나면 최종 keyindex에 key값을 저장한다.
			arr[keyIndex] = key;

			sb.append("PASS " + i + " : ");
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

### 윗 예시를 코드를 통해 똑같이 적용.

### n = 6,  array = [5, 10, 8, 6, 1, 3]

![](https://chlgpdus921.github.io/assets/images/insertionsort/result1.PNG)



