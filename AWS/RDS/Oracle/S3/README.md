### S3로 이동
```sql
aws s3 cp [덤프파일경로/덤프파일명].dmp s3://[주소]/
--결과
upload: ./[덤프파일명].dmp to s3://[주소]/[덤프파일명].dmp
```

### S3에서 RDS로 이동
### [S3->RDS](./S3->RDS.md)

### RDS에서 S3로 이동
### [RDS->S3](./RDS->S3.md)

### 확인
```sql
--BDUMP 디렉토리에 로그를 출력
--upload 처리를 실행했을 때에 TASK_ID를 반환하므로, 파일명을 dbtask-(TASK_ID).log로 설정하면 SQL로 해당 로그 확인 가능
SELECT text FROM  table(rdsadmin.rds_file_util.read_text_file('BDUMP','dbtask-1573713349502-624.log'));
```

### RDS 디렉토리, 파일 확인
```sql
SELECT * FROM TABLE(rdsadmin.rds_file_util.listdir('DATA_PUMP_DIR')) ORDER BY MTIME;
```

### 삭제
```sql
--S3에 업로드 할 수 있는지 확인한 후 DATA_PUMP_DIR위의 dump 파일을 삭제합니다. 삭제에는 UTL_FILE.FREMOVE프로 시저를 사용합니다.
exec utl_file.fremove( location => ' DATA_PUMP_DIR ' , filename => ' zunda-20191114.dmp ' );
exec utl_file.fremove( location => ' DATA_PUMP_DIR ' , filename => ' zunda-export-20191114.log ' );
EXEC UTL_FILE.FREMOVE('DATA_PUMP_DIR', '[파일 이름].dmp');
```
