DESC INDEX 確認(SYS_NC00000$)
---
```sql
select index_name, c0lumn_expression, column_position from DBA_IND_EXPRESSIONS where index_name = 'index_name'; 
```
