Table
--
### All_Tables

현재 사용자가 액세스할 수 있는 관계형 테이블을 나타냄.
이 보기의 통계를 수집하려면 DBMS_STATS패키지를 사용

### Example

```sql
select owner,table_name,tablespace_name from all_tables where  owner NOT IN ('제외할 테이블소유자 나열')order by owner,table_name,tablespace_name;
```

### 특정 테이블 스페이스에 테이블 생성
```sql
CREATE TABLE [테이블명](
    COL_01 VARCHAR2(10),
    COL_02 VARCHAR2(10),
    COL_03 VARCHAR2(10),
    COL_04 VARCHAR2(10)
)
TABLESPACE [테이블스페이스명];
```
