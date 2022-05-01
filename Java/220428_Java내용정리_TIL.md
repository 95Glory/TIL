# 22.04.28 Java 수업 내용정리:pencil2:
## **1. 상속과 오버라이딩**:pushpin:
* 기존의 클래스로 새로운 클래스를 작성하는 것.(코드의 재사용)
* 두 클래스를 부모와 자식으로 관계를 맺어주는 것
* 클래스의 확장개념으로 이해하자  
* 하위 클래스 즉,  자식클래스는 부모클래스로부터 멤버변수 및 행동메서드를 전부 할당 받을 수 있다.
* 때문에 하위 클래스 생성시, extends로 부모클래스로 상속을 받게 하였다면 멤버변수시 부모클래스에서 생성한 멤버변수들 혹은 메서드를 또 다시 만들 필요가 없다.


**문법 : class A extends B**
A : 상속 받을 하위 클래스
B : 상속 할 상위 클래스
* 상위 클래스는 하위 클래스보다 일반적인 의미를 가짐
* 하위 클래스는 상위 클래스보다 구체적인 의미를 가짐

**오버라이딩 메소드 (Override)**
상위클래스에서 하위클래스로부터 변수들을 상속하였다.
예를 들자면 동물이라는 상위 클래스가 존재하고  동물들의 울음소리를 표현하는  메서드를 부여하였다.  

그다음 쥐라는 하위클래스를 생성하고 상위 클래스에서 상속받은 sing 이라는 메서드를 실행할 건데, 쥐 클래스 만의 울음소리를 나타내고 싶다면 메서드의 값이 달라져야 할 것 이다. 때문에 오버라이딩 메서드를 활용하여 클래스마다의 다른 값을 출력시킬수 있게 할 수 있다. 
 
실전 예제를 통해  상속과 오버라이딩 메서드를 이해해보자

```java
public class Animal {
	// int age, String color 필드
	private int age; // 멤버 변수 중에서 인스턴스 변수
	private String color; // age와 마찬가지

	// 모든 필드를 매개변수로 받는 생성자
	public Animal(int age, String color) {
		super();
		System.out.println("Animal(age, color) 호출");
		this.age = age;
		this.color = color;
	}
	
	// setter, getter
	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}
	
	// void sing
	public void sing() {
		System.out.println("동물은 어떻게 울지?");
	}
}
```
구현사항
1. Animal 이라는 클래스를 생성. 우리는 이 클래스를 최상위 클래스로 정의할 것이다.(최상위 클래스임을 명시하는 부분은 없다 그냥 개발자가 인식해야 하는 부분이다.)    
2. age, color 로 동물에 대한 나이와 색상을 명시해 줄 수 있는 멤버변수를 생성하였다.  추가로 앞에 private 키워드를 붙여 다른 파일에서 함부로 변수값을 설정하지 못하도록 사전차단을 하였다.
3.  생성자 함수를 통해 동물 클래스에 멤버변수를 사용가능 하게끔 설정을 해주었다.  
4. getter / setter 메서드를 부여하여 private으로 외부파일에서 값을 조작하는걸 방지했으니 값을 설정하고 불러올수 있는 기능을 구현하였다.
```java
public class Mouse extends Animal {
	// Mouse is an Animal 성립.
	// Mouse는 Animal이다.
	// Animal 클래스가 가진 특성을 물려받을 수 있다. + 자신만의 특성을 확장할 수도 있다.
	// 특성 : 필드와 메서드

	private String address;

	public Mouse(int age, String color, String address) {

		// age,color 필드는 상위 클래스인 Animal이 가지고 있기 때문에
		// 해당 필드의 초기화는 해당 클래스에게 맡김
		super(age, color); // 상의 클래스의 생성자 호출
		this.address = address;
	}

	public String getAddress() {
		return address;
	}

	public void setAddress(String address) {
		this.address = address;
	}

	// 상위 클래스의 메서드(sing()) 재정의(Override)
	// 자신만의 특성에 맞게
	// public void sing() {
	// System.out.println("찍찍!");
	// }

	@Override // 해당 메서드가 overriding 되었다는 것을 의미하는 표기법
	public void sing() {
		System.out.println("찍찍!");
	}

	@Override
	public String toString() {
		// TODO Auto-generated method stub
		return super.getAge() + " "+super.getColor()+ " "+address;
	}
```

1. 동물이라는 클래스에서 상속해줄 하위 클래스 Mouse 클래스를 만들었다.  

2. 상속받는 쥐 클래스는 extends 키워드를 사용하여 상속받을 class인 Animal를 명시해주었다  

3. 쥐 클래스만의 멤버변수를 추가하기 위해 address 멤버변수를 추가적으로 생성을 해 주었다. 이 address 변수는 상위클래스인 animal 클래스에서의 사용은 불가능 하다.

4. 쥐 클래스의 생성자 함수를 작성한다. 우리는 이미 animal 클래스에서 age 와 color 변수를 선언해주었기 때문에 변수의 초기화는 상위 클래스인 animal 클래스에게 맡긴다,

5.  생성자 함수를 만들고 괄호에 사용할 멤버변수들을 정의해 준다.

6. 초기화 작업시, 우리는 this 키워드를 사용하여 초기화를 해주었는데 age, color는 상위 클래스에서 이미 진행하였기 때문에 상위 클래스에서 상속받는 다는 키워드 super 키워드를사용하여 괄호안에 상속받을 멤버변수를 자료형을 제외하고 변수명만 기입을 해준다.  

7. animal 클래스에서 우린 sing 이라는 메서드를 만들었고 "동물은 어떻게 울까?"를 출력하게 하였지만 mouse 클래스에서는 찍찍! 이라고 출력이 되게끔 오버라이딩 작업을 해주었다.  

8. 우리는 animal 클래스를 최상위 클래스로 알고 있지만, 사실 클래스 선언은 안하였지만 눈에 보이지 않는 상위 클래서 object 클래스가 존재한다. 한 마리도 상속을 받지 않은 클래스는 전부 object 클래스를 상속받고 object 클래스 안에는 11가지의 메서드가 존재하며 그 중 하나인 toString을 사용하였다.

 **[static 변수]**
static변수란 인스턴스(객체)를 생성하기 전에 사용이 가능한 변수이다.

우리는 클래스를 생성하고 멤버변수를 선언하고 해당 클래스의 객체를 만들시, 멤버변수를 사용 할 수 있었다,    
static 변수는 멤버변수 선언시 static 이라는 키워드를 붙이면 객체를 생성하기 전에도 그 변수가 사용이 가능하게끔 하는 키워드 이다.

---   

## **2. 다형성( polymorphism)**:pushpin:  

* 여러 가지 형태를 가질 수 있는 능력  

* 객체지향프로그래밍에서 중요한 개념 중 하나라고 하고, 다형성을 이해를 못한다면 인터페이스, 추상클래스를 이해하기란 쉽지 않다고 한다.  

* 참조변수의 타  입과 인스턴스 타입이 일치하여야 했지만 불일치 하여도 인스턴스 생성이 가능하다. 단, 상위 하위 클래스의 연계성이 있어야 한다.

```java
public class Animal {
	String myClass;
	
	Animal(){
		myClass = "동물";
	}
	
	void showMe() {
		System.out.println(myClass);
	}
```
```java
public class Mammal extends Animal { 
// 포유류는 동물이다.
	//Animal은 상위 클래스, Mammal : 하위 클래스
	Mammal(){
		myClass = "포유류";
	}
}
```
```java
public class Cat extends Mammal{
	Cat(){
		myClass = "고양이";
	}
}
public class Whale extends Mammal{
	Whale(){
		myClass = "고래";
	}

}
```
**[구현사항]**
1. Animal 이라는 최상위 클래스 생성
2. Animal을 상속받는 Mammal 클래스 생성
3. Mammal을 상속받는 Cat, Whale 클래스 생성
4. 각 클래스마다 어떤 클래스인지 알려주는 메서드를 생성, 메서드 이름은 각 동물의 이름으로 짓는다.
5. Animal 클래스에서 showme 메서드를 생성

```java
Animal animal = new Animal();
		Animal mammal = new Mammal();
		Animal whale = new Whale();
		Animal cat = new Cat();
		
		Animal[] animals = new Animal[4];
		animals[0] = animal;
		animals[1] = mammal;
		animals[2] = whale;
		animals[3] = cat;

		for (Animal anAnimal : animals) {
			anAnimal.showMe(); 
			//일괄적으로 호춯가능
		}
```
위 처럼 인스턴스의 타입을 상속하는 Aniaml타입을 참조변수의 타입으로 사용하여도 객체가 만들어질 수 있다.  

위처럼 다형성을 활용하면 배열을 생성하여 animal 클래스의 animals 라는 참조변수에서 일괄적으로 관리가 가능하다.






