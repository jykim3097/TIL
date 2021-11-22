# 데이터 삽입 시 PK 또는 UK가 중복되었을 경우

> 참고) [https://bamdule.tistory.com/112](https://bamdule.tistory.com/112)
- PK나 Unique key가 중복되었을 때

### ON DUPLICATE KEY UPDATE

- 데이터 삽입 시, PK나 UnIque Key가 중복되었을 경우 지정한 데이터만 update하는 명령어
- 중복된 키가 없을 경우 insert문을 수행한다

```sql
// 테이블 생성
CREATE TABLE member (
	id INT AUTO_INCREMENT primary key,
	name VARCHAR(50) UNIQUE KEY,
	price INT NOT NULL DEFAULT 0,
	cnt INT NOT NULL DEFAULT 0
);
```

```sql
// 데이터 삽입
INSERT INTO member (NAME, PRICE, CNT) 
VALUES ('kim', 1000, 0)
ON DUPLICATE KEY UPDATE 
	price = price * 2,
	cnt = cnt + 1;
```

- kim이라는 이름으로 데이터가 처음 삽입될 경우에는 1 | kim | 1000 | 0 으로 삽입되지만
- kim이라는 이름으로 중복으로 데이터가 삽입될 경우, 무결성 제약조건에 위배되므로 update문이 실행된다.
- 그래서 1 | kim | 2000 | 1 로 데이터가 업데이트 된다.
- 즉, name 값이 중복되므로 price와 cnt가 지정된 값에 따라 수정되었다.

---

### INSERT IGNORE

- 무결성 제약조건 위배 시 INSERT를 무시하는 명령어

```sql
INSERT IGNORE INTO member (NAME, PRICE, CNT)
VALUES ('kim',1000,0);
```

---

### REPLACE INTO

- 무결성 제약조건 위배 시 해당 레코드를 삭제하고 다시 삽입하는 명령어

```sql
REPLAC INTO member (NAME, PRICE, CNT)
VALUES ('kim',1000,0);
```