# Delete와 Truncate

## Delete
* 데이터만 삭제되고 메모리는 줄어들지 않는다
* 삭제한 내용을 되돌릴 수 **있다**
* 전체 데이터 혹은 일부만 삭제가 가능하다
* Truncate에 비해 속도가 느리다

### 테이블 내용 삭제
1. 특정 레코드만 삭제
```sql
DELETE TABLE test WHERE tno = 1;
```

2. 전체 데이터 삭제
```sql
DELETE TABLE test;
```

## Truncate
* 테이블의 초기 상태로 되돌린다
* 메모리가 줄어들고, 인덱스 등도 삭제된다
* 삭제후 되돌릴 수 **없다**
* 전체 삭제만 가능하다

```sql
TRUNCATE test;
```