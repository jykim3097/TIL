# data attribute (dataset)

* html5부터 추가된 Data 속성
* html 요소의 **data-**로 시작하는 속성이다
* 특정 데이터를 DOM 요소에 저장해두기 위해 데이터 속성을 사용한다

## 장점
* hidden으로 태그를 숨겨두고 데이터를 저장할 필요가 없기 때문에, 스크립트가 간결해진다
* 하나의 html 요소에 여러 개의 데이터 속성을 동시에 사용할 수 있다
```html
<input type="text" data-value="1" data-code="3" />
```

## 특징
* dataset은 자바스크립트이기 때문에 속성명을 카멜케이스로 변환한다
* 예를 들어 data-value는 dataValue가 된다
* 또 반대로 dataset.value는 data-value가 된다
