### S3에서 RDS로 이동

1. mys3bucket이라는 이름의 Amazon S3 버킷의 모든 파일을 DATA_PUMP_DIR 디렉터리로 다운로드 (파일 압축X -> 압축 해제X)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.download_from_s3(
      p_bucket_name    =>  'mys3bucket',
      p_directory_name =>  'DATA_PUMP_DIR') 
   AS TASK_ID FROM DUAL;
```

2. db이라는 Amazon S3 버킷에서 접두사가 mys3bucket인 모든 파일을 DATA_PUMP_DIR 디렉터리로 다운로드  
(GZIP으로 압축 -> 압축 해제 적용O)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.download_from_s3(
      p_bucket_name          =>  'mys3bucket', 
      p_s3_prefix            =>  'db', 
      p_directory_name       =>  'DATA_PUMP_DIR',
      p_decompression_format =>  'GZIP') 
   AS TASK_ID FROM DUAL;
```

3. myfolder/이라는 Amazon S3 버킷의 mys3bucket 폴더에 있는 모든 파일을 DATA_PUMP_DIR 디렉터리로 다운로드  
p_s3_prefix 파라미터를 사용하여 Amazon S3 폴더를 지정  
(업로드된 파일은 GZIP으로 압축되지만, 다운로드 중에는 압축 풀리지 않음)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.download_from_s3(
      p_bucket_name          =>  'mys3bucket', 
      p_s3_prefix            =>  'myfolder/', 
      p_directory_name       =>  'DATA_PUMP_DIR',
      p_decompression_format =>  'NONE')
   AS TASK_ID FROM DUAL;
```

4. mys3bucket이라는 Amazon S3 버킷의 mydumpfile.dmp 파일을 DATA_PUMP_DIR 디렉터리로 다운로드 (파일 압축X -> 압축 해제X)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.download_from_s3(
      p_bucket_name    =>  'mys3bucket', 
      p_s3_prefix      =>  'mydumpfile.dmp', 
      p_directory_name =>  'DATA_PUMP_DIR') 
   AS TASK_ID FROM DUAL;
```

5. 각 예에서, SELECT 문은 VARCHAR2 데이터 형식으로 작업 ID를 반환
해당 작업 ID를 통해 작업의 출력 파일을 표시하여 결과를 볼 수 있음 (task-id를 절차에서 반환된 작업 ID로 대체)
```sql
SELECT text FROM table(rdsadmin.rds_file_util.read_text_file('BDUMP','dbtask-task-id.log'));
```
