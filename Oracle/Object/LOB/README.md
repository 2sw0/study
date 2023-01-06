테이블스페이스에 엮인 segment 찾기
---
```sql
-- segment_type에 테이블이나 인덱스 없으면 다른 테이블쪽에서 LOB 가지고 있다는 
SELECT  A.TABLESPACE_NAME
      , A.SEGMENT_NAME
      , A.SEGMENT_TYPE      
      , ROUND(SUM(A.BYTES)/1024/1024) "SIZE_MB"      
  FROM DBA_SEGMENTS A
     , DBA_TABLES B
 WHERE A.SEGMENT_NAME = B.TABLE_NAME
   AND A.SEGMENT_TYPE IN ('TABLE','TABLE PARTITION')
 	 and a.tablespace_name in ('A')
--     AND A.OWNER = '유저아이디'
 GROUP BY A.TABLESPACE_NAME
        , A.SEGMENT_NAME
        , A.SEGMENT_TYPE
UNION ALL

-- INDEX SIZE
SELECT  A.TABLESPACE_NAME
      , A.SEGMENT_NAME
      , A.SEGMENT_TYPE
      , ROUND(SUM(A.BYTES)/1024/1024) "SIZE_MB"
  FROM DBA_SEGMENTS A
     , DBA_INDEXES B
 WHERE A.SEGMENT_NAME = B.INDEX_NAME   
   AND A.SEGMENT_TYPE IN ('INDEX','INDEX PARTITION') 
	 and a.tablespace_name in ('A')                 
--     AND A.OWNER = '유저아이디'
 GROUP BY A.TABLESPACE_NAME
        , A.SEGMENT_NAME
        , A.SEGMENT_TYPE
-- ORDER BY 2 DESC;
UNION ALL 
-- LOB  
SELECT  A.TABLESPACE_NAME
      , A.SEGMENT_NAME
      , A.SEGMENT_TYPE
      , ROUND(SUM(A.BYTES)/1024/1024) "SIZE_MB"
   FROM DBA_SEGMENTS A
      , DBA_LOBS B
  WHERE A.segment_name = B.segment_name  
    AND A.SEGMENT_TYPE LIKE 'LOB%'      
	and a.tablespace_name in ('A')
 GROUP BY A.TABLESPACE_NAME
        , A.SEGMENT_NAME
        , A.SEGMENT_TYPE        

 ORDER BY SEGMENT_TYPE,TABLESPACE_NAME DESC   
-- )
--  GROUP BY TABLESPACE_NAME 
;
```

LOB 세그먼트로 테이블 이름 찾기
---
```sql
select owner,segment_name,tablespace_name,table_name,column_name from dba_lobs
where segment_name in ('SYS_LOB0000000000A00000$$','SYS_LOB0000000000B00000$$');
```

해당 테이블스페이스로 테이블 이름 찾기
---
```sql
select owner,segment_name,tablespace_name,table_name,column_name from dba_lobs
where tablespace_name in ('A','B');
```

LOB 이동
---
```sql
SELECT
        'ALTER TABLE '||L.OWNER||'.'||L.TABLE_NAME||' MOVE LOB('||L.COLUMN_NAME||') STORE AS (TABLESPACE '||T.TABLESPACE_NAME||');' AS QUERY
FROM DBA_LOBS L, DBA_TABLES T
WHERE
        L.OWNER = T.OWNER AND L.TABLE_NAME = T.TABLE_NAME AND L.TABLESPACE_NAME <> T.TABLESPACE_NAME AND L.TABLESPACE_NAME = 'tablespace_name';

```



