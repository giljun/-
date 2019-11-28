# SQLD_그룹 함수

## 데이터 분석 개요

- 데이터 분석을 위해서 다음 세 가지 함수를 정의하고 있다.
  - AGGREGATE FUNCTION
    - COUNT, SUM, AVG, MAX, MIN
  - GROUP FUNCTION
    - ROLLUP
      -  GROUP BY의 확장된 형태로 사용하기가 쉬우며 병렬로 수행이 가능하기 때문에 매우 효과적일 뿐 아니라 시간 및 지역처럼 계층적 분류를 포함하고 있는 데이터의 집계에 적합하도록 되어 있다.
    - CUBE
      - 결합 가능한 모든 값에 대하여 다차원적인 집계를 생성하게 되므로 ROLLUP에 비해 다양한 데이터를 얻는 장점이 있는 반면에, 시스템에 부하를 많이 주는 단점이 있다.
    - GROUPING SETS
      - 원하는 부분의 소계만 손쉽게 추출할 수 있는 장점이 있다.
  - WINDOW FUNCTION



## ROLLUP 함수

- ROLLUP에 지정된 GROUPING  COLUMNS의 LIST는 SUBTOTAL을 생성하기 위해 사용되어지며, GROUPING COLUMNS의 수를 N이라고 했을 때, N+1 LEVEL의 SUBTOTAL이 생성된다.
- 인수는 계층 구조이므로 인수 순서가 바뀌면 수행 결과도 바뀌게 되므로 인수 순서에도 주의해야 한다.



## GROUPING 함수가 추가

- ROLLUP이나 CUBE에 의한 소계가 계산된 결과에는 GROUPING(EXPR) = 1이 표시되고, 그 외의 결과에는 GROUPING(EXPR) = 0이 표시된다.
- GROUPING 함수와 CASE/DECODE를 이용해, 소계를 나타내는 필드에 원하는 문자열을 지정할 수 있어서, 보고서 작성시 유용하게 사용할 수 있다.



## CUBE 함수

- ROLLUP에서는 단지 가능한 Subtotal만을 생성하였지만, CUBE는 결합 가능한 모든 값에 대하여 다차원 집계를 생성한다.
- CUBE를 사용할 경우에는 내부적으로는 GROUPING COLUMNS의 순서를 바꾸어서 또 한 번의 QUERY를 추가 수행해야 한다.
- 뿐만 아니라 GRAND TOTAL은 양쪽의 QUERY에서 모두 생성이 되므로 한 번의 QUERY에서는 제거되어야만 하므로 ROLLUP에 비해 시스템의 연산 대상이 많다.
  - 이처럼 GROUPING COLUMNS이 가질 수 있는 모든 경우에 대하여
    - SUBTOTAL을 생성해야 하는 경우에는 CUBE를 사용하는 것이 바람직하나,
    - ROLLUP에 비해 시스템에 많은 부담을 주므로 사용에 주의해야 한다.
    - CUBE 함수의 경우 표시된 인수들에 대한 계층별 집계를 구할 수 있으며,
    - 이 때, 표시된 인수들 간에는 계층 구조인 ROLLUP과는 달리 평등한 관계이므로 인수의 순서가 바뀌는 경우 행간에 정렬 순서는 바뀔 수 있어도 데이터 결과는 같다



## GROUPING SETS 함수

- GROUPING SETS를 이용해 더욱 다양한 소계 집합을 만들 수 있는데, GROUP BY SQL 문장을 여러 번 반복하지 않아도 원하는 결과를 쉽게 얻을 수 있게 되었다.
- GROUPING SET에 표시된 인수들에 대한 개별 집계를 구할 수 있으며, 이때 표시된 인수들 간에는 계층 구조인 ROLLUP과는 달리 평등한 관계이므로 인수의 순서가 바뀌어도 결과는 같다.
- 그리고 GROUPING SETS 함수도 결과에 대한 정렬이 필요한 경우는 ORDER BY 절에 명시적으로 정렬 칼럼이 표시가 되어야 한다.
- GROUPING  SETS 함수 사용 시, UNION ALL을 사용한 일반 그룹함수를 사용한 SQL과 같은 결과를 얻을 수 있다.
  - 괄호로 묶은 집합 별로 집계를 구할 수 있다.
  - GROUPING SETS의 경우 일반 그룹함수를 이용한 SQL과 결과 데이터는 같으나 행들의 정렬 순서는 다를 수 있다.

