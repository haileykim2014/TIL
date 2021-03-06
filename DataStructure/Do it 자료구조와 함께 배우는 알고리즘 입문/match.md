
## 목차
1. [브루트 포스법](#브루트-포스법)  


</br>  

# 브루트 포스법?

선형검색을 확장한 알고리즘이므로 단순법,소박법이라고 한다.  


### 실습 8-1  
- 텍스트에서 패턴을 검색하여 텍스트의 위치를 반환  
- 텍스트에 패턴이 여러개 있는 경우 가장 앞쪽에 위치한 텍스트의 인덱스반환  
- 검색에 실패하면 -1 반환  

```java
package chap08;
import java.util.Scanner;
// 브루트-포스법으로 문자열을 검색하는 프로그램

class BFmatch {
	// 브루트-포스법으로 문자열을 검색하는 메서드 
	static int bfMatch(String txt, String pat) {
		int pt = 0;		// txt 커서
		int pp = 0;		// pat 커서

		while (pt != txt.length() && pp != pat.length()) {
			if (txt.charAt(pt) == pat.charAt(pp)) {
				pt++;
				pp++;
			} else {
				pt = pt - pp + 1;
				pp = 0;
			}
		}
		if (pp == pat.length())			// 검색 성공!
			return pt - pp;
		return -1;						// 검색 실패!
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.print("텍스트：");
		String s1 = stdIn.next(); 					// 텍스트용 문자열 

		System.out.print("패턴：");
		String s2 = stdIn.next();					// 패턴용 문자열 

		int idx = bfMatch(s1, s2);					// 문자열 s1에서 문자열 s2를 검색

		if (idx == -1)
			System.out.println("텍스트에 패턴이 없습니다.");
		else {
			// 일치하는 문자 바로 앞까지의 길이를 구합니다.
			int len = 0;
			for (int i = 0; i < idx; i++)
				len += s1.substring(i, i + 1).getBytes().length;
			len += s2.length();

			System.out.println((idx + 1) + "번째 문자부터 일치합니다.");
			System.out.println("텍스트：" + s1);
			System.out.printf(String.format("패턴：%%%ds\n", len), s2);
		}
	}
}
```

실행결과

```
텍스트：ABC이지스DEF
패턴：이지스
4번째 문자부터 일치합니다.
텍스트：ABC이지스DEF
패턴：   이지스
```

### 실습 8-2

```java
package chap08;
import java.util.Scanner;
// String.indexOf, String.lastIndexOf 메소드에 의한 문자열 검색합니다.

class IndexOfTester {
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.print("텍스트：");
		String s1 = stdIn.next(); 					// 텍스트용 문자열 

		System.out.print("패턴：");
		String s2 = stdIn.next();					// 패턴용 문자열 

		int idx1 = s1.indexOf(s2);					// 문자열 s1에서 s2를 검색
		int idx2 = s1.lastIndexOf(s2);				// 문자열 s1에서 s2를 검색

		if (idx1 == -1)
			System.out.println("텍스트 안에 패턴이 없습니다.");
		else {
			// 찾아낸 문자열의 바로 앞까지의 문자 개수를 구합니다.
			int len1 = 0;
			for (int i = 0; i < idx1; i++)
				len1 += s1.substring(i, i + 1).length();
			len1 += s2.length();

			int len2 = 0;
			for (int i = 0; i < idx2; i++)
				len2 += s1.substring(i, i + 1).getBytes().length;
			len2 += s2.length();

			System.out.println("텍스트：" + s1);
			System.out.printf(String.format("패턴：%%%ds\n", len1), s2);
			System.out.println("텍스트：" + s1);
			System.out.printf(String.format("패턴：%%%ds\n", len2), s2);
		}
	}
}
```

실행결과

```
텍스트：AB주이지스DEF이지스12
패턴：이지스
텍스트：AB주이지스DEF이지스12
패턴：   이지스
텍스트：AB주이지스DEF이지스12
패턴：                 이지스
```

String.format("패턴：%%%ds\n", len1)

len1이 숫자3 이라면

%%3s\n 가 된다 : 3글자의 넓이에 맞춰 s2를 출력


### 실습 8-3  
KMP법 : 중간 검사 결과를 효율적으로 사용

검사했던 위치 결과를 버리지 않고 효율적으로 활용

몇 번째 문자부터 다시 검색할지에 대한 값을 미리 표로 만든다.

```java
package chap08;
import java.util.Scanner;
// KMP법에 의한 문자열 검색

class KMPmatch {
	// KMP법에 의한 문자열 검색
	static int kmpMatch(String txt, String pat) {
		int pt = 1;											// txt 커서
		int pp = 0;											// pat 커서
		int[] skip = new int[pat.length() + 1];				// 건너뛰기 표

		// 건너뛰기 표를 만듭니다.
		skip[pt] = 0;
		while (pt != pat.length()) {
			if (pat.charAt(pt) == pat.charAt(pp))
				skip[++pt] = ++pp;
			else if (pp == 0)
				skip[++pt] = pp;
			else
				pp = skip[pp];
		}

		// 검색
		pt = pp = 0;
		while (pt != txt.length() && pp != pat.length()) {
			if (txt.charAt(pt) == pat.charAt(pp)) {
				pt++;
				pp++;
			} else if (pp == 0)
				pt++;
			else
				pp = skip[pp];
		}

		if (pp == pat.length())		// pt - pp를 반환합니다.
			return pt - pp;
		return -1;					// 검색 실패
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.print("텍스트：");
		String s1 = stdIn.next(); 					// 텍스트용 문자열 

		System.out.print("패턴：");
		String s2 = stdIn.next();					// 패턴용 문자열 

		int idx = kmpMatch(s1, s2);	// 문자열 s1에서 문자열 s2를 브루트-포스법으로 검색

		if (idx == -1)
			System.out.println("텍스트에 패턴이 없습니다.");
		else {
			int len = 0;
			for (int i = 0; i < idx; i++)
				len += s1.substring(i, i + 1).getBytes().length;
			len += s2.length();

			System.out.println((idx + 1) + "번째 문자와 일치합니다.");
			System.out.println("텍스트：" + s1);
			System.out.printf(String.format("패턴：%%%ds\n", len), s2);
		}
	}
}
```


### 실습 8-4

```java
package chap08;
import java.util.Scanner;
// Boyer-Moore법으로 문자열을 검색 

class BMmatch {
	// Boyer-Moore법으로 문자열을 검색 
	static int bmMatch(String txt, String pat) {
		int pt;								// txt 커서
		int pp;								// pat 커서
		int txtLen = txt.length();			// txt의 문자 개수
		int patLen = pat.length();			// pat의 문자 개수
		int[] skip = new int[Character.MAX_VALUE + 1];	// 건너뛰기 표

		// 건너뛰기 표 만들기
		for (pt = 0; pt <= Character.MAX_VALUE; pt++)
			skip[pt] = patLen;
		for (pt = 0; pt < patLen - 1; pt++)
			skip[pat.charAt(pt)] = patLen - pt - 1;	// pt == patLen - 1
		// 검색
		while (pt < txtLen) {
			pp = patLen - 1;				// pat의 끝 문자에 주목

			while (txt.charAt(pt) == pat.charAt(pp)) {
				if (pp == 0)
					return pt;	// 검색 성공
				pp--;
				pt--;
			}
			pt += (skip[txt.charAt(pt)] > patLen - pp) ? skip[txt.charAt(pt)] : patLen - pp;
		}
		return -1;				// 검색 실패
	}

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);

		System.out.print("텍스트：");
		String s1 = stdIn.next(); 					// 텍스트용 문자열 

		System.out.print("패턴：");
		String s2 = stdIn.next();					// 패턴용 문자열 

		int idx = bmMatch(s1, s2);	// 문자열 s1에서 문자열 s2를 BM법으로 검색

		if (idx == -1)
			System.out.println("텍스트에 패턴이 없습니다.");
		else {
			int len = 0;
			for (int i = 0; i < idx; i++)
				len += s1.substring(i, i + 1).getBytes().length;
			len += s2.length();

			System.out.println((idx + 1) + "번째 문자와 일치합니다.");
			System.out.println("텍스트：" + s1);
			System.out.printf(String.format("패턴：%%%ds\n", len), s2);
		}
	}
}
```
