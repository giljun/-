# SQLD_DML

- 자료들을 입력, 수정, 삭제, 조회하는 명령어
  - INSERT, UPDATE, DELETE, SELECT



## INSERT

```sql
INSERT INTO TABLE_NAME ( COLUMN LIST ) VALUES ( COLUMN LIST VALUE );
```

- 해당 칼럼과 입력값을 1:1 매핑하여 입력한다.
- 칼럼의 데이터가 문자 유형일 경우, '(single quotation)'로 입력할 값을 입력한다.
- 숫자일 경우, 붙이지 않는다.



## UPDATE

```sql
UPDATE PLAYER SET BACK_NO = 99;
```



## DELETE

```sql
DELETE FROM PLAYER;
```



## SELECT

- ALL

  - Default 옵션이므로 별도로 표시하지 않아도 된다.
  - 중복된 데이터가 있어도 모두 출력한다.

- DISTINCT

  - 중복된 데이터가 있는 경우, 1건으로 처리해서 출력한다.

    ```sql
    SELECT DISTINCT POSITION FROM PLAYER;
    ```

- WILDCARD(*) 사용하기

  - 모든 칼럼 정보를 조회할 경우 사용

- ALIAS 부여하기

  - 조회된 결과에 별명을 부여하여 칼럼 레이블을 변경할 수 있다.

  - 칼럼명 바로 뒤에 온다.

  - 칼럼명과 ALIAS 사이에 AS, as 키워드를 사용할 수 있다.

  - 이중 인용부호는 ALIAS가 공백, 특수문자를 포함할 경우와 대소문자 구분이 필요할 경우 사용된다.

    ```sql
    SELECT PLAYER_NAME AS 선수명, POSITION AS 위치, HEIGHT AS 키 FROM PLAYER;
    
    SELECT PLAYER_NAME 선수명, POSITION 위치, HEIGHT 키 FROM PLAYER;
    ```



## 산술 연산자와 합성 연산자

- 산술 연산자란
  - NUMBER와 DATE 자료형에 적용
  - 수학에서의 4칙 연산과 동일
  - 산술 연산자는 수학에서와 같이 (), *, /, +, -의 우선순위를 가진다.
- 합성 연산자 특징
  - 문자와 문자를 연결하는 경우 2개의 수빅 바(||)에 의해 이뤄진다.
  - 문자와 문자를 연결하는 경우 + 표시에 의해 이뤄진다.
  - 두 벤더 모두 공통적으로 CONCAT( string1, string2 ) 함수를 사용할 수 있다.
  - 칼럼과 문자 또는 다름 칼럼과 연결시킨다.
  - 문자 표현식의 결과에 의해 새로운 칼럼을 생성한다.