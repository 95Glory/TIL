# 22.05.31 Spring Boot수업 내용정리:pencil2:
## 1. Spring Boot란?:pushpin:
Spring framework를 사용하기 위한 필수 설정파일을 작성해야하고 이를 다 외우는건 사실상 불가능 하기에 기존의 사용설정을 복붙 하거나 개발자가 일일히 검색을 통해 설정해주어야 했다. 이는 곧 생산성이 떨어져 비용문제로 직결된다. 하지만 스프링 부트를 사용하면 복잡한 설정 없이 쉽고 빠르게 스프링 프레임워크를 사용할 수 있다.

특히,스프링 부트는 WAS인 Tomcat을 내장하고 있다. @SpringBootApplication 어노테이션이 선언되어 있는 클래스의 mail()메소드를 실행하는 것만으로 서버를 구동시킬 수 있다.   
내장 톰캣을 사용하기 위한 별도 설정없이 web starter 의존성만 추가해주면 된다.

Spring Boot 프로젝트를 생성하여 간단한 CRUD를 PostMan이라는 프론트의 개입없이 백엔드 서버를 테스트 할 수 있는 웹으로 실행을 확인해보려고 한다. 

이클립스에서 스프링 부트 프로젝트 생성방법
참고 : https://daslyee.tistory.com/80

**[DemoApplication]**
```java
package dev.sample.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

}
```
@SpringBootApplication 어노테이션을 사용하여 자바에서 서버를 열 수 있게한다.  
기존 Tomcat을 사용하여 프로젝트에 대해 설정을 하고 builder path를 설정하는 등, 여러 설정을 할 필요없이 Spring Boot 가 Tomcat을 내장하고 있어 우리는 별도의 설정이 필요가 없다.  
@SpringBootApplication 어노테이션만 있다면 main메소드에서 바로 서버연결이 가능한점이 특징이다.



**[Todo]**
```java
package dev.sample.demo.model;

//import 생략

//lombok적용

@Builder
@RequiredArgsConstructor
@AllArgsConstructor
@Setter @Getter
@ToString
@Entity
public class Todo {
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	private String title;
	private String description;
	private LocalDate date;
	}
```
우리가 관리하여야 할 Entity에대해 구성필드를 정의하여 준다 코드 서두에 보면 여러가지의 에노테이션들이 많은데 하나씩 알아보자.  

**@Builder**
복합 객체의 생성 과정과 표현 방법을 분리하여 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴이다. 생성자 인자로 너무 많은 인자가 넘 져지는 경우 어떠한 인자가 어떠한 값을 나타내는지 확인하기 힘들다. 또 어떠한 인스턴스의 경우에는 특정 인자만으로 생성해야 하는 경우가 발생한다. 특정 인자에 해당하는 값을 null로 전달해줘야 하는데, 이는 코드의 가독성 측면에서 매우 좋지 않다는 것을 알 수 있다.

이러한 문제를 해결하기 위해서 빌더패턴을 사용할 수 있습니다.

**@RequiredArgsConstructor**
* final 필드, @NonNull 필드 대상
* null check 코드포함
@RequiredArgsConstructor는 각각의 필드에 대해서 1개의 파라미터를 가진 생성자를 만든다. 그리고 final, @NonNull 키워드에 대해서만 동작을 한다.
**@NonNull**이란 null을 포함하지 않을 경우를 말한다.

**@AllArgsConstructor**
* 모든 파라미터가 포함된 생성자
* @NonNull / null check 코드 포함

**@Setter, @Getter**
Setter,Getter 메서드를 사용하는 방법 및 이유는 사전에 학습한 내용이므로 현재 이해하고 있기 때문에 이번에는 설명을 넘어간다.

**@ToString**
객체의 주소값이 아닌, 객체를 설명해주는 문자열을 리턴한다.

**@Entity**
- @Entity가 붙은 클래스는 JPA가 관리하는 것으로, 엔티티라고 불리우며 테이블로 매핑한다.

**> 주의사항**

- 기본 생성자는 필수 (JPA가 엔티티 객체 생성 시 기본 생성자를 사용)

- final 클래스, enum, interface, inner class 에는 사용할 수 없음

- 저장할 필드에 final 사용 불가

**[TodoController]**
```java
package dev.sample.demo.controller;
// import 생략
@RestController
@RequestMapping("api/v1") // localhost:8080/api/v1까지 작성해야 todocontroller에 접근할 수 있음. baseUrl임
public class TodoController {

	@Autowired // 필드를 통한 DI(injection) 뒤에 = new TodoServiceImpl(); 생기는 것과 동일하다. 컨테이너에 연결해서 자동으로
				// 생성해준다.
	private TodoService todoService;

//	@RequestMapping(value="/get", method=RequestMethod.GET)

	@GetMapping
	public List<Todo> findAll() {
		// 실제 DB에 접근해서 전체 Todo를 가져오는 코드를 작성
//		TodoService service  = new TodoServiceImpl(); //의존성을 주입받지 않은 방법
		// 생성자 함수로 주입받는 방법을 활용했다 .bankstatement3에서 확인 아날라이져에서 파서를 필요로함.
		return todoService.findAll();
	}

	// post 요청
	@PostMapping
	public Todo save(@RequestBody Todo todo) {
		// @RequestBody - 클라이언트에서 보낸 값을 Todo의 필드와 맵핑해서 객체 형태로 바인딩
		return todoService.save(todo);
	}

	// putmapping
	@PutMapping
	public List<Todo> update(@RequestBody Todo todo) {
//		System.out.println(todo);
//		Todo(id=null, title=고양이만지기, description=고양이를 만진다., date=2022-05-31)
		return todoService.update(todo);
	}
}
```

**@RestController**

전통적인 Spring MVC의 컨트롤러인 **@Controller는 주로 View를 반환하기 위해 사용**한다.  
Spring MVC Container는 Client의 요청으로부터 View를 반환한다.  

하지만 **Spring MVC의 컨트롤러를 사용하면서 Data를 반환해야 하는 경우**도 있다.   
컨트롤러에서는 데이터를 반환하기 위해 @ResponseBody 어노테이션을 활용해주어야 한다.  
이를 통해 Controller도 Json 형태로 데이터를 반환할 수 있다.

**@RestController는 @Controller에 @ResponseBody가 추가된 것이다.**
당연하게도 RestController의 주용도는 Json 형태로 객체 데이터를 반환하는 것이다.   
최근에 데이터를 응답으로 제공하는 REST API를 개발할 때 주로 사용하며 객체를 ResponseEntity로 감싸서 반환한다. 이러한 이유로 동작 과정 역시 @Controller에 @ReponseBody를 붙인 것과 완벽히 동일하다.

**@Controller와 @RestController는 용도의 차이**라고 이해하면 될 것 같다.  
예전에 프로그래밍을 할 때에는 **jsp나 html과 같은 뷰를 전달해 주었기 때문에 @Controller를 사용해왔었지만, 최근에는 프론트엔드와 백엔드를 따로 두고, 백엔드에서는 REST API를 통해 json으로 데이터만 전달**하기 때문에 편리성을 위해 @RestController를 사용하게 되었다고 한다.

**@RequestMapping**  

우리는 특정 uri로 요청을 보내면 Controller에서 어떠한 방식으로 처리할지 정의를 한다.
이때 들어온 요청을 특정 메서드와 매핑하기 위해 사용하는 것이 @RequestMapping이다.
@RequestMapping에서 가장 많이사용하는 부분은 value와 method이다. value는 요청받을 url을 설정하게 된다. method는 어떤 요청으로 받을지 정의하게 된다.(GET, POST, PUT, DELETE 등)

하지만 각 메소드 마다 value가 같다면 일일히 다 써줘야 할까? 아니다, 해당하다 클래스 바로 위에 단 한번의 작성으로 클래스 안에있는 메서드에게 각자 전달이 완료가 되므로 각 메서드에는 
RequestMethod의  에노테이션만 작성해주면 된다.  

**[해당예시]**
```java
@RestController
@RequestMapping(value = "/hello") 
public class HelloController { 
@GetMapping() public String helloGet(...) { ... } 
@PostMapping() public String helloPost(...) { ... } 
@PutMapping() public String helloPut(...) { ... } 
@DeleteMapping() public String helloDelete(...) { ... } }
```


**[@RequestBody]**
@RequestBody는 클라이언트가 전송하는 Json(application/json) 형태의 HTTP Body 내용을 Java Object로 변환시켜주는 역할을 한다. 그렇기 때문에 Body가 존재하지 않는 HTTP Get 메소드에 @RequestBody를 활용하려고 한다면 에러가 발생하게 된다. @RequestBody로 받는 데이터는 Spring에서 관리하는 MessageConverter들 중 하나인 MappingJackson2HttpMessageConverte를 통해 Java 객체로 변환된다. 

Spring은 메세지를 변환되는 과정에서 객체의 기본 생성자를 통해 객체를 생성하고, 내부적으로 Reflection을 사용해 값을 할당하므로 @RequestBody에는 값을 주입하기 위한 생성자나 Setter가 필요 없다.

**[TodoRepository]**
```java
package dev.sample.demo.repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import dev.sample.demo.model.Todo;

@Repository
public interface TodoRepository extends JpaRepository<Todo, Long> { //<엔티티이름, id 타입>
}
```
Entity에 의해 생성된 DB에 접근하는 메서드(ex) findAll()) 들을 사용하기 위한 인터페이스이다. 위에서 엔티티를 선언함으로써 데이터베이스 구조를 만들었다면, 여기에 어떤 값을 넣거나, 넣어진 값을 조회하는 등의 CRUD(Create, Read, Update, Delete)를 해야 쓸모가 있는데, 이것을 어떻게 할 것인지 정의해주는 계층이라고 생각하면 된다.    

**[TodoRepository]**
  **JpaRepository**를 상속받도록 함으로써 기본적인 동작이 모두 가능해진다. JpaRepository는 어떤 엔티티를 메서드의 대상으로 할지를 다음 키워드로 지정한다.   
  **JpaRepository<대상으로 지정할 엔티티, 해당 엔티티의 PK의 타입>**
이렇게 extends를 통해서 상속받고나면, 해당 레포지토리의 객체를 이용해서 기본적으로 제공되는 메서드(save(), findAll(), get()) 등을 사용할 수 있게 된다.
```java
package dev.sample.demo.service;
//import 생략
@Service //@Component의 직관적인 네이밍 표기
//TodoService의 구현 클래스 
public class TodoServiceImpl implements TodoService{
	
	@Autowired // 너가 좀 찾아줘서 생성해줘
	private	TodoRepository repository;
	
	@Override
	public List<Todo> findAll() {
		//비지니스 로직 작성 부분
		
		
		//DB 접근해서 데이터 조회-> service가 하지않고, DAO, Repository가 한다.
		//JPARepository에서 내장 메서드인 findAll() 사용
		return repository.findAll();
		
		//JDBC에서는 ORM처리가 필요.
		/*// Object(Mouse) - Relation(Mouse table) Mapping
		 * Mouse mouse = new Mouse();
		 * mouse.setName(rs.getString("name")); 
		 */		
	}
	
	
	public Todo save(Todo todo) {
		return repository.save(todo);
	}


	@Override
	public List<Todo> update(Todo todo) {
		
		//기존의 순수 JPA Hibernate
		// Todo todo = em.find(Todo.class, 1L)
		// 이거는 아이디값을 지정해줘서 그것을 수정하는 것이다.
		
		//Id값에 의해서 데이터조회 SELECT * FROM todo WHERE = id
		final Optional<Todo> foundTodo = repository.findById(todo.getId());
		//Optional: Nullpointer 예외를 방지하기 위한 장치 라잌 섬팅
		foundTodo.ifPresent(newTodo -> {//id값에 의한 엔티티가 존재하면 (ifpresent)
			newTodo.setDate(todo.getDate());
			newTodo.setDescription(todo.getDescription());
			newTodo.setTitle(todo.getTitle());
			//지역변수todo: update할 새로운 데이터
			//newtodo: update완료한 후 DB에 persist 할 데이터
			repository.save(newTodo);//em.psersist()
		});
		return repository.findAll();//전체데이터 반환(조회)
	}
}
```
@Contoller 어노테이션을 붙이면 핸들러가 스캔할 수 있는 빈(Bean) 객체가 되어 서블릿용 컨테이너에 생성이 된다. 마찬가지로 **@service 어노테이션은 해당 클래스를 루트 컨테이너에 빈(Bean) 객체로 생성**해주는 어노테이션이다.

둘 다 Bean 객체를 생성해주고 딱히 다른 기능을 넣어주는게 아니라서 뭘 써도 상관 없긴한데 명시적으로 구분해주기 위해 각자 분리해서 사용한다. 부모 어노테이션인 @Component를 붙여줘도 똑같이 루트 컨테이너에 생성되지만 가시성이 떨어지기 때문에 잘 사용하지 않는다.


-   컨트롤러 : @Controller  (프레젠테이션 레이어, 웹 요청과 응답을 처리함)
-   로직 처리 : @Service  (서비스 레이어, 내부에서 자바 로직을 처리함)
-   외부I/O 처리 : @Repository (퍼시스턴스 레이어, DB나 파일같은 외부 I/O 작업을 처리함)

이렇게 해두면 이제 이 클래스는 **루트 컨테이너에 빈(Bean) 객체로 생성**된다.**DB 작업을 위해 이 DAO 객체를 불러오려면 new를 이용해 생성하면 안되고 컨테이너에서 받아와야 한다.** 루트 컨테이너의 객체는 어디서든 공유가능하기 때문에, 아래와 같이 자동 의존성 주입(DI) 어노테이션을 이용해 객체를 받아올 수 있다.

이 어노테이션들은 같은 빈(Bean) 객체에서만 작동하는 것이기 때문에 Bean으로 만들지 않은 일반 클래스에서 사용해봤자 아무 소용 없다. 하지만 일부 DTO객체 등 데이터 변경 작업을 동반하는 클래스 외, 로직을 가진 클래스들은 대부분 @Service 어노테이션을 통해 Bean 객체로 등록해주므로 크게 문제될 일은 없다.

**@Autowired**
-   필요한 의존 객체의 “타입"에 해당하는 빈을 찾아 주입한다.
    -   생성자
    -   setter
    -   필드
   
    위의 3가지의 경우에 Autowired를 사용할 수 있다. 그리고 Autowired는 기본값이 true이기 때문에 의존성 주입을 할 대상을 찾지 못한다면 애플리케이션 구동에 실패한다. 

