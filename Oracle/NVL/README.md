NVL(expr1, expr2)
---
```sql
expr1 - NULL인지 여부를 확인하는 값을 지정
expr2 - expr1 이 NULL이면 반환할 값을 지정 (expr1 과 동일한 데이터 유형을 지정)

expr1 이 NULL이 아닌 경우 expr1 을 반환
expr1 이 NULL이면 expr2 를 반환

ex)
사원표(emp)로부터 보합급(comm)을 취득. 보합급이 NULL인 경우는 0

SELECT NVL(comm, 0) FROM emp
```

NVL2(expr1, expr2, expr3)
---
```sql
expr1 - NULL인지 여부를 확인하는 값을 지정
expr2 - expr1 이 NULL이 아닌 경우 리턴할 값을 지정 (expr1 과 동일한 데이터 유형을 지정)
expr3 - expr1 이 NULL이면 반환할 값을 지정 (expr1 과 동일한 데이터 유형을 지정)

expr1 이 NULL이 아닌 경우 expr2 을 반환
expr1 이 NULL이면 expr3 를 반환

ex)
보합급(comm)이 NULL 이외일 때는 2배 값, NULL일 때는 0

SELECT NVL(comm, comm * 2, 0) FROM emp
```

