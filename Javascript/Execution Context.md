# Execution Context

- 마치 최종보스st인 실행 컨텍스트에 대해 정리해보고자 한다
- 그동안 함수선언식과 함수표현식의 차이, element와 node, property 등에 대해 이해를 해왔던 터라 이해하기가 수월했다.
- 그리고 이 개념을 기반으로 앞으로 호이스팅, 클로저 등에 대해 전보다 더 잘 이해할 수 있을 거라고 생각한다(...)
- 아래 페이지를 참조해서 정리했다
    
    > [https://poiemaweb.com/js-execution-context](https://poiemaweb.com/js-execution-context)
    > 
    
    > [https://velog.io/@won-developer/실행컨텍스트의-동작원리](https://velog.io/@won-developer/%EC%8B%A4%ED%96%89%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8%EC%9D%98-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC)
    > 
    
    > [https://mingcoder.me/2020/02/28/Programming/JavaScript/execute-context/](https://mingcoder.me/2020/02/28/Programming/JavaScript/execute-context/)
    > 

## 실행 컨텍스트란?

📢 자바스크립트에서 실행 가능한 코드들이 실행되는 환경

- 그리고 이 실행 가능한 코드에 따라 생성되는 컨텍스트가 다르다
- 실행 가능한 코드란?
    - 전역 코드 : 전역 영역에 존재하는 코드 → 전역 코드 실행 시 전역 컨텍스트 생성
    - 함수 코드 : 함수 내에 존재하는 코드 → 함수 실행 시 함수 컨텍스트 생성
    - eval 코드 : eval 함수로 실행되는 코드
    - 보통 실행 가능한 코드라고 하면, 전역 코드와 함수 코드를 의미한다
- scope, hoisting, closure, this 등의 동작 원리를 담고 있는 자바스크립트의 핵심 원리이다

## 실행 컨텍스트의 작동 원리

- 아래 함수를 예를 들어 실행 컨텍스트의 작동 원리를 살펴보자
    
    ```jsx
    var x = '내가 1등!';
    
    function func1 () {
      var y = ' 내가 2등!';
    
      function func2 () {
        var z = ' 내가 3등!';
        console.log(x + y + z); //내가 1등! 내가 2등! 내가 3등!
      }
      func2();
    }
    func1();
    ```
    
- 위 코드를 실행하면 아래와 같은 실행 컨텍스트 스택이 생성되고 소멸한다.
    
    ![실행컨텍스트.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/500fc572-1e32-4bde-ba93-6ae585d0a09e/실행컨텍스트.png)
    
    1. 컨트롤이 실행 가능한 코드로 이동하면, 논리적 스택 구조를 가지는 새로운 실행 컨텍스트 스택(Execute Context Stack)이 생성된다
    2. 컨트롤이 전역코드로 진입하면 전역 컨텍스트가 생성되고, 스택에 실행 컨텍스트 스택에 쌓인다
        1. 전역 컨텍스트는 애플리케이션이 종료될 때(웹페이지에서 나가거나 브라우저를 닫을 때)까지 유지된다
    3. 함수를 호출하면 해당 함수의 실행 컨텍스트가 생성되고 직전에 실행된 컨텍스트 위에 쌓인다
    4. 함수 실행이 끝나면 해당 함수의 실행 컨텍스트를 파기하고, 직전 실행 컨텍스트에 컨트롤을 반환한다

## 실행 컨텍스트의 구성요소

- 실행 컨텍스트는 실행 가능한 코드를 형상화하고 구분하는 추상적인 개념이지만,
- 물리적으로는 객체 형태를 띄고 있으며, 프로퍼티 3개를 갖고 있다.
    - Variable Object(변수 객체), Scope Chain(SC), this
        
        ```jsx
        // 객체 형태를 띈 실행 컨텍스트
        실행 컨텍스트 = {
        	Variable Object,
        	Scope Chain,
        	thisValue
        }
        ```
        

### Variable Object(VO, 변수객체)

- 실행 컨텍스트가 생성되면 자바스크립트 엔진은 실행에 필요한 정보들을 담을 객체를 생성하는데, 이를 변수객체라고 한다
- Variable Object는 코드가 실행될 때 엔진에 의해 참조되며, 코드에서는 접근할 수 없다
- Variable Object는 아래의 정보를 담고 있는 객체이다.
    - 변수
    - 함수선언
    - 매개변수(parameter) 또는 인수정보(arguments)
- 또, 변수객체는 실행 컨텍스트의 Property이기 때문에 값을 갖고 있는데, 이 값은 어떤 객체를 가리킨다.
    - 그런데 컨텍스트에 따라 가리키는 객체가 다른데, 이는 전역 코드와 함수의 내용이 다르기 때문이다. 예를 들어, 전역 코드에는 매개변수가 없지만 함수에는 매개변수가 있다
- 전역 객체(Global Object, GO)
    - 전역 컨텍스트가 가리키는 객체로, 최상위 객체이며 유일하다.
    - 모든 전역 변수와 전역 함수 등을 포함한다
    - 전역에 선언된 전역 변수와 전역 함수를 프로퍼티로 갖는다
        
        ![전역컨텍스트.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d1784ae2-38a1-46a3-83b6-342174742f74/전역컨텍스트.png)
        
- 활성 객체(Activation Object, AO)
    - 함수 컨텍스트가 가리키는 객체로, 전역 객체와 달리 arguments object가 있다.
    - arguments object는 매개변수와 인수들의 정보를 담고 있는 배열이다
        
        ![함수컨텍스트.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2120ebad-e30c-4b0c-9723-bd709e460c31/함수컨텍스트.png)
        

### Scope Chain(SC)

- 변수를 검색하는 메커니즘
    - 객체를 검색하는 매커니즘은 Prototype Chain
- 일종의 리스트로, 해당 전역 또는 함수가 참조할 수 있는 변수객체(전역객체 또는 활성객체)를 가리킨다
- 현재 실행 컨텍스트의 활성 객체를 선두로 해, 상위 컨텍스트의 활성 객체를 가리키며 마지막 리스트는 전역 객체를 가리킨다
    
    ![스코프체인.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/aa9a4499-3691-49ce-8ca1-c218d92bf976/스코프체인.png)
    
- 함수가 중첩되어 있으면, 중첩될 때마다 부모 함수의 Scope가 자식 함수의 스코프 체인에 포함된다
- 함수 실행 중에 변수를 만나면, 그 변수를 우선 현재 Scope인 AO에서 검색해보고, 값이 없다면 스코프 체인에 담겨진 순서대로 그 검색을 이어간다
- 이것이 스코프 체인이라고 불리는 이유다.
- 이처럼 순차적으로 스코프 체인에서 변수를 검색하다가 결국 검색에 실패하면, 정의되지 않은 변수에 접근하는 것으로 판단해 Reference 에러를 발생시킨다.
- 스코프 체인은 함수의 Property인 **[[Scope]]**로 참조할 수 있다

### This

- this에 할당되는 값은 일반적으로 전역 객체를 가리키고, 함수 호출 패턴에 의해 결정된다