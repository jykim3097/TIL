> [lodash-uniqby()-메소드-알아보기](https://webisfree.com/2020-09-17/lodash-uniqby()-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)

- 중복체크 코드를 짜면서 이코드 저코드 공부해보다가 발견했다.
- lodash 업데이트를 통해 unique()에서 분리된 메소드 중 하나
- **컬렉션 데이터를 기준값에 따라 고유한 값만 가져오는 메소드**
- 첫번째 인자 : 컬렉션 데이터(객체 배열 등), 두번째 인자 : 기준 값
    - 컬렉션 데이터가 아닌 단순 배열은 uniq() 함수 사용

```jsx
arr = [
	{a:1, b:2},
	{a:2, b:2},
	{a:2, b:2}
]

// 기준값이 a인 경우
newArr = _.uniqBy(arr, 'a');

// 출력 결과
newArr = [
	{a:1, b:2},
	{a:2, b:2}
]

// 기준값이 b인 경우
newArr = _.uniqBy(arr, 'b');

// 출력 결과
newArr = [
	{a:1, b:2}
]
```