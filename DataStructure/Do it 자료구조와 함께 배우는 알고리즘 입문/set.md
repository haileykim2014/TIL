
## 목차
1. [집합](#집합이란-)  


</br>  

# 집합이란 ?

명확한 조건을 만족하는 자료의 모임  


## 집합과 요소

집합 : 객관적으로 범위를 규정한 어떤것의 모임

요소 : 집합안에서의 각각의 어떤것

요소 개수가 1개여도 집합이다.

공집합 : 요소가 없는 집합

## 부분집합과 진부분집합

다른 집합에 포함된 집합

### 실습7-1 A,B

```java
package chap07;
// int형 집합

public class IntSet {
	private int max;			// 집합의 최대 개수
	private int num;			// 집합의 요소 개수
	private int[] set;			// 집합 본체

	// 생성자
	public IntSet(int capacity) {
		num = 0;
		max = capacity;
		try {
			set = new int[max];				// 집합 배열 생성
		}
		catch (OutOfMemoryError e) {		// 배열 생성 실패
			max = 0;
		}
	}

	// 집합의 최대 개수
	public int capacity() {
		return max;
	}

	// 집합의 요소 개수
	public int size() {
		return num;
	}

	// 집합에서 n을 검색합니다(index 반환, 몇번째인지).
	public int indexOf(int n) {
		for (int i = 0; i < num; i++)
			if (set[i] == n)
				return i;					// 검색 성공
		return -1;							// 검색 실패
	}

	// 집합에 n이 있는지 없는지 확인합니다. 
	public boolean contains(int n) {
		return (indexOf(n) != -1) ? true : false;
	}

	// 집합에 n을 추가합니다.
	public boolean add(int n) {
		if (num >= max || contains(n) == true)	// 가득 찼거나 이미 n이 존재합니다.
			return false;
		else {
			set[num++] = n;						// 가장 마지막 자리에 추가합니다.
			return true;
		}
	}

	// 집합에서 n을 삭제합니다.
	public boolean remove(int n) {
		int idx;									// n이 저장된 요소의 인덱스

		if (num <= 0 || (idx = indexOf(n)) == -1)	// 비어 있거나 이미 n이 존재합니다.
			return false;
		else {
			set[idx] = set[--num];					// 마지막 요소를 삭제한 곳으로 옮깁니다.
			return true;
		}
	}

	// 집합 s에 복사합니다. 
	public void copyTo(IntSet s)	{
		int n = (s.max < num) ? s.max : num;	// 복사할 요소 개수
		for (int i = 0; i < n; i++)
			s.set[i] = set[i];
		s.num = n;
	}

	// 집합 s를 복사합니다.
	public void copyFrom(IntSet s)	{
		int n = (max < s.num) ? max : s.num;	// 복사할 요소 개수
		for (int i = 0; i < n; i++)
			set[i] = s.set[i];
		num = n;
	}

	// 집합 s와 같은지 확인합니다. 
	public boolean equalTo(IntSet s)	{
		if (num != s.num)						// 요소 개수가 같지 않으면
			return false;						// 집합도 같지 않습니다.

		for (int i = 0; i < num; i++) {
			int j = 0;
			for ( ; j < s.num; j++)
				if (set[i] == s.set[j])
					break;
			if (j == s.num)						// set[i]는 s에 포함되지 않습니다.
				return false;
		}
		return true;
	}

	// 집합 s1과 s2의 합집합을 복사합니다.
	public void unionOf(IntSet s1, IntSet s2) {
		copyFrom(s1);								// 집합 s1을 복사합니다.
		for (int i = 0; i < s2.num; i++)			// 집합 s2의 요소를 추가합니다.
			add(s2.set[i]);
	}

	// "{ a b c }"형식의 문자열로 표현을 바꿉니다. 
	public String toString() {
		StringBuffer temp = new StringBuffer("{ ");
		for (int i = 0; i < num; i++)
			temp.append(set[i] + " ");
		temp.append("}");
		return temp.toString();
	}
}
```


### 실습 7C-1

```java
package chap07;
// toString 메서드의 오버라이드 차이점 확인하기

class A {
	// toString을 정의하지 않습니다.
}

class B {
	int x;
	
	// 생성자
	B(int x) { this.x = x; }
	
	// toString을 오버라이드합니다.
	public String toString() { return "B[" + x + "]"; }
}

public class ToStringTester {
	public static void main(String[] args) {
		A a1 = new A();
		A a2 = new A();
		B b1 = new B(18);
		B b2 = new B(55);

		System.out.println("a1 = " + a1.toString());
		System.out.println("a2 = " + a2);
		System.out.println("b1 = " + b1.toString());
		System.out.println("b2 = " + b2);
	}
}
```

인스턴스의 상태를 간단한 문자열로 반환하는 메서드는 public toString() 형식으로 정의하는 것이 좋다. 인스턴스의 상태를 출력할때 인스턴스를 출력하는 코드에 함께 넣으면 자동으로 호출된다.  
<br>

### 실습 7-2

```java
package chap07;
// int형 집합 클래스 IntSet을 사용하는 예

public class IntSetTester {
	public static void main(String[] args) {
		IntSet s1 = new IntSet(20);
		IntSet s2 = new IntSet(20);
		IntSet s3 = new IntSet(20);

		s1.add(10);			// s1 = {10}
		s1.add(15);			// s1 = {10, 15}
		s1.add(20);			// s1 = {10, 15, 20}
		s1.add(25);			// s1 = {10, 15, 20, 25}

		s1.copyTo(s2);		// s2 = {10, 15, 20, 25}
		s2.add(12);			// s2 = {10, 15, 20, 25, 12}
		s2.remove(25);		// s2 = {10, 15, 20, 12}

		s3.copyFrom(s2);	// s3 = {10, 15, 20, 12}

		System.out.println("s1 = " + s1);
		System.out.println("s2 = " + s2);
		System.out.println("s3 = " + s3);

		System.out.println("집합 s1에 15는 " + 
									(s1.contains(15) ? "포함됩니다." : "포함되지 않습니다"));

		System.out.println("집합 s2에 25는 " +
									(s2.contains(25) ? "포함됩니다." : "포함되지 않습니다"));

		System.out.println("집합 s1과 s2는 " + 
									(s1.equalTo(s2) ? "같습니다" : "같지 않습니다"));

		System.out.println("집합 s2와 s3은 " + 
									(s2.equalTo(s3) ? "같습니다" : "같지 않습니다"));

		s3.unionOf(s1, s2);		// s3 ← s1 ∪ s2

		System.out.println("집합 s1과 s2의 합집합은 " + s3 + "입니다.");
	}
}
```
