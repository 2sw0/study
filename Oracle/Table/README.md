Table
--
### All_Tables

현재 사용자가 액세스할 수 있는 관계형 테이블을 나타냄.
이 보기의 통계를 수집하려면 DBMS_STATS패키지를 사용
```sql
--Example
select owner,table_name,tablespace_name from all_tables where  owner NOT IN ('제외할 테이블소유자 나열')order by owner,table_name,tablespace_name;
```


### 테이블 복사하기 : 테이블 구조 + 데이터 복사
```sql
CREATE TABLE 새로만들테이블명 AS SELECT * FROM 복사할테이블명 [WHERE절];
```

### 특정 테이블 스페이스에 테이블 생성
```sql
CREATE TABLE [테이블명](
    내용
)
TABLESPACE [테이블스페이스명];
```
