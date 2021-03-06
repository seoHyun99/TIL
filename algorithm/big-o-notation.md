# [Algorithm] Big O

## Big O 표기법이란?
: 가장 많이 쓰이는 표현법으로 알고리즘 실행 시간의 상한을 나타낸 표기법  
: 시간 복잡도를 표현하는 방법으로 Big O 표기법 외에 오메가 표기법, 세타 표기법이 존재  

### 1(상수)
- 입력되는 데이터 양과 상관없이 일정한 실행 시간을 가진다.

### logN
- 데이터 양이 많아져도, 시간이 조금씩 늘어난다.
- 시간에 비례하여, 탐색 가능한 데이터 양이 2의 n제곱이 된다.
- 계속 반씩 줄어드는 경우 : 처음에는 100개, 50개, 25개 ...  
 ex. Binary Search

### N
- 데이터 양에 따라 시간이 정비례한다.
- 예 : 선형 탐색, for 문을 통한 탐색

### N log N
- 데이터 양이 N배 많아지면, 실행 시간은 N배 보다 조금 더 많아진다. (정비례 x)

### N^2
- 데이터 양에 따라 걸리는 시간은 제곱에 비례한다.
- 예 : 2중 for 문을 사용한 버블 정렬, 선택 정렬

### 2^N
- 데이터가 하나 증가할 때마다 처리시간이 두 배씩 증가하는 경우를 표현한다.


### 사용하는 방법
1. 입력값이 무엇인지 확인한다.
2. 수행 연산 횟수를 N의 식으로 표현한다.
3. 가장 차수가 높은 항만 남기고 그 아래차수와 상수는 없앤다. : 최고차항을 제외한 상수의 속도는 측정값에 별다른 영향을 끼치지 못함.

### 알아두면 좋을 것
- Binary Search(이분 검색) : O(logN)
- Quick Sort : 빠른 정렬  
  - 평균 : O(N log N)
  - 최악 : O(N^2)  


- Bubble Sort / Insertion Sort : O(N^2) - 느린 정렬
