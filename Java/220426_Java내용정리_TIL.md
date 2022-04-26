# 22.04.26 Java 수업 내용정리:pencil2:
## **1. 객체지향프로그래밍**:pushpin:
* 주체 vs 객체
 
* 나는 주체, 객체는 나를 제외한 모든 것.  다른 사람 입장에서는 내가 객체.

* 세상에 존재하는 모든 것은 사물 즉, 객체이다.
* 각각의 사물(인스턴스)은 고유함.
* 인스턴스 : 고유한 값들
---
## **2. 객체생성**:pushpin:

1. 인스턴스를 생성하기 위해서는 new 키워드와 함께 클래스 명( ) 를 기술한다.
   
2. new 클래스명("신덕이", 2, "갈색", 6.5);  -> 하나의 인스턴스

3. Dog 타입의 변수 sinduk에 생성한 인스턴스 값 할당
   
4.  타입 변수명
Dog sinduk = new Dog("신덕이", 2, "갈색", 6.5);    
위 자체가 값이기 때문에 별도의 변수에 저장을 하지 않으면 다음 줄의 코드부터는 활용이 불가능

5. 클래스(class) : 어떤 객체를 생성하기 위한 설계도
설계도가 없으면 객체나 인스턴스를 생성할 수 없음.
클래스는 객체에 비해 상대적으로 더 추상적인 레벨로
정의한다.

6. 객체(object) : 객체 지향 프로그래밍을 말할 떄 사용하기도 한다.  
클래스에 비해 상대적으로 구체적인 레벨단에서 정의한다.  
클래스에 선언된 모양 그대로 생성된 실제이며 소프트웨어 세계에 구현할 대상이다.

7. 인스턴스(instance) :   설계도를 바탕으로 소프트웨어 세계에 구현된 구체적인 실체 즉, 객체를 소프트웨어에 실체화 하면 그것을 '인스턴스'라고 부른다.

```java
class Person {// 모든 객체는 속성과 행위를 가지고 있음.
	String name; // 속성, Member field

	public void work() { // 행위, Member Method
		System.out.println(name + "이(가) 걷고 있습니다.");
	}
}

Person y = new Person("Yoo"); // 사람 객체(인스턴스) 생성
// y에는 "Yoo"라고하는 고유한 사람이 들어있음.
Peron h = new Person("HongDoHee");

System.out.println(y == h); //false, 서로 다른 사람이기 때문에 같지 않다.
```

***OOP(Object-Oriented Programming) 객체 지향 프로그래밍***  
> -모든 데이터를 객체(object)로 취급하며, 이러한 객체가 바로 프로그래밍의 중심   
 -객체(object)란 간단히 이야기 하자면 실생활에서 우리가 인식할 수 있는 있는 사물로 설명할 수 있다.
---
 ## **3. 실습예제**:pushpin:  
  
    
## [구현사항]:point_up:
>1. 'Student'클래스를 생성할 것.  

>2. Student 클래스의 멤버변수로 학번,이름,학년,주소지를 생성할 것.  

>3. 학생의 이름과 학년을 나란히 출력하는 메서드를 생성할 것.  

>4. 학생인스턴스의 멤버변수값을 직접 기입하고 출력.  

**[최종 출력 값 : **톰,2**]**

```java
package com.sample;

public class Student {
	int studentID; // 학번
	String studentName; // 학생이름
	int grade; // 학년
	String address; // 주소,사는 곳
	
	public Student(String studentName,int grade){
		super();
		this.studentName = studentName;
		this.grade = grade;	
	};
	public void showStudent() {
		System.out.println("showStudent() 호출");
		System.out.println(studentName + "," + grade);
	}
}
```
---
```java
package com.sample;

public class App {
	public static void main(String[] args) {
		Student s = new Student("톰",2);
		s.showStudent(); 
		
	}
}
```
## 풀이:thumbsup: 
>1. 'Student'클래스를 생성할 것.  
```java
public class Student {


}
```
클래스의 이름은 대/소문자 상관없이 작성가능하다. 파일 맨 위 상단에 public class '클래스명' 을 작성후 중괄호 { }를 작성하고 이 사이에 해당 클래스의 설계도를 작성한다.     

>2. Student 클래스의 멤버변수로 학번,이름,학년,주소지를 생성할 것.  
```java
int studentID; // 학번
	String studentName; // 학생이름
	int grade; // 학년
	String address; // 주소,사는 곳
```
* 1번 과정에서 생성된 중괄호 {} 사이에 멤버변수들의 자료형을 파악하고 요구사항에 맞게끔 '자료형 변수명'으로 기입하여 선언한다.

>3. 학생의 이름과 학년을 나란히 출력하는 메서드를 생성할 것.  

```java
public Student(String studentName,int grade){
		super();
		this.studentName = studentName;
		this.grade = grade;	
	};
```
* 멤버변수들중 학생의 이름과 학년만 출력을 받으려고 한다. 그렇다면 멤버변수중  Student 인스턴스에는 studentName와 grade만 파라미터로 받아내면 된다.   

* 이러한 과정을 **생성자 함수**를 만든다고 한다.
생성자 함수에서 파라미터로 받는 인자들은 멤버변수와 이름은 같을 수 있어도 엄연히 다른 종류의 변수이다.

* 멤버변수와 생성자 함수의 인자값을 할당하기 위해 가시적으로 표현할 뿐, 다른 변수이다.  
 
* 때문에 this를 사용하게 되는데 여기서의 this는 현재 존재하고있는 클래스의 변수명이다. 즉 Student 클래스의 멤버변수이다.
* 추후에 학생이름과 등급에 값을 기입할때 그 값은 변수 studentName 와 grade 에 할당이 되고 다시 this.studentName 와 this.grade에 할당이 되어 멤버변수에 값을 전달하는 형태이다.

```java
	public void showStudent() {
		System.out.println("showStudent() 호출");
		System.out.println(studentName + "," + grade);
	}
```
* 원하는 변수에 값을 입력하여 클레스의 멤버변수에 전달했다면 그 값이 출력되도록 진행해주는 showStudent 메서드를 생성한다. System.out.println 를 사용해 화면에 출력되도록 해준다.

>4. 학생인스턴스의 멤버변수값을 직접 기입하고 출력.  
```java
package com.sample;

public class App {
	public static void main(String[] args) {
		Student s = new Student("톰",2);
		s.showStudent(); 
	}
}
```
* 이제 클래스의 설계도의 작성이 끝이 나면 새로운파일에 main메서드를 호출하고 새로운 객체를 new를 통해 생성하고 변수 s에 담아준다 또한 괄호에 기입할 데이터를 적어야 하며 선언된 자료형에 맞게 작성을 해야 한다  
*  예를 들어 int a 를 선언하여 정수형 변수를 만들었는데 "2" 처럼 숫자를 문자로 변경하여 할당하면 오류가 나는 것 처럼 말이다.  
* 마지막으로 새로운 객체를 담은 s 에 showStudent 메서드를 사용하여 값을 화면으로 출력하게 해준다.

   ## **4. getter / setter 메서드**:pushpin:
*  객체지향 프로그래밍에서 객체의 데이터는 객체 외부에서 직접적으로 접근하는 것을 막는다. 객체 데이터를 외부에서 읽고 변경 시 객체의 무결성이 깨지기 쉽기 때문이다.  

* 예를 들어, 사람의 나이를 외부에서 223살로 변경해버린다면 이 데이터가 과연 신뢰를 할 수 있는 데이터인가? 이러한 현상을 막기 위해 값이 정의되어있는 클래스 외부에서 값을 변경하는 것을 막도록 한다.

* 이렇게 외부에서의 값을 정해진 규격 혹은 자료형의 무결성이 깨지지 않게 값을 안전하게 재할당 해주는 메서드가 setter 메서드 이다.

   ``` java
   public void setAge(int age) {
		if(age >= 1 && age <= 100) { 
			this.age = age;
		} else {
			return;
		}
	}
   ```
* 변수 명명법은 set + 멤버변수명으로 명명하면 된다.     
  
* 변수의 이름은 달라지지만 파라미터로 int age라는 멤버변수로 할당을 받기 때문에 무결성을 지킬 수 있다.  
  
* 위 처럼 사람의 나이를 1보다 크고 100보다 작은 수로 하여 제약을 걸어 외부에서 setter 메서드를 사용하여 값을 200을 입력하더도 출력되지 않게끔 조치를 취할수있다.

   ```java
   public class SetterTest {

	public static void main(String[] args) {
		Person park = new Person();
		park.setName("린킨박");
		
		// 린킨박의 나이를 20살로 설정
		park.setAge(20);
		
		// 멤버 메서드 호출
		System.out.println(park.showPerson());
	}


* 위와 같이, Person의 객체를 담은 park 에 닷(.)을 사용하여 접근하고 setter메서드를 사용한다.

* 이에 비해 getter 메서드는 객체의 해당요소의 값을 읽어오는 역할을 한다. setter로 변수의 값을 변경하였다면 값의 가공을 걸친 후 출력해주는 메서드라고 생각하면 된다.

||Getter|Setter|
|:---:|:---:|:---:|
|리턴타입|필드(멤버)의 리턴타입|Void|
|메소드 이름|get+필드이름|set+필드이름|
|리턴 값|필드값||
|매개 변수 타입||필드타입|

   ## **5. 접근제한자 pubilc / private**:pushpin:
   클래스와 인터페이스를 다른 패키지에서 사용하지 못하도록 막을 필요가 있다. 그리고 객체 생성을 막기 위해 생성자를 호출하지 못하게 하거나 필드나 메소드를 사용하지 못하도록 막아야 되는 경우도 있다. 이때 접근 제한자를 사용할 수 있다.

[**public 접근 제한**]  
 public 접근 제한은 모든 영역에서 아무런 제한 없이 생성자를 호출할 수 있도록 한다. 

[**private 접근 제한**]  
 private 접근 제한은 동일한 패키지이건 다른 패키지이건 상관없이 생성자를 호출하지 못하도록 제한한다. 오로지 클래스 내부에서만 생성자를 호출할 수 있고 객체를 만들 수 있다.

 |접근제한|적용대상|접근할 수 없는 클래스|
 |:---:|:---:|:---:|
 |public|클래스,필드,생성자,메서드|없음|
 |private|필드,생성자,메서드|모든 외부 클래스|

 접근제한자에 대한 추가설명은 내일 진행하기로 한다고 한다.
