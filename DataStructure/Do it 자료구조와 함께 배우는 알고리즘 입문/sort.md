## 목차
1. [버블 정렬](#버블-정렬)  
2. [단순 삽입 정렬](#단순-삽입-정렬)
3. [셸 정렬](#셸-정렬)
4. [퀵 정렬](#퀵-정렬)
5. [병합 정렬](#병합-정렬)
6. [힙정렬](#힙정렬)
7. [도수정렬](#도수정렬)

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
<img src="./단순삽입.jpg.png" width="50%" height="50%">



</br>  


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
		//2회의 재귀호출
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

</br>

### 실습 6C-1

퀵 정렬을 수행하는 과정출력

```java
// 퀵 정렬
	static void quickSort(int[] a, int left, int right) {
		int pl = left;					// 왼쪽 커서
		int pr = right;					// 오른쪽 커서
		int x = a[(pl + pr) / 2];		// 피벗

		System.out.printf("a[%d]~a[%d] : {",left,right);
		for(int i = left ;i <right;i++)
			System.out.printf("%d , ",a[i]);
		System.out.printf("%d|\n",a[right]);

		do {
			while (a[pl] < x) pl++;
			while (a[pr] > x) pr--;
			if (pl <= pr)
				swap(a, pl++, pr--);
		} while (pl <= pr);

		if (left < pr)  quickSort(a, left, pr);
		if (pl < right) quickSort(a, pl, right);
	}
```

<aside>
📎 a[0]~a[8] : {5 , 8 , 4 , 2 , 6 , 1 , 3 , 9 , 7|
a[0]~a[4] : {5 , 3 , 4 , 2 , 1|
a[0]~a[2] : {1 , 3 , 2|
a[0]~a[1] : {1 , 2|
a[3]~a[4] : {4 , 5|
a[5]~a[8] : {6 , 8 , 9 , 7|
a[5]~a[6] : {6 , 7|
a[7]~a[8] : {9 , 8|

</aside>

비재귀적인 정렬

### 실습 6-10

```java
package chap06;
import java.util.Scanner;
//퀵 정렬 (비재귀 버전)

class QuickSort2 {
	// 배열 요소 a[idx1]과 a[idx2]의 값을 바꿉니다.
	static void swap(int[] a, int idx1, int idx2) {
		int t = a[idx1];  a[idx1] = a[idx2];  a[idx2] = t;
	}

	// 퀵정렬
	static void quickSort(int[] a, int left, int right) {
		//스택의 생성
		IntStack lstack = new IntStack(right - left + 1);
		IntStack rstack = new IntStack(right - left + 1);

		lstack.push(left);
		rstack.push(right);

		while (lstack.isEmpty() != true) {
			int pl = left  = lstack.pop();		// 왼쪽 커서
			int pr = right = rstack.pop();		// 오른쪽 커서
			int x = a[(left + right) / 2];		// 피벗

			do {
				while (a[pl] < x) pl++;
				while (a[pr] > x) pr--;
				if (pl <= pr)
					swap(a, pl++, pr--);
			} while (pl <= pr);

			if (left < pr) {
				lstack.push(left);				// 왼쪽 그룹 범위의 
				rstack.push(pr);				// 인덱스를 푸시합니다.
			}
			if (pl < right) {
				lstack.push(pl);				// 오른쪽 그룹 범위의 
				rstack.push(right);				// 인덱스를 푸시합니다.
			}
		}
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("퀵 정렬(비재귀 버전)");
		System.out.print("요솟수：");
		int nx = stdIn.nextInt();
		int[] x = new int[nx];

		for (int i = 0; i < nx; i++) {
			System.out.print("x[" + i + "]：");
			x[i] = stdIn.nextInt();
		}

		quickSort(x, 0, nx - 1);			// 배열 x를 퀵 정렬합니다.

		System.out.println("오름차순으로 정렬했습니다.");
		for (int i = 0; i < nx; i++)
			System.out.println("x[" + i + "]＝" + x[i]);
	}
}
```

```java
package chap06;
// int형 스택

public class IntStack {
	private int max;			// 스택의 용량
	private int ptr;			// 스택포인터
	private int[] stk;			// 스택의 본체

	// 실행시 예외：스택가 비어 있음
	public class EmptyIntStackException extends RuntimeException {
		public EmptyIntStackException() { }
	}

	// 실행시 예외：스택이 가득 참
	public class OverflowIntStackException extends RuntimeException {
		public OverflowIntStackException() { }
	}

	// 생성자
	public IntStack(int capacity) {
		ptr = 0;
		max = capacity;
		try {
			stk = new int[max];			// 스택 본체용의 배열을 생성
		} catch (OutOfMemoryError e) {	// 생성할 수 없음
			max = 0;
		}
	}

	// 스택에 x을 푸시
	public int push(int x) throws OverflowIntStackException {
		if (ptr >= max)										// 스택은 가득 참
			throw new OverflowIntStackException();
		return stk[ptr++] = x;
	}

	// 스택에서 데이터를 팝
	public int pop() throws EmptyIntStackException {
		if (ptr <= 0)										// 스택 비어 있음
			throw new EmptyIntStackException();
		return stk[--ptr];
	}

	// 스택에서 데이터를 피크
	public int peek() throws EmptyIntStackException {
		if (ptr <= 0)										// 스택 비어 있음
			throw new EmptyIntStackException();
		return stk[ptr - 1];
	}

	// 스택에서 x을 찾아서 인덱스를 반환 (찾지 못하면-1을 반환)
	public int indexOf(int x) {
		for (int i = ptr - 1; i >= 0; i--)
			if (stk[i] == x)
				return i;		// 검색 성공
		return -1;				// 검색 실패
	}

	// 스택을 비움
	public void clear() {
		ptr = 0;
	}

	// 스택의 용량을 반환
	public int capacity() {
		return max;
	}

	// 스택의 데이터 수를 반환
	public int size() {
		return ptr;
	}

	// 스택이 비어 있나?
	public boolean isEmpty() {
		return ptr <= 0;
	}

	// 스택이 가득 차 있는가?
	public boolean isFull() {
		return ptr >= max;
	}

	// 스택 내의 모든 데이터를 바닥에서 꼭대기 순서로 출력함
	public void dump() {
		if (ptr <= 0)
			System.out.println("스택이 비어 있습니다.");
		else {
			for (int i = 0; i < ptr; i++)
				System.out.print(stk[i] + " ");
			System.out.println();
		}
	}
}
```

</br> 


## 병합 정렬

배열을 앞부분과 뒷부분으로 나누어 각각 정렬한 다음 병합하는 작업을 반복하여 정렬을 수행하는 알고리즘

- 배열 a에서 선택한 요소와 배열b에서 선택한 요소를 비교하여 작은 값을 c에 저장한다.
    - 커서를 한칸 옮긴다.
- 배열b의 모든 요소를 배열c로 복사하고 배열a에는 아직 복사하지 못한 요소가 남아있는 상태 : pa를 한 칸씩 진행하면서 복사하지 않은 모든 배열 a의 요소를 배열 c에 복사한다.
- 배열a의 모든 요소를 배열c로 복사하고 배열a에는 아직 복사하지 못한 요소가 남아있는 상태 : pb를 한 칸씩 진행하면서 복사하지 않은 모든 배열 a의 요소를 배열 c에 복사한다.

### 실습 6-11

```java
package chap06;
import java.util.Scanner;
// 정렬을 마친 배열의 병합

class MergeArray {
	// 정렬을 마친 배열 a, b를 병합하여 배열 c에 저장합니다. 
	static void merge(int[] a, int na, int[] b, int nb, int[] c) {
		int pa = 0;
		int pb = 0;
		int pc = 0;

		while (pa < na && pb < nb)	// 작은 값을 저장합니다.
			c[pc++] = (a[pa] <= b[pb]) ? a[pa++] : b[pb++];

		while (pa < na)				// a에 남아 있는 요소를 복사합니다.
			c[pc++] = a[pa++];

		while (pb < nb)				// b에 남아 있는요소를 복사합니다.
			c[pc++] = b[pb++];
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		int[] a = {2, 4, 6, 8, 11, 13};
		int[] b = {1, 2, 3, 4, 9, 16, 21};
		int[] c = new int[13];

		System.out.println("두 배열의 병합");

		merge(a, a.length, b, b.length, c);	  // 배열 a와 b를 병합하여 c에 저장

		System.out.println("배열 a와 b를 병합하여 배열 c에 저장했습니다.");
		System.out.println("배열 a：");
		for (int i = 0; i < a.length; i++)
			System.out.println("a[" + i + "] = " + a[i]);

		System.out.println("배열 b：");
		for (int i = 0; i < b.length; i++)
			System.out.println("b[" + i + "] = " + b[i]);

		System.out.println("배열 c：");
		for (int i = 0; i < c.length; i++)
			System.out.println("c[" + i + "] = " + c[i]);
	}
}
```

병합 정렬

정렬을 마친 배열의 병합을 응용하여 분할 정복법에 따라 정렬하는 알고리즘을 병합 정렬이라한다.

배열의 요소 개수가 2개 이상인 경우

1. 배열의 앞부분을 병합 정렬로 정렬
2. 배열의 뒷부분을 병합 정렬로 정렬
3. 배열의 앞부분과 뒷부분을 병합

### 실습 6-12

```java
package chap06;
import java.util.Scanner;
// 병합 정렬

class MergeSort {
	static int[] buff;	// 작업용 배열

	// a[left] ~ a[right]를 재귀적으로 병합 정렬 
	static void __mergeSort(int[] a, int left, int right) {
		if (left < right) {
			int i;
			int center = (left + right) / 2;
			int p = 0;
			int j = 0;
			int k = left;

			__mergeSort(a, left, center);			// 배열의 앞부분을 병합 정렬합니다.
			__mergeSort(a, center + 1, right);		// 배열의 뒷부분을 병합 정렬합니다.

			for (i = left; i <= center; i++)
				buff[p++] = a[i];

			while (i <= right && j < p)
				a[k++] = (buff[j] <= a[i]) ? buff[j++] : a[i++];

			while (j < p)
				a[k++] = buff[j++];
		}
	}

	// 병합 정렬
	static void mergeSort(int[] a, int n) {
		buff = new int[n];				// 작업용 배열을 생성합니다.

		__mergeSort(a, 0, n - 1);		// 배열 전체를 병합 정렬합니다.

		buff = null;					// 작업용 배열을 해제합니다.
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("병합 정렬");
		System.out.print("요솟수：");
		int nx = stdIn.nextInt();
		int[] x = new int[nx];

		for (int i = 0; i < nx; i++) {
			System.out.print("x[" + i + "]：");
			x[i] = stdIn.nextInt();
		}

		mergeSort(x, nx);		// 배열 x를 병합 정렬합니다.

		System.out.println("오름차순으로 정렬했습니다.");
		for (int i = 0; i < nx; i++)
			System.out.println("x[" + i + "]＝" + x[i]);
	}
}
```


### 실습 6-13

기본자료형 배열의 정렬(퀵정렬)

```java
package chap06;
import java.util.Arrays;
import java.util.Scanner;
// Arrays.sort 메서드를 사용하여 정렬합니다(퀵 정렬).

class ArraysSortTester {
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.print("요솟수：");
		int num = stdIn.nextInt();
		int[] x = new int[num];		// 배열의 크기는 num입니다.

		for (int i = 0; i < num; i++) {
			System.out.print("x[" + i + "]：");
			x[i] = stdIn.nextInt();
		}

		Arrays.sort(x);				// 배열 x를 정렬합니다.

		System.out.println("오름차순으로 정렬했습니다.");
		for (int i = 0; i < num; i++)
			System.out.println("x[" + i + "]＝" + x[i]);
	}
}
```

### 실습 6-14

get(MONTH)에 의해 얻은 값은 0~11이므로 화면에 출력할때는 1을 더해야한다.

```java
package chap06;
import java.util.Arrays;
import java.util.GregorianCalendar;
import static java.util.GregorianCalendar.*;
// 달력의 배열을 정렬

class SortCalendar {
	public static void main(String[] args) {
		GregorianCalendar[] x = {
			new GregorianCalendar(2017, NOVEMBER, 1),	// 2017년 11월 01일
			new GregorianCalendar(1963, OCTOBER, 18),	// 1963년 10월 18일
			new GregorianCalendar(1985, APRIL, 5),		// 1985년 04월 05일
		};

		Arrays.sort(x);  // 배열 x를 정렬

		for (int i = 0; i < x.length; i++)
			System.out.printf("%04d년 %02d월 %02d일\n", 
				x[i].get(YEAR),
				x[i].get(MONTH) + 1,
				x[i].get(DATE)
			);
	}
}
```

### 실습 6-15

```java
package chap06;
import java.util.Arrays;
import java.util.Scanner;
import java.util.Comparator;
// 신체검사 데이터 배열을 정렬합니다.

class PhyscExamSort {
	// 신체검사 데이터
	static class PhyscData {
		String name;			// 이름
		int    height;			// 키
		double vision;			// 시력

		// 생성자
		PhyscData(String name, int height, double vision) {
			this.name = name;
			this.height = height;
			this.vision = vision;
		}

		// 신체검사 데이터를 문자열로 반환합니다.
		public String toString() {
			return name + " " + height + " " + vision;
		}

		// 키 오름차순용 comparator
		static final Comparator<PhyscData> HEIGHT_ORDER = new HeightOrderComparator();

		private static class HeightOrderComparator implements Comparator<PhyscData> {
			public int compare(PhyscData d1, PhyscData d2) {
				return (d1.height > d2.height) ?  1 :
						 (d1.height < d2.height) ? -1 : 0;
			}
		}
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		PhyscData[] x = {
			new PhyscData("이나령", 162, 0.3),
			new PhyscData("전서현", 173, 0.7),
			new PhyscData("이수민", 175, 2.0),
			new PhyscData("홍준기", 171, 1.5),
			new PhyscData("유지훈", 168, 0.4),
			new PhyscData("이호연", 174, 1.2),
			new PhyscData("김한결", 169, 0.8),
		};

		Arrays.sort(x,								// 배열 x를 
						PhyscData.HEIGHT_ORDER		// HEIGHT_ORDER을 사용하여 정렬
					  );

		System.out.println("■ 신체 검사 리스트 ■");
		System.out.println(" 이름       키        시력");
		System.out.println("--------------");
		for (int i = 0; i < x.length; i++)
			System.out.printf("%-8s%3d%5.1f\n",	x[i].name, x[i].height, x[i].vision);
	}
}
```



## 힙정렬

- 가장 큰 값이 루트에 위치
- 큰 값인 루트를 꺼내는 작업을 반복
- 선택정렬 응용
- 힙으로 구성된 10개의 요소에서 가장 큰 값을 없애면 나머지 9개 요소중에서 가장 큰 값을 루트로 정한다. 따라서 나머지 9개의 요소로 만든 트리도 힙의 형태를 유지할 수 있도록 재구성해야한다.
- 루트를 없애고 힙상태 유지하기

<img src="./힙정렬.jpg" width="50%" height="50%">


### 실습 6-16

- 변수 i의 값을 n-1로 초기화한다.
- a[0]과 a[i]를 바꾼다.
- a[0],a[1],...a[i-1]를 힙으로 만든다.
- i의 값을 1씩 줄여 0이되면 끝이 난다

```java
package chap06;
import java.util.Scanner;
// 힙 정렬

class HeapSort {
	// 배열 요소 a[idx1]과 a[idx2]의 값을 바꿉니다. 
	static void swap(int[] a, int idx1, int idx2) {
		int t = a[idx1];  
		a[idx1] = a[idx2];  
		a[idx2] = t;
	}

	// a[left] ~ a[right]를 힙으로 만듭니다. 
	static void downHeap(int[] a, int left, int right) {
		int temp = a[left];				// 루트
		int child;						// 큰 값을 가진 노드
		int parent;						// 부모

		for (parent = left; parent < (right + 1) / 2; parent = child) {
			int cl = parent * 2 + 1;							// 왼쪽 자식
			int cr = cl + 1;									// 오른쪽 자식
			child = (cr <= right && a[cr] > a[cl]) ? cr : cl;	// 큰 값을 가진 노드를 자식에 대입 
			if (temp >= a[child])
				break;
			a[parent] = a[child];
		}
		a[parent] = temp;
	}

	// 힙 정렬
	static void heapSort(int[] a, int n) {
		for (int i = (n - 1) / 2; i >= 0; i--)	// a[i] ~ a[n-1]를 힙으로 만들기
			downHeap(a, i, n - 1);

		for (int i = n - 1; i > 0; i--) {
			swap(a, 0, i);				// 가장 큰 요소와 아직 정렬되지 않은 부분의 마지막 요소를 교환
			downHeap(a, 0, i - 1);		// a[0] ~ a[i-1]을 힙으로 만듭니다.
		}
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("힙 정렬");
		System.out.print("요솟수：");
		int nx = stdIn.nextInt();
		int[] x = new int[nx];

		for (int i = 0; i < nx; i++) {
			System.out.print("x[" + i + "]：");
			x[i] = stdIn.nextInt();
		}

		heapSort(x, nx);	// 배열 x를 힙 정렬합니다.

		System.out.println("오름차순으로 정렬했습니다.");
		for (int i = 0; i < nx; i++)
			System.out.println("x[" + i + "]＝" + x[i]);
	}
}
```



## 도수정렬

요소의 대소관계를 판단하지 않고 빠르게 정렬

1단계: 배열 a를 바탕으로 각 점수에 해당하는 학생이 몇명인지 나타내기

2단계: 누적도수분포표 만들기 

3단계:목적배열 만들기

### 실습 6-17

```java
package chap06;
import java.util.Scanner;
// 도수 정렬

class Fsort {
	// 도수 정렬(0 이상 max 이하의 값을 입력합니다） 
	static void fSort(int[] a, int n, int max) {
		int[] f = new int[max + 1];		// 누적 도수
		int[] b = new int[n];			// 작업용 목적 배열

		for (int i = 0;     i < n;    i++) f[a[i]]++;				// 1단계
		for (int i = 1;     i <= max; i++) f[i] += f[i - 1];		// 2단계
		for (int i = n - 1; i >= 0;   i--) b[--f[a[i]]] = a[i];		// 3단계
		for (int i = 0;     i < n;    i++) a[i] = b[i];				// 4단계
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.println("도수 정렬");
		System.out.print("요솟수：");
		int nx = stdIn.nextInt();
		int[] x = new int[nx];

		for (int i = 0; i < nx; i++) {
			do {
				System.out.print("x[" + i + "]：");
				x[i] = stdIn.nextInt();
			} while (x[i] < 0);
		}

		int max = x[0];
		for (int i = 1; i < nx; i++)
			if (x[i] > max) max = x[i];

		fSort(x, nx, max);				// 배열 x를 도수 정렬

		System.out.println("오름차순으로 정렬했습니다.");
		for (int i = 0; i < nx; i++)
			System.out.println("x[" + i + "]＝" + x[i]);
	}
}
```
데이터의 비교,교환 작업이 필요 없다.  
단일 for문 사용  
도수분포표 필요 : 데이터의 최소값, 최대값 필요  


