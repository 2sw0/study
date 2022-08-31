### S3로 이동
```sql
aws s3 cp [덤프파일경로/덤프파일명].dmp s3://[주소]/

--결과
upload: ./[덤프파일명].dmp to s3://[주소]/[덤프파일명].dmp
```

### S3에서 RDS로 이동
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.download_from_s3(
      p_bucket_name    =>  '[S3 버킷 이름]', 
      p_s3_prefix      =>  '[폴더명]/[덤프파일명].dmp', 
      p_directory_name =>  'DATA_PUMP_DIR') 
   AS TASK_ID FROM DUAL;
 
--p_bucket_name : 파일을 업로드할 Amazon S3 버킷의 이름
--p_directory_name : 파일을 업로드할 Oracle 디렉터리 객체의 이름 (사용자가 생성한 디렉터리 객체 또는 Data Pump 디렉터리(예: DATA_PUMP_DIR)일 수 있음)
--(*지정된 디렉터리의 파일만 업로드할 수 있습니다. 지정된 디렉터리의 하위 디렉터리에서는 파일을 업로드할 수 없음)
--p_s3_prefix : 파일이 업로드되는 Amazon S3 파일 이름 접두사. 빈 접두사는 모든 파일을 지정된 Amazon S3 버킷의 최상위 레벨에 업로드하며, 접두사를 파일 이름에 추가하지 않음
--(*예를들어 접두사가 folder_1/oradb이면 파일이 folder_1에 업로드됨. 이 경우 oradb 접두사가 각 파일에 추가됨
```

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
```
