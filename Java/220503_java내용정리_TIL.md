# 22.05.03 Java 수업 내용정리:pencil2:
## 1. 예외처리:pushpin:
**[프로그램 오류]**
* 컴파일 에러
 : 컴파일 할 때 발생하는 에러이다. 구문이 오류가 날 때 나는 에러이며 좌측에 빨간색으로 표시가 된 다.  
 
* 런타일 에러
 :실행 할 때 발생하는 에러이다. 구문상 오류가 나지는 않지만 막상 실행을 하게 되며 콘솔창에 에러 문구가 나오면서 실행이 되지 않는다.  
 
* 논리적 에러 
 : 작성 의도와 다르게 동작하는 에러이다. 문법적으로도 오류가 나지 않고 실행도 잘 되지만 인간의 상식상 옳지 않은 결과가 나올때 발생하는 에러이다. 예를 들면 사람의 나이가 음수로 나오는 현상같은 오류이다.

>컴파일 에러, 논리적 에러는 개발자의 역량에 따라 언제든지 해결 할 수 있는 문제이다. 컴파일에러는 문법적으로 검토를 해결이 되고, 논리적 에러는 실행값을 검증 및 검토 하면 되지만 **런타일 에러는 손쉽게 오류사항을 파악하기는 어려운 일**이다.때문에, **런타임 에러를 처리하는 방법**에 대해 알아보려 한다.  
>

**[자바의 런타임 에러]**
* 에러 : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류(메모리 부족으로 인한 오류 및 하드웨어 문제 등)  

* 예외 : 프로그램 코드에 의해서 수습할 수 있는 다소 미약한 오류(개발자의 코드수정으로 인해 해결가능)

**[예외처리의 정의와 목적]**
* 정의 : 프로그램 실행 시 발생할 수 있는 예외의 발생에 대비한 코드를 작성
*  목적 : 프로그램 비정상 종료를 막고, 정상적인 실행상태를 유지하는 것  

**[예외의 종류]**
* Exception 
: **사용자의 실수**와 같은 외적인 요인에 의해 발생하는 예외  

* RuntimeException
: **프로그래머의 실수**로 발생하는 예외  

**[예외처리 기본 문법]**
```
try{
    예외가 발생할 수 있는 코드 부분
    } catch(처리할 예외 타입 e){
    try 블록 안에서 예외가 발생했을 때 예외를 처리하는 부분
    }
```
**[실습]**
```java
public class Ex0503 {

	public static void main(String[] args) {
		int[] arr = {1,2,3,4,5};
		for (int i = 0; i <= 5; i++) {
			System.out.println(arr[i]);
		}
		System.out.println("end");
	}
}
```
> **결과 값**
> 1
2
3
4
5
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5
	at stet02_test/Ex0503.Ex0503.main(Ex0503.java:8)
```
결과값과 같이  ArrayIndexOutOfBoundsException 에러가 발생한다.
배열의 크기를 초과하는 배열의 인덱스를 호출하니 나오는 에러이다.
for문에서 에러가 나니 end를 출력하는 명령어가 먹히지 않는다.
```
**[에외처리 후]**
```java
	public static void main(String[] args) {
		int[] arr = {1,2,3,4,5};
		try {
			for (int i = 0; i <= 5; i++) {
				System.out.println(arr[i]);
			}
		} catch (ArrayIndexOutOfBoundsException e) {
			System.out.println(e);
		}
		System.out.println("end");
		
	}
}
```
>결과 값
>1
2
3
4
5
java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5
end
```
에러메세지가 문자형태로 출력이 되면서, 프로그램이 죽지않고 계속 실행되어  
 마지막 "end" 또한 잘 출력이 되는 걸 볼 수 있다.
```
**[예외의 우선순위]**
예외의 종류에도 상속이 존재한다.  
Exception 은 예외처리의 최 상위 객체이고, ArithmeticException은 산술오류가 날 때, 발생하는 예외처리의 객체 즉, Exception의 하위 클래스 이다.
 ArithmeticException 가 발생할 때 몰론 ArithmeticException 예외처리를 해도 좋지만 부모 클래스인 Exception을 사용해도 처리가 된다.

**[Finally]**
파일, 데이터베이스와 같은 자원들은 작업이 끝났을 때 연결을 끊어줘야 한다.  
이러한 작업들에 대해서 반드시 해야 할 작업들을 처리해야 할 때 finally를 이용한다.

