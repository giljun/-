# SQLD_표준 조인

## 표준 SQL의 기능

- STANDARD JOIN 기능 추가 ( CROSS, OUTER JOIN 등 새로운 FROM 절 JOIN 기능들 )
- SCALAR SUBQUERY, TOP-N QUERY  등의 새로운 SUBQUERY 기능들
- ROLLUP, CUBE, GROUPING SETS 등의 새로운 리포팅 기능
- WINDOW FUNCTION 같은 새로운 개념의 분석 기능들



### 일반 집합 연산자

- UNION 연산은 UNION 기능으로
- INTERSECTION 연산은 INTERSECT 기능으로
- DIFFERENCE 연산은 EXCEPT( Oracle은 MINUS ) 기능으로
- PRODUCT 연산은 CROSS JOIN 기능으로



### 순수 관계 연산자

- SELECT 연산은 WHERE 절로 구현
- PROJECT 연산은 SELECT 절로 구현
- ( NATURAL ) JOIN 연산은 다양한 JOIN 기능으로 구현
- DIVIDE 연산은 현재 사용되지 않는다.



## FROM 절 JOIN 형태

- INNER JOIN
  - 기존의 WHERE 절의 검색 조건과 JOIN 조건을 그대로 사용할 수 있으며
  - 추가된 선택 기능으로 JOIN 조건을 FROM 절에서 명시적으로 정의할 수 있게 되었다.
- NATURAL JOIN
  - INNER JOIN의 하위 개념으로
  - 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 EQUI JOIN을 수행
  - USING 조건절
  - ON 조건절
  - CROSS JOIN
  - OUTER JOIN



## INNER JOIN

- JOIN 조건에서 동일한 값이 있는 행만 반환
- FROM 절에서 정의
- USING, ON 조건절을 필수적으로 사용해야 한다.



## NATURAL JOIN

- 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 대해 EQUI(=) JOIN을 수행
- NATURAL JOIN이 명시되면 WHERE 절에서 JOIN 조건을 정의할 수 없다. ( USING, ON 조건절 )
- SQL Server에서는 지원하지 않는다.
- 기타 설명
  - JOIN 컬럼을 지정하지 않았지만 공통된 칼럼으로 JOIN 처리 함.
  - JOIN에 사용된 칼럼은 같은 데이터 유형이어야한다.
  - ALIAS나 테이블명과 같은 접두사를 붙일 수 없다.
- NATURAL JOIN과 INNER JOIN의 차이
  - NATURAL JOIN은 JOIN에 사용된 같은 이름의 칼럼을 하나로 처리하지만
  - INNER JOIN은 모두 표시한다.



## USING 조건절

- FROM 절에 USING 조건절을 이용하여 같은 이름을 가진 칼럼 중에 원하는 칼럼에 대해서만 EQUI JOIN을 할 수 있다.
  - NATURAL JOIN에서는 모든 일치되는 칼럼을 조인하지만 USING은 원하는 칼럼만 JOIN한다
- SQL SERVER에서는 지원하지 않는다.
- JOIN 칼럼에 대해서 ALIAS나 테이블 이름과 같은 접두사를 붙일 수 없다.



## ON 조건절

- ON 조건절을 사용하면 칼럼명이 다르더라도 JOIN 조건을 사용할 수 있다.

- 임의의 JOIN 조건을 지정할 수 있다.

- 이름이 다른 칼럼명을 JOIN 조건으로 사용할 수 있다.

- JOIN 칼럼명을 명시할 수 있다.

- ALIAS나 테이블 명과 같은 접두사를 사용할 수 있다.

- WHERE 절과의 혼용

- ON 조건절 + 데이터 검증 조건 추가

  - ON 조건절에 데이터 검색 조건을 추가할 수 있다.
  - 검색 조건 목적인 경우는 WHERE절을 사용할 것을 권고

- 다중 테이블 JOIN

  ```sql
  SELECT E.EMPNO, D.DEPTNO
  FROM EMP E, DEPT D, DEPT_TEMP T
  WHERE E.DEPTNO = D.DEPTNO
  AND E.DEPTNO = T.DEPTNO
  ```



## OUTER JOIN

- JOIN 조건에서 동일한 값이 없는 행도 반환할 때 사용

- OUTER JOIN

- LEFT OUTER JOIN

  - 조인 수행시 좌측 테이블에서 데이터를 먼저 읽은 후, 우측 테이블에서 JOIN 대상을 읽어온다.

- RIGHT OUTER JOIN

  - LEFT OUTER JOIN과 반대로

- FULL OUTER JOIN

  - LEFT OUTER JOIN과 RIGHT OUTER JOIN의 결과를 합집합으로 처리한 결과와 동일하다.

    ```sql
    SELECT L.DEPTNO, L.DNAME, L.LOC, R.DEPTNO, R.DNAME, R.LOC
    FROM DEPT L LEFT OUTER JOIN DEPT_TEMP R
    ON L.DEPTNO = R.DEPTNO
    UNION
    SELECT L.DEPTNO, L.DNAME, L.LOC, R.DEPTNO, R.DNAME, R.LOC
    FROM DEPT L RIGHT OUTER JOIN DEPT_TEMP R
    ON L.DEPTNO = R.DEPTNO
    ```



## INNER VS OUTER VS CROSS JOIN 비교





