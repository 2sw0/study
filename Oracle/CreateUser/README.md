CreateUser
===


### 전체 유저 확인
```sql
select * from all_users;
```

### 유저 생성
```sql
create user 유저명 identified by "암호";
```

### 유저 권한 부여
connect(접속 권한), resource(객체 및 데이터 조작 권한), dba
```sql
grant connect, resource, dba to 유저명;
```

### 유저 권한 취소
connect(접속 권한), resource(객체 및 데이터 조작 권한), dba
```sql
revoke 권한 from 유저명;
```


###  삭제
```sql
drop user 유저명 cascade;
```
