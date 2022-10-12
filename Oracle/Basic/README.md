### 결과값 한줄로 출력
```sql
SELECT LISTAGG(COLUMN_NAME,', ') WITHIN GROUP(ORDER BY COLUMN_POSITION) AS result 
FROM all_ind_columns 
WHERE [where 조건] 
order by COLUMN_POSITION;
```

### 서버 정지/재가동
```sql
1. 리스너 종료
   $lsnrctl stop

2. sysdba 권한으로 접속
   $sqlplus "/as sysdba"

3. Oracle 종료
   SQL>shutdown
   SQL>shutdown abort
   SQL>shutdown immediate
   ※추천 방법 : shutdown immediate한후 종료가 안될시 새창을 띠워서 shutdown abort 시킴

4. 오라클 재가동
   SQL>startup

5. 리스너 시작
   $lsnrctl start

* 8i일경우
   $sqlplus /nolog
   SQL>connect / as sysdba
   SQL>shutdown immediate;
   SQL>startup
```
