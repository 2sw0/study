CreateUser
===

```sql
--전체 유저 확인
select * from all_users;
```

```sql
--유저 생성
create user 유저명 identified by "암호";
```

```sql
--유저 권한 부여
--connect(접속 권한), resource(객체 및 데이터 조작 권한), dba
grant connect, resource, dba to 유저명;
```

```sql
--유저 권한 취소
--connect(접속 권한), resource(객체 및 데이터 조작 권한), dba
revoke 권한 from 유저명;
```

```sql
--계정 삭제
drop user 유저명 cascade;
```
