### [mysqldump](./mysqldump/README.md)

### 시작, 정지, 재시작, 상태 확인
|분류|우분투|CentOS 6|CentOS 7|
|-|-|-|-|
|시작|`service mysql start`|`service mysqld start`|`systemctl start mysqld`|
|정지|`service mysql stop`|`service mysqld stop`|`systemctl stop mysqld`|
|재시작|`service mysql restart`|`service mysqld restart`|`systemctl restart mysqld`|
|상태 확인|`service mysql status`|`service mysqld status`|`systemctl status mysqld`|

<br>

### 스키마 이름 변경
InnoDB에서 잘 작동: 새로운 빈 데이터베이스를 만들고 새로운 데이터베이스로 각 테이블의 이름을 변경
```sql
RENAME TABLE old_db.table TO new_db.table;
```
그 후 권한 조정 필요

#### 셸에서 스크립팅하려면 다음 중 하나를 사용할 수 있음
```sql
mysql -u username -ppassword old_db -sNe 'show tables' | while read table; \ 
do mysql -u username -ppassword -sNe "rename table old_db.$table to new_db.$table"; done
```
또는
```sql
for table in `mysql -u root -ppassword -s -N -e "use old_db;show tables from old_db;"`; do mysql -u root -ppassword -s -N -e "use old_db;rename table old_db.$table to new_db.$table;"; done;
```
메모:  
* -p 옵션과 암호 사이에는 공백 X (데이터베이스에 암호가없는 경우 -u username -ppassword 부분을 제거)  
* 일부 테이블에 트리거가있는 경우 위의 방법로 이동 불가능 ( Trigger in wrong schema 오류로 트리거 발생)  
* 이 경우 기존 방법을 사용하여 데이터베이스를 복제 한 다음 이전 데이터베이스를 삭제  
```sql mysqldump old_db | mysql new_db```
* 만약 stored 프로시저가 있다면 다음처럼 복사 가능  
```sql mysqldump -R old_db | mysql new_db```

