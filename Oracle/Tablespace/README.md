Tablespace
--

### default Tablespace 확인
```sql
SELECT * FROM USER_USERS ;
```

### Tablespace 이름으로 관련 data file 찾기
```sql
SELECT file_name, tablespace_name, bytes FROM dba_data_files WHERE tablespace_name = '[TablespaceName]'
```

### Tablespace 크기 늘리기
```sql
--(1) data file 추가(가장 많이 쓰는 방법)
ALTER TABLESPACE <tablespace name> ADD DATAFILE '[FILE_NAME]' SIZE [숫자 k or m];

--(2) 기존의 data file 크기 변경
ALTER DATABASE DATAFILE '[FILE_NAME]' RESIZE [숫자 k or m];

--(3) datafiledml size를 자동으로 늘어나게 하는 명령
ALTER DATABASE DATAFILE '[FILE_NAME]' AUTOEXTEND ON MAXSIZE UNLIMITED;
```
