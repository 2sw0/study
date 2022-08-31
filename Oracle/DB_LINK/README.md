ORACLE DB LINK 조회
--
```sql
SELECT * FROM DBA_DB_LINKS; 
``` 

DBLINK 정상동작 확인
--
```sql
SELECT * FROM [원격지 테이블명]@[DBLINK명] where rownum < 10; --SQL문 실행시 데이터를 불러오는 것을 확인

--다른 DB의 테이블과 함께 JOIN 조회도 가능
SELECT A.*, B.*
FROM [테이블명1]@[DBLINK명1] A,
     [테이블명2]@[DBLINK명2] B
WHERE A.ID = B.ID
  AND A.NO = B.NO;
```

DBLINK 생성 권한 부여 및 확인
--
```sql
GRANT CREATE DATABASE LINK TO [사용자명]
SELECT * FROM DBA_SYS_PRIVS WHERE GRANTEE='사용자명';
--해당 명령은 SYS 계정으로 사용자한테 부여
```
 
DBLINK 생성/삭제 및 조회
--
```sql
CREATE DATABASE LINK [링크명] CONNECT TO [원격지 사용자명] IDENTIFIED BY "[원격지 사용자 비밀번호]" USING '[인스턴스명]';
SELECT * FROM DBA_DB_LINKS WHERE DB_LINK='[링크명]';

DROP DATABASE LINK [링크명]; --DBLINK를 잘못 만들었을 때 DROP DATABASE LINK [링크명] 실행
```

ORA-12154 오류 출력 해결 방법
--
1. DBLINK  재생성 
```sql
--인스턴스명 대신 원격지 IP 주소, 포트를 DBLINK 생성할 때 같이 넣고 생성하는 방법
CREATE DATABASE LINK [링크명] CONNECT TO [원격지 사용자명] IDENTIFIED BY "[원격지 사용자 비밀번호]"
USING '(DESCRIPTION =
               (ADDRESS_LIST =
                   (ADDRESS = (PROTOCOL = TCP)(HOST = [원격지 호스트 IP])(PORT = [원격지 호스트 PORT]))
                )
                (CONNECT_DATA =
                    (SERVER = DEDICATED)
                    (SERVICE_NAME=[인스턴스명])
                )
            )';
```

2. tnsnames.ora 수정
```sql
--로컬 서버의 tnsnames.ora에 원격지의 인스턴스가 등록이 안되어 있으므로 tnsnames.ora에 인스턴스를 등록
su
cd $TNS_ADMIN
vi tnsnames.ora

--tnsnames.ora는 관리자 계정으로만 수정 가능
--보통 환경변수에 $TNS_ADMIN 이 등록되어 있으므로 해당 경로 사용
```
```sql
--tnsnames.ora에 입력
[인스턴스명] =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = [원격지 호스트 IP])(PORT = [원격지 호스트 PORT]))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = [인스턴스명])
    )
  )
```
