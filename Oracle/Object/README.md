Object 정보 확인
--

select distinct object_type from dba_objects;

OBJECT_TYPE
--

CLUSTER  
FUNCTION  
INDEX  
PACKAGE  
PACKAGE BODY  
PROCEDURE  
SEQUENCE  
SYNONYM  
TABLE  
TRIGGER  
VIEW  

example
--
```sql
select owner,object_name,object_type from dba_objects where object_type = 'TABLE' order by owner,object_name;
select owner,object_name,object_type from dba_objects where object_type = 'SEQUENCE' order by owner,object_name;
select owner,object_name,object_type from dba_objects where object_type = 'SYNONYM' order by owner,object_name;
select owner,object_name,object_type from dba_objects where object_type = 'PROCEDURE' order by owner,object_name;
select owner,object_name,object_type from dba_objects where object_type = 'PACKAGE' order by owner,object_name;
```
