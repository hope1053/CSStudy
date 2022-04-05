## 목적

- 대표적인 그래프 탐색 알고리즘
- 특정 노드를 찾아가는 탐색

## DFS (Depth First Search)

- 정점의 자식들부터 먼저 탐색하는 방법, 특정 노드에서 다음 분기(브랜치)로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법
- **스택 or 재귀함수**를 통해 구현함
- **모든 경로를 방문해야 할 경우**에 적합함

### 기본 원칙

- DFS에서 데이터를 찾을 때는 항상 **“앞으로 찾아가야할 노드"**와 **“이미 방문한 노드"**를 기준으로 데이터를 탐색함
- 특정 노드가 **“앞으로 찾아가야할 노드"**라면 계속 검색하는것이고 **“이미 방문한 노드"**라면 무시하거나 따로 저장하면 됨

### 구현

- Stack 사용하는 경우

```python
def dfs(graph, start_node):
    visited, need_visit = list(), list()
    need_visit.append(start_node)

    while need_visit:
        node = need_visit.pop()
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])

    # return visited
    print(visited)

dfs(graph, 'A')
```

```python
def dfs_recursive(graph, start, visited = []):
## 데이터를 추가하는 명령어 / 재귀가 이루어짐 
    visited.append(start)
 
    for node in graph[start]:
        if node not in visited:
            dfs_recursive(graph, node, visited)
    return visited
```

- visited 자료형을 기본 함수 인자로 포함시키고 방문한 리스트들을 재귀함수를 통해서 계속 visited에 담음

### 예시

- A에서 H까지 갈 수 있는 경로를 모두 구해라

```python
# 새로운 graph
graph = {'A':['B','C'],
         'B':['A','D','E'],
         'C':['A','F','G'],
         'D':['B'],
         'E':['B','H'],
         'F':['C','H'],
         'G':['C'],
         'H':['E','F']}
```

```python
paths = []

def dfs_paths(graph, start, end, visited=[]):
    # 그 전에 방문했던 노드들을 기록하고
    # 이번 차례 방문하는 노드를 새로 추가한다.
    visited = visited + [start]
    
    #도착할 경우, paths에 경로를 기록한다.
    if start == end:
        paths.append(visited)
    
    #현재 노드의 자손 노드들 중, 방문하지 않은 노드들에 대해 재귀 호출
    for node in graph[start]:
        if node not in visited:
            dfs_paths(graph, node, end, visited)
```

```python
dfs_paths(graph,'A','H')

# [['A', 'B', 'E', 'H'], ['A', 'C', 'F', 'H']]
```

### 시간 복잡도

while문이 시간 복잡도를 결정함

- 노드 수: V
- 간선 수: E
- V + E 만큼 while문을 반복하기 때문에
- O(V+E)

## BFS (Breadth First Search)

- 정점들과 같은 레벨에 있는 노드들을 먼저 탐색하는 방법, 인접한 노드를 먼저 탐색하는 방법
- 큐를 통해 구현함(해당 노드의 주변부터 탐색해야하기 때문에)
- **최소 비용**(모든 곳을 탐색하는 것보다 최소 비용이 우선일 때)에 적합

### 기본 원칙

- **“방문하고자 하는 노드"**와 **“방문했던 노드"**를 나누어서 알고리즘을 구성하는 것이 핵심원리
1. 시작 노드를 방문했던 노드에 삽입
2. 방문할 노드에 시작 노드의 Child Node를 삽입
3. Child 노드를 중심으로 다시 1~2단계를 거쳐 탐색

### 구현

```python
def bfs(graph, start_node):
    visited = list()
    need_visit = list()

    need_visit.append(start_node)

    while need_visit: #방문 필요한 노드가 없는 경우, 모두 visit 한 경우
        node = need_visit.pop(0) #index 번호를 써주면 자동으로 해당 index 값 pop하고 index도 채워줌
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node]) #리스트 뒤에 리스트를 붙일 수 있는 method

    return visited

bfs(graph, 'A')
```

- while문이 시간 복잡도를 결정함
    - 노드 수: V
    - 간선 수: E
    - V + E 만큼 while문을 반복하기 때문에
    - O(V+E)
- 아래와 같은 경우에 BFS로 효과적으로 풀 수 있다
    - 최소 비용 문제
    - 간선의 가중치가 1이다
    - 정점과 간선의 개수가 적다(시간 제약, 메모리 제한 내에 만족한다)

## BFS vs DFS

둘의 가장 큰 차이점은 While문 다음에 어떤 자료를 우선적으로 추출하냐

- DFS: 리스트의 가장 끝에 있는 데이터를 기준으로 추출
- BFS: 리스트의 가장 처음에 있는 인자