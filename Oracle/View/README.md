뷰(view) 생성
---
```sql
CREATE OR REPLACE [FORCE|NOFORCE] VIEW 뷰_네임 [(column_aliases)]
AS 서브쿼리
[WITH CHECK OPTION [CONSTRAINT 원하는제약조건명]]
[WITH READ ONLY]
;

- OR REPLACE : 해당 구문을 사용하면 뷰를 수정할 때 DROP 없이 수정이 가능하다. 
- FORCE : 뷰를 생성할 때 쿼리문의 테이블, 컬럼, 함수 등이 존재하지 않아도 생성이 가능하다.
- NORORCE : 뷰를 생성할 때 쿼리문의 테이블, 컬럼 함수 등이 존재하지 않으면 생성되지 않는다.
- column_aliases : SELECT 컬럼의 별칭을 미리 정의할 수 있다.
- WITH READ ONLY : SELECT 만 가능하다. (INSERT, UPDATE, DELETE 불가능)
- WITH CHECK OPTION : WHERE 절의 조건에 해당하는 데이터만 저장, 변경이 가능하다.
- 함수를 사용한 컬럼은 반드시 ALIAS를 지정해야 한다.
- UNION, GROUP BY 등을 사용한 쿼리는 INSERT, UPDATE, DELETE를 사용할 수 없다.

-- 예시1 (SELECT만 가능)
CREATE OR REPLACE VIEW A.B 
AS
  SELECT * FROM　C UNION ALL
  SELECT * FROM　D UNION ALL
  SELECT * FROM　E
  WITH READ ONLY;

-- 예시2 (EMP.a가 10인 데이터만 조회 및 INSERT,UPDATE,DELETE가능)
CREATE OR REPLACE VIEW V_EMP 
AS
  SELECT * FROM EMP
  WHERE EMP.a = 10 
  WITH CHECK OPTION CONSTRAIN EMP_CK;
```

뷰(view) 수정
---
```sql
-- 생성과 동일
CREATE OR REPLACE VIEW [OWNER].[VIEW NAME] AS
SELECT 내용;
```
뷰(view) 삭제
---
```sql
DROP VIEW [OWNER].[VIEW NAME];
```
뷰(view) 조회
---
```sql
SELECT view_name, text FROM ALL_VIEWS; 
```
제약조건(constraint) 조회
---
```sql
select * from all_constraints;
```
