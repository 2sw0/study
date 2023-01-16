뷰(view) 생성
---
```sql
CREATE OR REPLACE [FORCE|NOFORCE] VIEW 뷰_네임
AS 서브쿼리
[WITH CHECK OPTION [CONSTRAINT 원하는제약조건명]]
[WITH READ ONLY]
;

- FORCE : 기본 테이블 유무에 관계없이 VIEW를 생성
- WITH CHECK OPTION : VIEW에 의해 엑세스될 수 있는 행만이 입력되거나 변경될 수 있음을 지정
- WITH READ ONLY : SELECT만 가능한 VIEW 생성
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
