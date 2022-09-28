### 결과값 한줄로 출력
```sql
SELECT LISTAGG(COLUMN_NAME,', ') WITHIN GROUP(ORDER BY COLUMN_POSITION) AS result 
FROM all_ind_columns 
WHERE [where 조건] 
order by COLUMN_POSITION;
```
