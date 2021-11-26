# Property
- 어제부터 시작된 무한 공부의 늪.. ~~일도 없는데 잘됐지 모..~~
- parentNode와 parentElement의 차이가 궁금해서 공부를 시작했는데
- 마치 감자 캐는 것처럼 개념들이 우수수 딸려나와 실행 컨텍스트까지 공부하게 됐다는 story..
- Property 공부도 그 과정 중에 있었다 😊 (nodeType property에서 시작된 또 하나의 감자)
- 참조한 페이지는 아래와 같고, 이 페이지들을 망라해서 정리해보고자 한다.
    > [위키피디아](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D))  
    > [쉽게 읽는 프로그래밍](https://m.blog.naver.com/magnking/220966405605)  
    > [개발하는 감자](https://byul91oh.tistory.com/167)
  
# 정의를 정리해보자

## 위키백과ver.

📢 **일부 객체지향프로그래밍 언어에서 필드(데이터 멤버)와 메소드 간 기능의 중간인 클래스 멤버의 특수한 유형이다.**

- 그런데 무슨 말인지 하나도 이해가 안가고요... 기능의 중간이 중간 기능을 한다는 건지도 모호하다

## MDNver.

📢 해당 object의 특징으로, 보통 데이터 구조와 연관된 속성을 나타낸다

- Property는 아래와 같이 두 종류가 있다.
    - Instance property : 특정 object 인스턴스의 특정한 데이터를 갖고 있다
    - Static property(정적 프로퍼티) : 모든 object 인스턴스에 공유된 데이터를 갖고 있다
- property는 이름과 값으로 구성되어 있는데,
    - 값에는 원시함수(primitive), 메서드(method) 또는 객체 참조(object reference)가 있다.
    - 보통 **property가 object를 갖고 있다**고 말하는 것은 **property가 객체 참조를 갖고 있다**고 해석해야 한다
    - property 값이 변하더라도, object는 그대로 남아있기 때문이다

## 정리하자면

📢 Property는 '속성'이란 뜻으로, Javascript에서는 객체 내부의 속성을 의미한다.

📢 기본적으로 '어떤 값'을 의미하는데, 이 값이 객체(object)와 연관이 있을 때 property라고 부른다.

- length는 문자열이 담고 있는 문자의 양을 의미하는 대표적인 property이다.
- 객체(object)와 연관된 값을 담는 유형으로 변수와 비슷한 느낌을 준다
- 객체에 정의된 일반적인 property가 아닌 function을 담고 있는 값은 property이면서 method이다
    - 함수를 담고 있는 프로퍼티를 메소드라고 부르기 때문이다  
        
        ```jsx
        // 객체 선언
        var person = {name: "jiyoung"}

        // property 접근
        console.log(person.name); // jiyoung

        // property 수정
        person.name = "jiwon";
        console.log(person.name); // jiwon

        // property 추가
        person.age = 20;
        console.log(person.age); // 20

        // property 삭제
        delete person.age;
        console.log(person.age); // undefined
        ```

# Property의 6가지 특징

### value

- property의 속성 값으로 단지 값을 의미한다.
- value에 대한 접근권한자를 설정하기 위해 enumarable, writable, configurable을 이용한다

### get&set

- ES6에서부터 나오기 시작한 문법
- 객체 속성값(value)에 대한 접근권한자 역할을 할 수 있다
- 그래서 get과 set 자체가 writable 속성을 갖고 있어서  writable 속성과 함께 사용할 수 없다

### enumarable(열거할 수 있는)

- 객체 내 property가 열거할 수 있는 속성이라면(enumarable : true) 루프를 통해 값에 접근할 수 있다
- 열거 가능한 property의 key도 Object.keys()를 통해 반환받을 수 있다.
- 또, 조회 가능한 것과 열거 가능한 것은 엄연히 다른 의미이다.
    
    ```jsx
    var obj = {a:1,b:2};
    
    obj.c = 3;
    
    Object.defineProperty(obj, 'd', {
    	value = 4,
    	enumarable : false
    });
    
    console.log(obj.d); // 4 -> 조회는 가능하다!
    
    for(var key in obj) {
    	console.log(obj[key]); // 1, 2, 3 -> 열거할 수는 없다
    }
    
    console.log(Object.keys(obj)); // 'a', 'b', 'c'
    ```
    

### writable

- property가 쓸 수 있는 속성이라면(writable:true) 값을 수정할 수 있다
- 원시 속성
    
    ```jsx
    var obj = {a:1};
    
    Object.defineProperty(obj, 'b', {value:2, writable:false});
    
    obj.b = 3;
    obj.b = 4;
    
    console.log(obj.b); // 2 -> 변경되지 않는다
    ```
    

- 참조 속성
    
    ```jsx
    var obj = {a:1};
    
    Object.defineProperty(obj, 'ect', {value:{b:2}, writable:false});
    
    // writable:false 속성을 객체에 줬다면 객체 내부 수정은 가능하다
    obj.ect.c = 3;
    obj.ect.d = 4;
    console.log(obj.ect); // {c:3, d:4}
    
    // writable:false 속성을 갖는 객체는 수정할 수 없다
    obj.ect = 'hello';
    console.log(obj.ect); // {c:3, d:4}
    ```
    

### configurable

- 구성할 수 있는 Property(configurable:true)는 제거 여부를 의미한다
    
    ```jsx
    var obj = {};
    
    Object.defineProperty(obj, 'a', {value:1, configurable: true});
    delete obj.a;
    console.log(obj); // {}
    
    Object.defineProperty(obj, 'a', {value:1, configurable: false});
    delete obj.a;
    console.log(obj); // {a:1}
    ```
