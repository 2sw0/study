### RDS에서 S3로 이동
1. DATA_PUMP_DIR 디렉터리에 있는 모든 파일을 mys3bucket이라는 이름의 Amazon S3 버킷에 업로드 (파일 압축 X)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.upload_to_s3(
      p_bucket_name    =>  'mys3bucket',
      p_prefix         =>  '', 
      p_s3_prefix      =>  '', 
      p_directory_name =>  'DATA_PUMP_DIR') 
   AS TASK_ID FROM DUAL;
```

2. db 디렉터리에 있는 DATA_PUMP_DIR 접두사의 모든 파일을 mys3bucket이라는 이름의 Amazon S3 버킷에 업로드  
(level 9 : 최고 수준의 GZIP 압축)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.upload_to_s3(
      p_bucket_name       =>  'mys3bucket', 
      p_prefix            =>  'db', 
      p_s3_prefix         =>  '', 
      p_directory_name    =>  'DATA_PUMP_DIR',
      p_compression_level =>  9) 
   AS TASK_ID FROM DUAL;
```
3. DATA_PUMP_DIR 디렉터리에 있는 모든 파일을 mys3bucket이라는 이름의 Amazon S3 버킷에 업로드  
파일은 dbfiles 폴더에 업로드됨 (level 1 : 가장 빠른 GZIP 압축)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.upload_to_s3(
      p_bucket_name       =>  'mys3bucket', 
      p_prefix            =>  '', 
      p_s3_prefix         =>  'dbfiles/', 
      p_directory_name    =>  'DATA_PUMP_DIR',
      p_compression_level =>  1) 
   AS TASK_ID FROM DUAL;        
```
4. DATA_PUMP_DIR 디렉터리에 있는 모든 파일을 mys3bucket이라는 이름의 Amazon S3 버킷에 업로드  
파일은 dbfiles 폴더에 업로드되고 각 파일 이름의 시작 부분에 ora가 추가됨 (압축 적용 X)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.upload_to_s3(
      p_bucket_name    =>  'mys3bucket', 
      p_prefix         =>  '', 
      p_s3_prefix      =>  'dbfiles/ora', 
      p_directory_name =>  'DATA_PUMP_DIR') 
   AS TASK_ID FROM DUAL;
```
5. 명령이 계정 A에서 실행되지만, 계정 B에서 버킷 콘텐츠를 완전히 제어해야 한다고 가정  
명령 rdsadmin_s3_tasks.upload_to_s3는 DATA_PUMP_DIR 디렉터리의 모든 파일을 s3bucketOwnedByAccountB라는 이름의 버킷으로 전송  
액세스 제어가 FULL_CONTROL로 설정되어 계정 B가 버킷의 파일에 액세스할 수 있음  
(level 6 : 속도 및 파일 크기가 균형을 이루는 GZIP 압축)
```sql
SELECT rdsadmin.rdsadmin_s3_tasks.upload_to_s3(
      p_bucket_name               =>  's3bucketOwnedByAccountB', 
      p_prefix                    =>  '', 
      p_s3_prefix                 =>  '', 
      p_directory_name            =>  'DATA_PUMP_DIR',
      p_bucket_owner_full_control =>  'FULL_CONTROL',
      p_compression_level         =>  6) 
   AS TASK_ID FROM DUAL;
```
6. 각 예에서, SELECT 문은 VARCHAR2 데이터 형식으로 작업 ID를 반환  
해당 작업 ID를 통해 작업의 출력 파일을 표시하여 결과를 볼 수 있음 (task-id를 절차에서 반환된 작업 ID로 대체)
```sql
SELECT text FROM table(rdsadmin.rds_file_util.read_text_file('BDUMP','dbtask-task-id.log'));
```
