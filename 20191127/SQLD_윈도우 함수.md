# SQLD_윈도우 함수

- 행과 행간의 관계를 쉽게 정의하기 위해 만든 함수
- 종류
  - 순위 관련 함수
    - RANK, DENSE_RANK, ROW_NUMBER
  - 집계 관련 함수
    - SUM, MAX, MIN, AVG, COUNT
  - 행 순서 관련 함수
    - FIRST_VALUE, LAST_VALUE, LAG, LEAD
  - 비율 관련 함수
    - CUME_DIST, PERCENT_RANK, NTILE, RATIO_TO_REPORT



## 그룹 내 순위 함수

### RANK 함수

- 특정 항목 / 특정 범위 / 전체 데이터에 대한 순위를 구하는 함수



### DENSE_RANK 함수

- RANK 함수와 흡사하나, 동일한 순위를  하나의 건수로 취급하는 것이 틀린 점



### ROW_NUMBER 함수

- RANK나 DENSE_RANK 함수가 동일한 값에 대해서는 동일한 순위를 부여하는데 반해, 동일한 값이라도 고유한 순위를 부여



## 일반 집계 함수

### SUM 함수

- 파티션별 윈도우의 합

- RANGE UNBOUNDED PRECEDING
  - 현재 행을 기준으로 파티션 내의 첫 번째 행까지의 범위를 지정



### MAX 함수

- 파티션별 윈도우의 최대값



### MIN 함수

- 파티션별 윈도우의 최소값



### AVG 함수

- EMP 테이블에서 같은 매니저를 두고 있는 사원들의 평균 SALARY를 구하는데, 조건은 같은 매니저 내에서 자기 바로 앞의 사번과 바로 뒤의 사번인 직원만을 대상으로 한다.
- ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
  - 현재 행을 기준으로 파티션 내에서 앞의 한 건, 현재 행, 뒤의 한 건을 범위로 지정한다.



### COUNT 함수

- RANGE BETWEEN 50 PRECEDING AND 150 FOLLOWING
  - 현재 행의 급여 값을 기준으로 급여가 -50에서 +150의 범위 내에 포함된 모든 행이 대상이 된다.



## 그룹 내 행 순서 함수_SQL_SERVER 지원 X

### FIRST_VALUE 함수

- SQL SERVER에서 지원 X
- 파티션별로 윈도우에서 가장 먼저 나온 값을 구한다.



### LAST_VALUE 함수

- SQL SERVER에서 지원 X
- 파티션별로 윈도우에서 가장 나중에 나온 값을 구한다.
- ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING
  - 현재 행을 포함해서 파티션 내의 마지막 행까지의 범위를 지정한다.
- 공동 등수를 인정하지 않고 가장 나중에 나온 행만을 처리



### LAG 함수

- 파티션별 윈도우에서 이전 몇 번째 행의 값을 가져올 수 있다.
- 인자
  - 두 번째 인자는 몇 번째 앞의 행을 가져올지 결정
  - 세 번째 인자, NULL 값을 다른 값으로 바꾸어 줄 수 있다.



### LEAD 함수

- 파티션별 윈도우에서 이후 몇 번째 행의 값을 가져올 수 있다.



## 그룹 내 비율 함수_SQL_SERVER에서 지원 X

### RATIO_TO_REPORT 함수

- 파티션 내 전체 SUM값에 대한 행별 칼럼 값의 백분율을 소수점으로 구할 수 있다.



### PERCENT_RANK 함수

- 파티션별 윈도우에서 제일 먼저 나오는 것을 0으로, 제일 늦게 나오는 것을 1로 하여, 값이 아닌 행의 순서별 백분율을 구한다.



### CUME_DIST 함수

- 파티션별 윈도우의 전체건수에서 현재 행보다 작거나 같은 건수에 대한 누적백분율



### NTILE 함수

- 파티션별 전체 건수를 ARGUMENT 값으로 N 등분한 결과









