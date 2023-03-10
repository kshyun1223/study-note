# 알고리즘
## 탐욕법 (Greedy Algorithm)
### 개요
- 현재 상황에서 지금 당장 좋은 것만 고르는 방법

### 활용
- 단순히 가장 좋아보이는 것을 반복적으로 선택해도 최적의 해를 구할 수 있는지 검토하는 정당성 분석이 중요하다
- 일반적인 상황에서는 최적해를 보장할 수 없는 경우가 많다
- 코딩테스트에서는 탐욕법으로 얻은 해가 최적해인 상황에서 이를 추론할 수 있어야 풀리도록 출제된다

## 구현 (Implementation)
### 개요
- 머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정을 의미한다
- 코딩테스트에서는 풀이를 떠올리는 것은 쉽지만 코드로 옮기기 어려운 문제를 지칭한다

### 예시
- 좌표 문제
  - 요구사항대로 충실히 구현하기만 하면 된다
  - 시뮬레이션 유형으로 분류된다
- 시간 계산 문제
  - 가능한 모든 시간의 경우를 초 단위로 전부 세서 푸는 문제 
  - 완전탐색 유형으로 분류된다

## 깊이 우선 탐색 (DFS, Depth-First Search)
### 개요
- 그래프에서 깊은 부분을 우선적으로 탐색하는 방법
- 스택 자료구조를 이용한다

### 상세
1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다
2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다
3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다

## 너비 우선 탐색 (BFS, Breadth-First Search)
### 개요
- 그래프에서 가까운 노드부터 우선적으로 탐색하는 방법
- 큐 자료구조를 이용한다

### 상세
1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다
2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리한다
3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다

## 정렬 (Sort)
### 선택정렬(Selection Sort)
- 처리되지 않은 데이터 중에서 가장 작은 데이터를 선택해서 맨 앞의 데이터와 바꾸는 것을 반복한다

### 삽입정렬 (Insertion Sort)
- 처리되지 않는 데이터를 하나씩 골라서 적절한 위치에 삽입한다
- 일반적으로 선택정렬에 비해 구현 난이도가 높지만 더 효율적이다

### 계수정렬 (Counting Sort)
- 각각의 데이터가 몇 번 나왔는지 세는 방식으로 동작한다
- 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때 사용 가능하다
- 특정한 조건에 부합할 때만 사용할 수 있지만 동작이 매우 빠르다

## 탐색 (Search)
### 순차탐색 (Sequential Search)
- 리스트 안에 있는 특정한 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 확인하는 방법

### 이진탐색 (Binary Search)
- 정렬되어 있는 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 방법
- 시작점, 끝점, 중간점을 이용하여 탐색 범위를 설정한다

## 동적 계획법 (Dynamic Programming)
### 개요
- 메모리를 적절히 사용하여 수행시간 효율성을 비약적으로 향상시키는 방법
- 이미 계산된 결과는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 한다
- Top-down(하향식) 방식과 Bottom-up(상향식) 방식이 있다

### 사용 조건
- 최적 부분 구조 (Optimal Substructure)
  - 큰 문제를 작은 문제로 나눌 수 있으며, 작은 문제의 답을 모아서 큰 문제를 해결할 수 있다
- 중복되는 부분 문제 (Overlapping Subproblem)
  - 동일한 작은 문제를 반복적으로 해결해야 한다

### 메모이제이션 (Memorization)
- 한번 계산한 결과를 메모리 공간에 메모하는 기법
- 같은 문제를 다시 호출하면 메모했던 결과를 그대로 가져온다
- 값을 기록해 놓는다는 점에서 캐싱(Caching)이라고도 한다
- 다이나믹 프로그래밍에만 국한된 개념은 아니다

### 분할 정복(Divide and Conquer)과의 비교
- 공통점
  - 다이나믹 프로그래밍과 분할 정복은 모두 최적 부분 구조를 가질 때 사용할 수 있다
- 차이점
  - 다이나믹 프로그래밍은 각 부분 문제들이 서로 영향을 미치며 부분 문제가 중복된다
  - 분할 정복은 동일한 부분 문제가 반복적으로 계산되지 않는다

### 활용
- 해당 문제가 다이나믹 프로그래밍 유형인지 파악하는 것이 중요하다
- 그리디, 구현, 완전 탐색 등 다른 알고리즘이 적용될 수 있는지 검토해보고, 그렇지 않을 경우 다이나믹 프로그래밍을 고려한다
- 먼저 비효율적인 완전 탐색 코드를 작성한 뒤에 작은 문제에서 구한 답이 큰 문제에서 그대로 사용될 수 있는 것이 확인되면 코드를 개선해나간다

## 다익스트라 알고리즘 (Dijkstra Algorithm)
### 개요
- 특정 노드에서 다른 모든 노드로 가는 최단 경로를 계산한다
- 음의 간선이 없을 때만 사용할 수 있다
- 매 상황에서 가장 비용이 적은 노드를 선택해 임의의 과정을 반복한다
- 그리디 알고리즘의 일종으로 분류된다

### 상세
1. 출발 노드를 설정한다
2. 최단 거리 테이블을 초기화 한다
3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택한다
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다
5. 3~4의 과정을 반복해서 수행한다

## 플로이드 워셜 알고리즘 (Floyd-Warshall Algorithm)
### 개요
- 모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산한다
- 다익스트라 알고리즘과 달리 방문하지 않은 노드 중에 최단 거리를 갖는 노드를 찾는 과정이 필요하지 않다
- 2차원 테이블에 최단 거리 정보를 저장한다
- 다이나믹 프로그래밍의 일종으로 분류된다

### 상세
- 각 단계마다 특정한 노드 k를 거쳐 가는 경우를 확인한다
- a에서 b로 가는 최단 거리보다 a에서 k를 거쳐 b로 가는 거리가 더 짧은지 검사한다

## 크루스칼 알고리즘 (Kruskal Algorithm)
### 개요
- 크루스칼 알고리즘은 대표적인 최소 신장 트리(Minimum Spanning Tree) 알고리즘이다
- 그리디 알고리즘의 일종으로 분류된다
- 신장트리는 그래프에서 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프를 의미한다
- 최소한의 비용으로 구성되는 신장 트리를 최소 신장 트리라고 한다

### 상세
1. 간선 데이터를 비용에 따라 오름차순으로 정렬한다
2. 간선을 하나씩 확인하며 현재의 간선이 사이클을 발생시키는지 확인한다
3. 사이클이 발생하지 않는 경우 최소 신장 트리에 포함시킨다
4. 사이클이 발생하는 경우 최소 신장 트리에 포함시키지 않는다
5. 모든 간선에 대하여 2~4의 과정을 반복한다

## 위상 정렬 (Topological sort)
### 개요
- 사이클이 없는 방향 그래프의 모든 노드를 방향성에 거스르지 않도록 순서대로 나열하는 것을 의미한다
- 진입차수(Indegree)는 특정한 노드로 들어오는 간선의 개수를 의미한다
- 진출차수(Outdegree)는 특정한 노드에서 나가는 간선의 개수를 의미한다

### 큐를 이용하는 경우
1. 진입차수가 0인 모든 노드를 큐에 넣는다
2. 큐에서 원소를 꺼내 해당 노드에서 나가는 간선을 그래프에서 제거한다
3. 새롭게 진입차수가 0이 된 노드를 큐에 넣는다
4. 큐가 빌 때까지 2~3의 과정을 반복한다

### 특징
- DAG(Direct Acyclic Graph, 순환하지 않는 방향 그래프)에만 사용할 수 있다
- 한 단계에서 큐에 새롭게 들어가는 원소가 2개 이상인 경우가 있다면 여러 가지 답이 존재하게 된다
- 모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재한다고 판단하여, 사이클에 포함된 원소 중에서 어떠한 원소도 큐에 들어가지 못한다