ExplainPlan
===

### PLAN_TABLE_OUTPUT 생성
```sql
explain plan for
SELECT * FROM owner_name.table_name;
```

### 실행계획 확인
```sql
SELECT * FROM TABLE(dbms_xplan.display);
```
