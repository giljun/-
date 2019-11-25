# SQLD_DDL

## 데이터 유형

- 숫자타입
- 문자열 유형
  - VARCHAR와 CHAR의 차이
    - 고정길이와 가변길이
    - 문자열 비교할 때, CHAR는 공백을 채워서 비교
    - 문자열 비교할 때, VARCHAR는 공백도 하나의 문자로 취급



## CREATE TABLE

- 테이블과 칼럼 정의

  - 후보키 중에 하나를 선정하여 기본키 칼럼으로 지정

- CREATE TABLE

  - 주의사항
    - 테이블명
      - 객체를 의미할 수 있는 적절한 이름을 사용
    - 벤더에서 사전에 정의한 예약어는 쓸 수 없다.
  - 추가적으로 주의 사항
    - 테이블 생성시 대/소문자 구분은 하지 않는다. 기본적으로 대문자
    - DATETIME 데이터 유형에는 별도로 크기를 지정하지 않는다.
    - 문자 데이터 유형은 반드시 가질 수 있는 최대 길이를 표시해야 한다.
    - 칼럼과 칼럼의 구분은 콤마로 하되, 마지막 칼럼은 콤마를 찍지 않는다.
    - 칼럼에 대한 제약조건이 있으면 CONSTRAINT를 이용하여 추가

- 제약조건

  - 데이터의 무결성을 유지하기 위한 데이터베이스의 보편적인 방법
  - 종류
    - NULL 의미
      - 조건에 맞는 데이터가 없을 때의 공집합과도 다르다.
      - 아직 정의되지 않은 미지의 값이거나 현재 데이터를 입력하지 못하는 경우를 의미
    - DEFAULT 의미
      - 데이터 입력 시에 칼럼의 값이 지정되어 있지 않을 경우 기본값

- 생성된 테이블 구조 확인

  ```sql
  /*
  	Oracle
  */
  DESCRIBE PLAYER;
  
  /*
  	SQL Server
  */
  exec sp_help 'dbo.PLAYER' go
  ```

- SELECT 문장을 통한 테이블 생성 사례

  - SELECT 문장을 활용해서 테이블을 생성할 수 있는 방법

  - CTAS 기법 사용시 주의할 점

    - NOT NULL만 새로운 복제 테이블에 적용이 되고,
    - 기본키, 고유키, 외래키, CHECK 등의 다른 제약 조건은 없어진다는 점
    - 제약 조건을 추가하기 위해서는 ALTER TABLE 기능을 사용해야 한다.

    ```sql
    CREATE TABLE TEAM_TEMP AS SELECT * FROM TEAM;
    
    SELECT * INTO TEAM_TEMP FROM TEAM;
    ```



## ALTER TABLE

- ADD COLUMN

  - 칼럼을 추가
  - 칼럼의 위치를 지정할 수는 없다

  ```sql
  ALTER TABLE PLAYER ADD (ADDRESS VARCHAR2(80));
  
  ALTER TABLE PLAYER ADD ADDRESS VARCHAR(80);
  ```

- DROP COLUMN

  - 칼럼을 삭제

    ```sql
    ALTER TABLE PLAYER DROP COLUMN ADDRESS;
    
    ALTER TABLE PLAYER DROP COLUMN ADDRESS;
    ```

- MODIFY COLUMN

  - 명령을 이용해 칼럼의 데이터 유형, 디폴트 값, NOT NULL 제약조건에 대한 변경을 포함
  - 몇 가지 사항을 고려해서 변경
    - 칼럼의 크기를 늘릴 수는 있지만,  줄이지는 못한다.
    - NULL 값만 가지고 있거나 테이블에 아무 행도 없으면 칼럼의 폭을 줄일 수 있다.
    - NULL 값만을 가지고 있으면 데이터 유형을 변경할 수 있다.
    - DEFAULT 값을 바꾸면 변경 작업 이후 발생하는 행 삽입에만 영향을 미치게 된다.
    - NULL 값이 없을 경우에만 NOT NULL 제약조건을 추가할 수 있다.

- RENAME COLUMN

  - 칼럼명이 변경되면, 해당 칼럼과 관계된 제약조건에 대해서도 자동으로 변경되는 장점

  - 일부 DBMS에서만 지원하는 기능

    ```sql
    ALTER TABLE PLAYER RENAME COLUMN PLAYER_ID TO TEMP_ID;
    
    sp_rename 'dbo.TEAM_TEMP.TEAM_ID', 'TEAM_TEMP_ID', 'COLUMN';
    /*
    	엔터티 이름 부분을 변경하면 스크립트 및 저장 프로시저를 손상시킬 수 있다.
    */
    ```

- DROP CONSTRAINT

  ```sql
  ALTER TABLE PLAYER DROP CONSTRAINT PLAYER_FK;
  ```

- ADD CONSTRAINT

  ```sql
  ALTER TABLE PLAYER ADD CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID);
  ```

  - 참조 제약조건을 추가하면, 참조 무결성 옵션에 따라서 만약 TEAM 테이블이나 TEAM 테이블의 데이터를 삭제하려 할 경우 외부에서 참조되고 있기 때문에 삭제가 불가능하게 제약을 할 수 있다.
  - 즉, 외부키를 설정함으로써 실수에 의한 테이블 삭제나 필요한 데이터의 의도하지 않은 삭제와 같은 불상사를 방지하는 효과를 볼 수 있다.



## RENAME TABLE

```sql
RENAME TEAM TO TEAM_BACKUP; 테이블 이름이 변경되었다.

sp_rename 'dbo.TEAM', 'TEAM_BACKUP'
```



## DROP TABLE

```sql
DROP TABLE PLAYER;
```

- CASCADE CONSTRAINT 옵션은 해당 테이블과 관계가 있었던 참조되는 제약조건에 대해서도 삭제한다는 것을 의미한다.
- SQL Server에서는 CASCADE 옵션이 존재하지 않으며 테이블을 삭제하기 전에 참조하는 FOREIGN KEY 제약 조건 또는 참조하는 테이블을 먼저 삭제해야 한다.



## TRUNCATE TABLE

```sql
TRUNCATE TABLE TEAM;
```

- 해당 테이블에 들어있던 모든 행들이 제거되고
- 저장 공간을 재사용 가능하도록 해제한다.

- 내부 처리 방식이나 Auto Commit 특성 등으로 인해 DDL로 분류
- 전체 데이터를 삭제하는 경우, DELETE보단 TRUNCATE가 시스템 부하가 적다.
- 복구가 불가능하므로 주의



