1. database별 용량 확인
### 쿼리
```
SELECT table_schema "Database", ROUND(SUM(data_length+index_length)/1024/1024,1) "MB" FROM information_schema.TABLES GROUP BY 1;
```

### du
```
du -h /var/lib/mysql
```
1. 전체 용량 확인
### 쿼리
```
SELECT SUM(data_length+index_length)/1024/1024 used_MB, SUM(data_free)/1024/1024 free_MB FROM information_schema.tables;
```

### du
```
du -sh /var/lib/mysql
```
