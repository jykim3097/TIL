# Spring의 세가지 의존주입(DI) 방법
## 필드 주입
* 일반적인 방법, 내가 사용해왔던 방법이다.
```java
public class ClassA {
	
	@Autowired
	private ClassB b;

	public void MethodA() {
		//내용
	}
}
```
## Setter 주입
* 최근에 사용 중인 방법, 의존주입 공부를 다시 하게 된 이유!
```java
public class ClassA {
	
	private ClassB b;

	@Autowired
	public void setB(ClassB b){
		this.b = b;
	}

	public void MethodA() {
		//내용
	}
}
```
## 생성자 주입
* 공부하면서 알게 된 방법
* 생성자의 매개변수에 의존주입할 빈을 넣어 사용한다
* 스프링 4.3 버전 이후로 @Autowired를 안 넣어도 사용할 수 있다.
```java
public class ClassA {

	private ClassB b;

	public ClassA(ClassB b) {
		this.b = b;
	}

	public void MethodA() {
		//내용
	}
}
```
## 세가지 방법의 공통점과 차이점
* 세가지 방법은 같은 결과를 내지만
* 순환참조라는 상황에서 차이를 보인다.
* 필드, setter 주입 방식은 정상 동작하지만, 생성자 주입 방식은 에러가 발생한다.
### 이유는?
* 생성자 의존 주입은 객체를 생성자로 생성하는 시점에 필요한 빈을 의존주입한다.
* **즉, 객체를 생성하는 동시에 빈을 주입하는 것과 객체를 생성한 후에 빈을 주입한다는 것이 차이점이다.**
* 단순히 서로 참조하기 때문이 아니라, 서로 참조하는 객체가 생성되지도 않았는데, 그 빈을 참조하기 때문에 예외가 발생한 것이다.
* 그렇기 때문에 순환참조는 생성자 의존주입에서만 문제가 된다.
## 그래서? 순환참조를 피하기 위해 필드/Setter 주입만 사용해야되는가?
* 답은 아니다!
* 순환참조를 유발하는 객체가 잘못된 것이므로, 잘 설계된 객체인지 확인할 필요가 있다.

> 참고1 : https://coding-start.tistory.com/250
> 참고2 : https://yaboong.github.io/spring/2019/08/29/why-field-injection-is-bad/