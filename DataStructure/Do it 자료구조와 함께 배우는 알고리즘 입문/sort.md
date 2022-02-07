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
