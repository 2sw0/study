ExplainPlan
===

### 실행계획 생성
```sql
EXPLAIN PLAN FOR
SELECT * FROM owner_name.table_name;
```

### 실행계획 확인
```sql
SELECT * FROM TABLE(dbms_xplan.display);
```
