# INSERT INTO SELECT 구문
> 참고)  [https://makand.tistory.com/entry/SQL-INSERT-INTO-SELECT-구문](https://makand.tistory.com/entry/SQL-INSERT-INTO-SELECT-%EA%B5%AC%EB%AC%B8)
- 같은 내용의 테이블 데이터를 복사하는데 사용

```sql
INSERT INTO table1
SELECT * FROM table2;
```

- 이미 작성되어 있는 table1에 table2의 내용을 모두 복사한다.
- 일반적인 INSERT문과 마찬가지로, 일부 컬럼에만 적용할 수 있다

```sql
INSERT INTO table1(id, name, age)
SELECT id, name, age FROM table2;
```

- table1에 SELECT문을 복사하는 것인데, SELECT문에는 WHERE절, JOIN문 등 여러가지로 응용해서 사용할 수 있다.