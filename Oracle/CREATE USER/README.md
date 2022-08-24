CREATE USER
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
grant connect, resource, dba to 유저명;
```
