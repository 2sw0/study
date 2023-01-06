DESC INDEX 確認
---
```sql
select index_name, column_expression, column_position from DBA_IND_EXPRESSIONS where index_name = 'index_name'; 
```
