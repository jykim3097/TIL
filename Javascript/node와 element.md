# node와 element
- parentNode와 parentEelement의 차이가 궁금해서 찾아보기 시작했는데,
- 둘의 차이를 공부하기 앞서 node와 element의 개념을 잡고 가야할 것 같다
    > 출처1) [https://dev-dain.tistory.com/128](https://dev-dain.tistory.com/128)    
    > 출처2) [https://hianna.tistory.com/412](https://hianna.tistory.com/412)

### Element ⊂ Node

- node
    - DOM 계층구조에 속한 객체의 어떤 타입이든 가리킬 수 있는 '이름'
    - 즉, doument객체도 node이고 input 태그, p태그 등도 node라고 할 수 있다
- **element**는 이 node의 한 타입
    - html의 태그 또는 id or class 속성을 가진 것처럼 특정할 수 있는 것을 의미
- 각각의 node들은 .nodeType 프로퍼티를 갖고 있는데, 이것이 그 node의 타입을 알려준다

### .nodeType 프로퍼티

- node의 type을 상수로 리턴
    
    | 리턴 상수 | 타입 | 예제 |
    | --- | --- | --- |
    | 1 | element | <p />, <div /> 등 |
    | 3 | text | Hello |
    | 4 | CDATA Section | <!CDATA[[...]]> |
    | 7 | ProcessingInstruction | <?xml-stylesheet... ?> |
    | 8 | Comment (주석) | <!-- comment -→ |
    | 9 | Document | document |
    | 10 | DocumentType | <!DOCTYPE html> |
    | 11 | DocumentFragment |  |

### parentNode와 parentElement의 차이

- parentNode는 DOM 트리에서 특정 노드의 parent 노드를 반환한다
- parent노드가 element노드라면 parentElement와 같은 값을 반환한다
- 그런데 document와 documentFagment 노드처럼 **부모 노드가 없으면 null을 반환한다**
       
- parentElement은 부모가 꼭 요소여야만 element형식으로 반환하고, 그렇지 않으면 null을 반환한다
- 즉, 노드의 부모 요소를 반환하는데, **부모 요소가 없거나 DOM 요소가 아니면 null을 반환한다**
- 즉, parentElement의 반환값은 항상 DOM element이거나 null이다
