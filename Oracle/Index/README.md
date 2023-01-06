Index
===
### [DESC_INDEX](./DESC_INDEX/README.md)
### 생성
```sql
CREATE INDEX owner_name.index_name ON owner_name.table_name(column_name1, column_name2, column_name3 ...) TABLESPACE tablespace_name;
```

### 테이블의 인덱스 확인
```sql
SELECT   INDEX_NAME, COLUMN_NAME, COLUMN_POSITION
FROM     ALL_IND_COLUMNS
WHERE    TABLE_OWNER = 'owner_name' AND TABLE_NAME = 'table_name'
ORDER BY INDEX_NAME, COLUMN_POSITION;
```

### 인덱스가 속한 테이블스페이스 확인
```sql
SELECT   INDEX_NAME,TABLESPACE_NAME
FROM     ALL_INDEXES
WHERE    TABLE_NAME = 'table_name'
ORDER BY INDEX_NAME
```
