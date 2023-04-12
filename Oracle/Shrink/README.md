### SHRINK 사용조건

#### 1. ORACLE 10g 이상 사용가능

#### 2. ASSM(Automatic Segment Space Management) 사용하는 테이블스페이스만 가능
```
1) 조회하는 방법

select tablespace_name, segment_space_management from user_tablespaces;

(segment_space_management = AUTO 일 경우 가능)
```
 
##### 3. row movement= enable 
```
1)조회하는 방법

select table_name, ROW_MOVEMENT from dba_tables where table_name ='[table명]';

2) ROW MOVEMENT 활성화/비활성화

ALTER TABLE [owner명].[table명] ENABLE ROW MOVEMENT; --활설화

ALTER TABLE [owner명].[table명] DISABLE ROW MOVEMENT; --비활성화
```
 
#### SHRINK 명령어
```
alter table [owner명].[table명] shrink space cascade;

cascade 옵션 : segment shrink는 dependent 한 오브젝트들에 대해서도 자동으로 수행
```
