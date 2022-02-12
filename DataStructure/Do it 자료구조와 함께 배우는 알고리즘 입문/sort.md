## 목차
1. [버블 정렬](#버블-정렬)  
2. [단순 삽입 정렬](#단순-삽입-정렬)
3. [셸 정렬](#셸-정렬)
4. [퀵 정렬](#퀵-정렬)

</br>  

# 정렬이란 ?

이름,학번,키 등 핵심 항목의 대소 관계에 따라 데이터 집합을 일정한 순서로 줄지어 늘어서도록 바꾸는 작업.  

## 버블 정렬  

 요소의 개수가 n개인 배열에서 n-1회 비교, 교환을 하고 나면 가장 작은 요소가 맨 처음으로 이동한다. 수행하는 패스의 횟수가 n회가 아니라 n-1회 인것은 n-1개 요소의 정렬이 끝나면 마지막 요소는 이미 끝에 놓이기 때문

버블정렬 이라는 말은 액체 안의 공기 방울이 보글보글 위로 올라오는 모습에서 착안

### 실습6-1

```java
import java.util.Scanner;

class BubbleSort {
    static void swap(int[] a, int idx1, int idx2) {
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = t;
    }

    //버블 정렬
    static void bubbleSort(int[] a, int n) {
        for (int i = 0; i < n - 1; i++)
            for (int j = n - 1; j > i; j--)
                if (a[j - 1] > a[j])
                    swap(a, j - 1, j);
    }

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);

        System.out.println("버블 정렬(버전1)");
        System.out.println("요소수 :");
        int nx = stdIn.nextInt();
        int[] x = new int[nx];

        for (int i = 0; i > nx; i++) {
            System.out.println("x[" + i + "]: ");
            x[i] = stdIn.nextInt();
        }

        bubbleSort(x, nx);

        System.out.println("오름차순으로 정렬했습니다.");
        for (int i = 0; i < nx; i++)
            System.out.println("x[" + i + "]=" + x[i]);
    }
}
```

```java
버블 정렬(버전1)
요소수 :
7
x[0]: 
22
x[1]: 
5
x[2]: 
11
x[3]: 
32
x[4]: 
120
x[5]: 
68
x[6]: 
70
오름차순으로 정렬했습니다.
x[0]=5
x[1]=11
x[2]=22
x[3]=32
x[4]=68
x[5]=70
x[6]=120
```

| i = 0 | j = 5 | if( a[5] > a[6] ) |
| --- | --- | --- |
|  | j = 4 | if( a[4] > a[5] ) |
|  | j = 3 | if( a[3] > a[4] ) |
|  | j = 2 | if( a[2] > a[3] ) |
|  | j = 1 | if( a[1] > a[2] ) |
|  |  |  |
| i = 1 | j = 5 | if( a[5] > a[6] ) |
|  | j = 4 | if( a[4] > a[5] ) |
|  | j = 3 | if( a[3] > a[4] ) |
|  | j = 2 | if( a[2] > a[3] ) |
|  |  |  |
| i =2 | j = 5  | if( a[5] > a[6] ) |
|  | j = 4 | if( a[4] > a[5] ) |
|  | j = 3 | if( a[3] > a[4] ) |
|  |  |  |
| i = 3 | j = 5 | if( a[5] > a[6] ) |
|  | j = 4 | if( a[4] > a[5] ) |
|  |  |  |

### 실습6-2  

정렬을 마친 배열이나 정렬이 거의 다 된 상태의 배열에 대한 연산 생략  

개선한 버블 정렬  

- 정렬하는데 시간이 줄어든다.

```java
// 버블 정렬
	static void bubbleSort(int[] a, int n) {
		for (int i = 0; i < n; i++) {
			int exchg = 0;
			for (int j = n - 1; j > i; j--)
				if (a[j - 1] > a[j]) {
					swap(a, j - 1, j);
					exchg++;
				}
		}
	}
```

| i = 0 | j = 5 | if( a[5] > a[6] ) | exchg = 1 |
| --- | --- | --- | --- |
|  | j = 4 | if( a[4] > a[5] ) | exchg = 2 |
|  | j = 3 | if( a[3] > a[4] ) | exchg = 3 |
|  | j = 2 | if( a[2] > a[3] ) | exchg = 4 |
|  | j = 1 | if( a[1] > a[2] ) | exchg = 5 |
|  |  |  |  |
| i = 1 | j = 5 | if( a[5] > a[6] ) | exchg = 1 |
|  | j = 4 | if( a[4] > a[5] ) | exchg = 2 |
|  | j = 3 | if( a[3] > a[4] ) | exchg = 3 |
|  | j = 2 | if( a[2] > a[3] ) | exchg = 4 |
|  |  |  |  |
| i = 2 | j = 5 | if( a[5] > a[6] ) | exchg = 1 |
|  | j = 4 | if( a[4] > a[5] ) | exchg = 2 |
|  | j = 3 | if( a[3] > a[4] ) | exchg = 3 |
|  |  |  |  |
| i = 3 | j = 5 | if( a[5] > a[6] ) | exchg = 1 |
|  | j = 4 | if( a[4] > a[5] ) | exchg = 2 |
|  |  |  |  |
| i = 4 | j = 5 | if( a[5] > a[6] ) | exchg = 1 |  



### 실습6-3

어떤 시점 이후에 교환이 수행되지 않는다면 그보다 앞쪽의 요소는 이미 정렬을 마친 상태. 따라서 두번째 패스는 첫 요소를 제외한 6개의 요소가 아니라 4개의 요소에 대해서 비교,교환을 수행.

- last 는 각 패스에서 마지막으로 교환한 두 요소 가운데 오른 쪽 요소의 인덱스를 저장하기 위한 변수. 교환을 수행할 때 마다 오른쪽 요소의 인덱스 값을 last에 저장.
- 하나의 패스를 마쳤을때 last값을 k에 대입하여 다음에 수행할 패스의 범위를 제한
- 다음 패스에서 마지막을 비교할 요소는 a[k]와 a[k+1]
- k값을 0으로 초기화하는 이유는 첫 번째 패스에서는 모든 요소를 검사해야한다.

```java
// 버블 정렬
	static void bubbleSort(int[] a, int n) {
		int k = 0;//a[k]보다 앞쪽은 정렬을 마친 상태
		while (k < n - 1) {
			int last = n - 1;//마지막으로 요소를 교환한 위치
			for (int j = n - 1; j > k; j--)
				if (a[j - 1] > a[j]) {
					swap(a, j - 1, j);
					last = j;
				}
			k = last;
		}
	}
```

</br>  


## 단순 선택 정렬

가장 작은 요소부터 선택해 알맞은 위치로 옮겨서 순서대로 정렬

### 실습6-4

```java
static void selectionSort(int[] a, int n) {
		for(int i = 0 ; i < n-1 ; i++) {
			int min = i;
			for(int j = i + 1 ;j < n ; j++)
				if(a[j] < a[min])
					min = j;
				swap(a,i,min);
		}
	}
```



## 단순 삽입 정렬

선택한 요소를 그보다 더 앞쪽의 알맞은 위치에 삽입하는 작업을 반복하여 정렬

2번째 요소부터 선택하여 진행

### 실습6-5
- 정렬된 열의 왼쪽끝에 도달한다.
- tmp 보다 작거나 같은 key를 갖는 항목 a[j]를 발견한다.
- 드모르간 법칙 적용
 - j가 0 보다 크다
 - a[j-1]값이 tmp보다 크다 

```java
static void insertSort(int[] a, int n) {
		for(int i = 1; i < n ; i++) {
			int j;
			int tmp = a[i];
			for(j = i ; j > 0 && a[j - 1] > tmp; j--)
				a[j] = a[j-1];
			a[j] = tmp;
		}
	}
```

## 셸 정렬

단순 삽입 정렬의 장점은 살리고 단점은 보완

### 실습6-6

```java
static void sellSort(int[] a, int n) {
		for(int h = n /2 ; h > 0 ; h /= 2)
			for(int i = h; i < n ; i++) {
				int j;
				int tmp = a[i];
				for(j = i - h ; j >= 0 && a[j] > tmp; j -= h)
					a[j + h] = a[j];
				a[j + h] = tmp;
			}
	}
```

### 실습6-7

```java
// 셸정렬
	static void shellSort(int[] a, int n) {
		int h;
		for (h = 1; h < n / 9; h = h * 3 + 1)
			;

		for ( ; h > 0; h /= 3)
			for (int i = h; i < n; i++) {
				int j;
				int tmp = a[i];
				for (j = i - h; j >= 0 && a[j] > tmp; j -= h)
					a[j + h] = a[j];
				a[j + h] = tmp;
			}
	}
```

</br>

## 퀵 정렬

가장 빠른 정렬 알고리즘 중 하나

### 실습6-8

배열 가운데에 있는 요소를 피벗으로 정하고 그룹을 나눈다.

```java
package chap06;
import java.util.Scanner;
// 배열을 나눕니다.

class Partition {
	// 배열 요소 a[idx1]과 a[idx2]의 값을 바꿉니다. 
	static void swap(int[] a, int idx1, int idx2) {
		int t = a[idx1];  
		a[idx1] = a[idx2];  
		a[idx2] = t;
	}

	// 배열을  나눕니다.  
	static void partition(int[] a, int n) {
		int pl = 0;			// 왼쪽 커서
		int pr = n - 1;		// 오른쪽 커서
		int x = a[n / 2];	// 피벗 (가운데 위치의 값）

		do {
			while (a[pl] < x) pl++;
			while (a[pr] > x) pr--;
			if (pl <= pr)
				swap(a, pl++, pr--);
		} while (pl <= pr);

		System.out.println("피벗의 값은 " + x + "입니다.");

		System.out.println("피벗 이하의  그룹");
		for (int i = 0; i <= pl - 1; i++)			// a[0] ~ a[pl - 1]
			System.out.print(a[i] + " ");
		System.out.println();

		if (pl > pr + 1) {
			System.out.println("피벗과 일치하는 그룹");
			for (int i = pr + 1; i <= pl - 1; i++)	// a[pr + 1] ~ a[pl - 1]
				System.out.print(a[i] + " ");
			System.out.println();
		}

		System.out.println("피벗 이상의 그룹");
		for (int i = pr + 1; i < n; i++)			// a[pr + 1] ~ a[n - 1]
			System.out.print(a[i] + " ");
		System.out.println();
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("배열을  나눕니다.");
		System.out.print("요솟수：");
		int nx = stdIn.nextInt();
		int[] x = new int[nx];

		for (int i = 0; i < nx; i++) {
			System.out.print("x[" + i + "]：");
			x[i] = stdIn.nextInt();
		}
		partition(x, nx);				// 배열 x를 나눕니다.
	}
}
```

### 실습6-9

재귀 호출 사용하여 구현

quickSort메서드는 배열 a, 나눌 구간의 첫번째 요소(left), 마지막 요소(right)의 인덱스를 매개변수로 받는다.

```java
package chap06;
import java.util.Scanner;
// 퀵 정렬

class QuickSort {
	// 배열 요소 a[idx1]과 a[idx2]의 값을 바꿉니다.
	static void swap(int[] a, int idx1, int idx2) {
		int t = a[idx1];  a[idx1] = a[idx2];  a[idx2] = t;
	}

	// 퀵 정렬
	static void quickSort(int[] a, int left, int right) {
		int pl = left;					// 왼쪽 커서
		int pr = right;					// 오른쪽 커서
		int x = a[(pl + pr) / 2];		// 피벗

		do {
			while (a[pl] < x) pl++;
			while (a[pr] > x) pr--;
			if (pl <= pr)
				swap(a, pl++, pr--);
		} while (pl <= pr);

		if (left < pr)  quickSort(a, left, pr);
		if (pl < right) quickSort(a, pl, right);
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("퀵 정렬");
		System.out.print("요솟수：");
		int nx = stdIn.nextInt();
		int[] x = new int[nx];

		for (int i = 0; i < nx; i++) {
			System.out.print("x[" + i + "]：");
			x[i] = stdIn.nextInt();
		}

		quickSort(x, 0, nx - 1);			// 배열 x를 퀵 정렬

		System.out.println("오름차순으로 정렬했습니다.");
		for (int i = 0; i < nx; i++)
			System.out.println("x[" + i + "]＝" + x[i]);
	}
}
```
