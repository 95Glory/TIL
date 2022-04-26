# 22.04.25 Java 수업 내용정리
---

## 1. Java란 무엇인가?
1. 객체지향 프로그래밍 언어
2. 운영체제에 독립적이다
3. 풍부한 클래스 라이브러리가 존재한다
4. 필요한 시점에 클래스를 로딩하여 사용할 수 있다는 장점이 있다.   
---
## 2. JVM / JRE / JDK 은 무엇인가?
### 2.1 JVM 
> * 바이코드를 읽고, 검증하고, 실행한다.  
> * 실행환경의 규격을 제공한다.(필요한 라이브러리 및 기타파일)
### 2.2 JRE 
> * 컴파일된 자바 프로그램을 실행시킬 수 있는 자바 환경  
> * JRE는 JVM의 실행환경을 구현했다고 할 수 있다
> * 자바 프로그램을 실행시키기 위해선 JRE를 반드시 설치해야함.  
> * 하지만 자바 프로그래밍 도구는 포함되어있지 않기 때문에
>   자바 프로그래밍을 하기 위해선 JDK가 필요하다.
### 2.3 JDK 
> * 자바 개발 키트의 줄임말
> * JRE에 컴파일러, 디버거 등 개발도구를을 포함하는 프로그램
---
## 3. JavaScript vs Java 비교해보자
**[JavaScript]**
1. 변수선언시 정수형 / 문자형 그 외 등등 지정된 변수타입은 없다.
2. 변수의 타입이 코드의 실행 및 동작 과정에서 변할수 있다.
3. 즉, 동적타입 언어다.

**[Java]**  
1. 변수선언시 js와 다르게 변수의 타입을 선언해야 한다.
2. 한 번 지정한 변수에는 값을 초기화 할 순 있지만 타입변경은 불가하다.
3. 즉, 정적타입이라고 한다.

> 해당차이를 보았을 때, Js 보다는 Java는 데이터 타입에 대해 엄격하게 규정을 하고 있다. 때문에 추후 코드의 유지 및 보수가 용이할 것으로 보이고 좀 더 엄격한 환경에서 개발작업을 진행이 가능할 것 같다는 나의 생각이다.
---
## 4. 변수(Variable)
**[변수의 선언]**  
Java에서는 변수 선언 시 Keyword로 Data type을 명시하기 때문에 해당 변수에는 특정 type의 값만 담을 수 있음. 추가로 변수의 초기화를 진행하지 않으면 변수는 생성되지 않는다.
```java
// 정수형 타입의 변수 a 선언
int a; // Integer의 줄임표현

System.out.println(a); 
// error: variable a might not have been initialized`
```
**[변수의 초기화]**  
변수에 실제로 값을 대입하는 것.
```java
int a;
a = 10;
System.out.println(a);
// 10
```
**[변수 이름 규칙]** 
1. 영문자(대소문자), 특수문자($,_)만 사용 가능
2. 숫자로 시작할 수 없음
3. 키워드, 예약어 사용 불가(while, int break 등)
4. **Java에서는 JavaScript와 동일하게 camelCase 방식을 사용.**

```java
int age; //변수의 선언, 생성이라고도 함
//System.out.println(age); // error: variable age might not have been initialized.
// -> 값이 초기화 되어있지 않기 때문에 실행(컴파일) 불가
	
age = 10; //age 변수를 10이란 값으로 '초기화(initialization)'
System.out.println(age);

int age2 = 20; //선언과 초기화를 한 번에 작성가능

/**
 * 변수 네이밍 컨벤션(명명 규칙)
 * 1. 특수 문자($ 와 _만 가능)
 * 2. 숫자로 시작할 수 없음
 * 3. 키워드, 예약어 사용 불가(while, int, break 등 추후 설명)
 */

//특수 문자
int $age; // 접두에 $ 가능
int _age; // 접두에 _ 가능

int 335; // 숫자로 시작 불가

// 예약어(Keyword)로 선언 불가
int int;
int while;
int for;
```
---
## 5. 데이터 타입(Data Type)
**[기본타입]**
### 일반적인 숫자(정수, 실수), 문자열, 논리형 등과 같은 기본적인 데이터 타입, 숫자형(Java에서는 정수형이라고 함)은 값의 범위에 따라 보관할 수 있는 크기(size)가 다름
```java
public static void main(String[] args) {
		//정수형(양수, 음수, 0)
		byte a = 127; //-128 ~ 127 / 1바이트
		short b = -32768; //-32768 ~ 32767 / 2바이트
		int c = 0; //약 20억, 정수형의 기본 사용 타입 /4바이트
		long d = 200000; //약 2의 63승 / 8바이트
		
		//문자형
		char ch1 = 'A';
		System.out.println(ch1);
		System.out.println((int)ch1);//65, ASCII코드 문자도 결국 숫자로 변환됨.
		
		char ch2 = 66;
		System.out.println(ch2);
		
		//실수형
		float fnum = 1.5f; //4바이트
		System.out.println(fnum);
        double fnum = 1.5; //8바이트
		System.out.println(fnum);
		
		//논리형
		boolean isMan = true; // true, false
		System.out.println(isMan);
		
		//상수
		final int MAX_NUM;
		final double PI = 3.141592;
		
		MAX_NUM = 100; //처음 초기화만 가능.
		
		MAX_NUM = 200; //두 번째 부터는 값 변경 불가.
	}

}
```
**[참조타입]**
### 추후 객체수업시 설명듣기로 함.
---
## 6.연산자(Operator)
**[부호 연산자]**  
```java
int num = 10;

System.out.println(+num);
System.out.println(-num);// 부호만 바뀜
System.out.println(num); // 값 10이 그대로 출력됨.

num = -num;
System.out.println(num); // -10 
```
**[산술 연산자]**
```java
// 수학 점수와 영어 점수의 총점과 평균 구하기

int mathScore = 90;
int engScore = 70;

int totalScore = mathScore + engScore;
System.out.println(totalScore);

double avgScore = totalScore / 2.0;
System.out.println(avgScore);
```
**[증감 연산자]**
```java
// 수학 점수와 영어 점수의 총점과 평균 구하기

int mathScore = 90;
int engScore = 70;

int totalScore = mathScore + engScore;
System.out.println(totalScore);

double avgScore = totalScore / 2.0;
System.out.println(avgScore);
```
**[증감 연산자의 위치]**
```java
int a = 10;
int b = ++a;
System.out.println(b);

int c = 10;
int d = c++;
System.out.println(d);
```
**[관계 연산자]**
```java
int myAge = 27;
boolean value = (myAge > 25);
System.out.println(value); // true
```
```java
int myAge = 22;
int yourAge = 25;
System.out.println(myAge <= yourAge);
```
**[논리 연산자]**
```java
// && 논리 곱

int a = 10;
int b = 20;

boolean flag = (a > 0) && (b > 0);
System.out.println(flag); //둘 다 ture이어야만 true.

flag = (a < 0) && (b > 0);
System.out.println(flag); // 하나라도 false면 false.

// || 논리 합
flag = (a < 0) || (b > 0);
System.out.println(flag);//하나라도 true면 true.

// ! 부정
flag = true;
flag = !flag;
System.out.println(flag);
```
---
## 7.반복문
ava의 조건문(Condition)과 반복문(Loop)은 JavaScript와 차이가 없음.  
Java가 JavaScript보다 먼저 존재했고, JavaScript가 Java의 문법을 거의 표방했기 때문.
때문에 이번 수업에서 새롭게 알게 된 Foreach에 대해 알아보려 한다.

foreach(For-each)문은 for, while, do-while 반복문과 같은 배열 탐색 기법.
사용방법은 다음과 같습니다.
1. 일반적인 for 반복문과 동일하게 for 키워드를 사용.
2. 반복문 내에 카운터 변수를 선언하고 콜론(:) 다음 배열이름을 순서대로 선언.
3. 일반적으로 배열이나 Collection 클래스(ArrayList ... 등)를 반복하는 데 사용.

```java
//기존 for문 사용
int[] arr = {0, 1, 2, 3, 4};
for (int i = 0; i < 5; i++) { 
System.out.println(arr[i]); // 0 1 2 3 4 출력
}

//foreach문 사용
int[] arr = {0, 1, 2, 3, 4};
for (int i : arr) { 
System.out.println(arr[i]); // 0 1 2 3 4 출력
}
```
---
## 8. 배열(Array)
객체가 관여된 배열은 JavaScript 와 Java는 많은 차이가 존재한다. 자바에서의 배열은 class가 관여가 같이 들어가게된다.

**[배열의 선언]**  

자료형[] 배열이름 = new 자료형[개수];  
자료형 배열이름[] = new 자료형[개수];
```java
	int[] test1 = new int[5];
	int test2[] = new int[5];
```

**[배열의 초기화]**

```java
	int[] studentIds = new int[] {101,102,103}; //개수는 생략
	int[] studentIds = new int[3] {101,102,103}; // 오류발생 배열의 개수와 값은 동시에 입력 불가
	int[] studentId ={101,102,103};// int형 요소가 3개인 배열
```

**[객체배열]]**
```java
package Ex;

public class Family {
	private String members; //필드의 선언
	private int ages; //필드의 선언
	
	// 객체의 생성을 도와주는 함수 즉 생성자라고 칭한다.
	// new 키워드를 사용하여 호출
	public Family(String member, int age) {
		super();
		this.members = member; //클래스의 변수를 상속받아 객체의 필드값에 넣어주기
		this.ages = age;//클래스의 변수를 상속받아 객체의 필드값에 넣어주기
	}
	public String getmembers() { //값을 읽어온다
		return members;
	}
	public void setmembers(String members) { //값을 재설정 해준다
		this.members = members;
	}
	public int getages() { //값을 읽어온다
		return ages;
	}
	public void setages(int ages) { //값을 재설정 해준다
		this.ages = ages;
	}
	
```
```java
package Ex;

public class Ex {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Family[] group = new Family[4]; //클래스이자, 타입인 Family에 배열이름인 group을 
		                                //생성후 배열크기 4 지정
		group[0] = new Family("김경수",63); //요소에 값 입력
		group[1] = new Family("김혜경",66);
		group[2] = new Family("김주만",90);
		group[3] = new Family("김영광",95);

		for (Family groups : group) {   
			//foreach 사용하여 group[i]에 반복을 돌려 새로운 배열 groups에 할당
			System.out.println(groups.getmembers()+":"+groups.getages()); 
			//입력된 값을 getter메소드로 읽어온다. 
		}
	}
}
```













  
