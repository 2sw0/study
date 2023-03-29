### 1. database별 용량 확인

#### 쿼리
```
SELECT table_schema "Database", ROUND(SUM(data_length+index_length)/1024/1024,1) "MB" FROM information_schema.TABLES GROUP BY 1;
```
#### du
```
du -h /var/lib/mysql
```
### 2. 전체 용량 확인

#### 쿼리
```
SELECT SUM(data_length+index_length)/1024/1024 used_MB, SUM(data_free)/1024/1024 free_MB FROM information_schema.tables;
```
#### du
```
du -sh /var/lib/mysql
```
### 3. 테이블별 용량 확인
#### 쿼리
```
SELECT table_name AS 'TableName',
       ROUND(SUM(data_length+index_length)/(1024*1024), 2) AS 'All(MB)',
       ROUND(data_length/(1024*1024), 2) AS 'Data(MB)',
       ROUND(index_length/(1024*1024), 2) AS 'Index(MB)'
FROM   information_schema.tables
GROUP BY table_name;
```
