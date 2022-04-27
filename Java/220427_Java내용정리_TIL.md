# 22.04.26 Java 수업 내용정리:pencil2:

## **1. 오버로딩(overloading)**:pushpin:
* 오버로딩의 사전적 정의는 '과적하다'
* 한 클래스 안에 같은 이름의 메서드 여러 개 정의하는 것

**[성립조건]**
* 메서드 이름은 동일해야 함
* 매개변수의 개수 또는 타입이 달라야 한다.
* 반환 타입은 영향없다.
```java
	int add (int a, int b) {return a+b;}
	int add (int x, int y) {return a+b;}
	// 메서드 이름은 같지만 매개변수자료형이 두 가지 전부 일치한다.
	// 때문에, 오류가 난다
	
	int add (int a, int b) {return a+b;}
	long add (int a, int b) {return a+b;}
	// 메서드의 반환타입이 같던 다르던 오버로딩의 영향을 주지 않기때문에 오류발생원인이 아니다
	// 이번에도 역시, 매개변수의 자료형이 일치하므로 오류가 난다.
	
	long add (int a, int b) {return a+b;}
	long add (long a, int b) {return a+b;}
	// 매개변수의 자료형이 동일하지 않으므로 해당구문은 문법적 오류없이 잘 수행된다.
	// 혹시 2번째 매개변수가 둘이 똑같아서 안되지 않을까 싶었지만 첫 번째 매개변수 타입이
	// 다르게 지정하였더니, 잘 수행되는걸로 봐서는 자리수 중에 하나만 자료형이 다르면
	// 문제없이 실행이 가능한걸로 보인다.
```
**[추가 주의사항]**
```java
int add (int a, int b) {return a+b;}
long add (long a, int b) {return a+b;}
```
>위 구문에서 **메서드의 타입만 변경**하였다.
	 분명 메소드의 타입이 같던 다르던 오버로딩에 영향을 주지 않는다고 하였다.
	 그런데 지금 오류가 나는 이유는 사실 **첫 번째 메서드의 타입**때문이다.
	 무슨 말이냐 하면, **add의 메소드 타입은 int로 4byte의 메모리인데 
	 매개변수로 8byte의 long 타입을 저장시키기 때문에 오류가 난다.**
	 4개의 구슬을 담을수 있는 주머니에 8개의 공간을 차지하는 구슬을 넣을수 없는것 처럼 말이다. 메서드의 타입은 오버로딩에 영향을 주지 않는다고 해도 매개변수와의 타입에 대해 영향이 생길수도 있으니 꼭 참고해야한다. 

```java
	long add (int a, long b){
		return a+b;  
	}
	// add(2,3) 오류남
	// add(2,3L) 정상출력
```
> **매개변수 b의 타입은 long**이라서 입력값을 3 으로 입력을 하게되면 입력오류가 난다.
> 따라서 3 이란 값을 입력하고 싶다면  long 타입의 특징을 적용하여 값 뒤에 L 을 첨부하여 입력하도록 한다.
---

## **2. 참조변수**:pushpin:
``` java
Mouse mickey = new Mouse();
```
* new 키워드를 사용하여 인스턴스 주소값을 생성
*  생성된 주소값은 객체 데이터를 포함하니 Heap 메모리에 할당
*  주소값을 할당하는 mickey 라는 참조변수를 생성한다.
* 이후 mickey를 호출하면 할당된 주소로 찾아간다.
```java
public class YourClassNameHere {
class Mouse {
    int age;
    String name;
    String address;
    
    public void sing() {
        System.out.println(name + "찍찍!!");
    }
    
    public static void main(String[] args) {
       Mouse mickey = new Mouse();// 인스턴스생성
        
        mickey.name = "미키마우스";
        mickey.age = 85;
        mickey.address = "할리우드";
        
        System.out.println(mickey);
        
        mickey.sing();
    }
}
}
```
1. Mouse 라는 클래스를 생성하고 나이,이름,주소 라는 멤버변수를 생성하였다.
2. sing 이라는 메서드를 생성하고 그 메서드는 객체의 이름 값 + "찍찍!!"을 출력한다. 
3.  new 키워드를 사용하여 mouse 클래스의 인스턴스 주소값을 생성한다.
4. mickey라는 참조변수에 인스턴스 주소값 즉, 참조값을 담았다.
5. 미키의 주소값에 이름,나이, 주소 라는 멤버변수를 선언 후 변수 별로 값을 담았다.
6. 미키에게 메서드를 실행시키니 미키의 이름인 미키마우스가 호출이 된다.
7. 즉 출력은 미키마우스찍찍!! 이 출력된다.

```java
//App.java
public class App {

	public static void main(String[] args) {
		// 학생 인스턴스 2개 생성
		
		//박서준, park
		Student park = new Student("박서준", 25);
		
		//한소희, han
		Student han = new Student("한소희", 25);
		
		System.out.println(park.getAge() + park.getName());
		System.out.println(han.getAge() + han.getName());
		System.out.println(park);// 각각의 주소값을 가지고 있음
		System.out.println(han);
		
		park = han;// park이라는 참조변수에 han참조변수를 덮어씌움, 
		System.out.println(park.getName()); // 출력값: 한소희
		System.out.println(park); //기존의 값에서 han의 주소값으로 할당 기존의 할당된 힙메모리는 자동적으로 해제됨
		System.out.println(han);// 같은 주소값인 com.reference.Student@5d22bbb7 출력
	}
}
```
```java
// Student.java
public class Student {
	//멤버변수 생성 
	private String name;
	private int age;
	//기본 생성자함수 생성
	public Student() {}
	//name, age 인자를 갖는 생성자 함수
	public Student(String name, int age) {
		this.name = name;
		this.age = age;
	}
	//getter,setter
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
}
```
---
## **3. 접근제어자**:pushpin:

* 자바 클래스에서 멤버들이 노출되는 것을 막기 위해 접근을 제한해주는 제어자  

* 모두가 접근 가능한 변수나 메소드는 제약 조건 없이 쉽게 데이터가 변경가능하여데이터를 안전하게 변경하기 위해 접근을 할 수 있는 대상을 지정해 줄 때 사용  

저번 강의정리 내용으로 접근제어자에 대한 설명을 자세히 다뤘으므로 해당내용은 04월27일 수업내용정리 md 파일을 보면 된다.


