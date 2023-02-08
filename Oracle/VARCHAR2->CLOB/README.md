varchar2 -> clob
---
'ORA-00910: 데이터형에 지정된 길이가 너무 깁니다.'


### 1.테이블 내에 데이터가 없을 경우
```sql
varchar2 -> long -> clob

ALTER TABLE (스키마.)테이블명 modify 타입변경_컬럼 long; --varchar2 -> long

ALTER TABLE (스키마.)테이블명 modify 타입변경_컬럼 clob; --long -> clob
```


### 2.테이블 내에 데이터가 있을 경우
```sql
ALTER TABLE (스키마.)테이블명 ADD 타입변경_컬럼_temp clob; --임시 컬럼 생성

UPDATE (스키마.)테이블명 SET 타입변경_컬럼_temp = 기존_컬럼; --데이터 복제

ALTER TABLE (스키마.)테이블명 drop column 기존_컬럼; -- 기존 컬럼 및 데이터 drop

ALTER TABLE (스키마.)테이블명 rename column 타입변경_컬럼_temp to 기존_컬럼; --기존 컬럼 명으로 대체
```


### 컬럼 위치까지 동일하게 (invisible/visible 이용)
```sql
ALTER TABLE (스키마.)테이블명 modify 기존_컬럼의_뒷컬럼1 INVISIBLE;

ALTER TABLE (스키마.)테이블명 modify 기존_컬럼의_뒷컬럼2 INVISIBLE;
….

ALTER TABLE (스키마.)테이블명 modify 기존_컬럼의_뒷컬럼1 VISIBLE;

ALTER TABLE (스키마.)테이블명 modify 기존_컬럼의_뒷컬럼2 VISIBLE;
```


### ALTER TABLE… INVISIBLE 쿼리 반복 작업
```sql
select 'ALTER TABLE ' \|\| table_name \|\| ' modify ' \|\| column_name \|\| ' INVISIBLE;' 

from all_tab_columns

where 1=1 and table_name = '테이블_이름'

and column_id >= 원래대로_되돌아갈_위치

and column_id < 제일 마지막 번호;
```


