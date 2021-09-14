# Javascript prototype

## Prototype과 Class
* js는 객체지향 언어이지만 **Class라는 개념이 없다**
* 대신 Prototype이 존재하는데, 그래서 js가 Prototype 기반 언어라고 불린다
* Class가 없기 때문에 상속을 할 수 없지만, **Prototype으로 상속을 흉내내서 구현한다**
	* 함수와 new를 사용해 클래스를 비슷하게 흉내낼 수 있다
* ECMA6 표준에서 Class 문법이 추가되었지만, 이것이 클래스 기반으로 바뀌었다는 뜻은 아니다

## Prototype
* (함수명).prototype이라는 빈 Object가 어딘가에 존재하고,
* 함수로부터 생성된 (여러) 객체는 이 어딘가에 존재하는 Object에 들어있는 값을 모두 쓸 수 있다
* 그래서 **객체는 언제나 함수로 생성된다**


### Prototype Link와 Prototype Object
* Prototype = Prototype Link + Prototype Object

* 함수가 정의 될 때 2가지 일이 동시에 이루어지는데,
1. 해당 함수에 생성자(Constructor) 자격을 부여한다
	* 생성자 자격이 부여되면, new를 통해 객체를 만들어낼 수 있게 된다.
		* 함수만 new 키워드를 사용할 수 있는 이유!
2. 해당 함수의 Prototype Object가 생성되고 연결된다
	* 함수를 정의하면 함수와 Prototype Object가 같이 생성된다
	* 생성된 함수는 prototype이라는 속성을 통해 Prototype Object에 접근할 수 있다
	* Prototype Object는 일반 객체와 같고, 기본 속성으로 constructor와 __proto__를 갖고 있다
		* constructor는 Prototype Object와 같이 생성된 함수를 가리키고,
		* __proto__는 **Prototype Link**이다

#### prototype 속성은 함수만 갖고 있지만  __proto__ 속성은 모든 객체가 갖고 있는 속성이다

* 그래서 __proto__는 객체가 생성될 때 조상이었던 함수의 Prototype Object를 가리킨다
	* 함수로부터 생성된 객체가 어떤 속성을 갖고 있지 않더라고, 그 속성을 찾을 때까지 상위 prototype을 탐색해서 결과를 반환한다
		* 이때 찾지 못하면 undefined를 리턴한다
* 이렇게 __proto__ 속성을 통해 상위 프로토타입과 연결되어 있는 형태를 **프로토타입 체인(Chain)**이라고 한다

### Prototype Chain
* 이런 Prototype Chain 구조 때문에 모든 객체는 Object의 자식이라고 불린다


> 참고 : https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67