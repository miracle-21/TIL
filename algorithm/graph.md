- [그래프 탐색 알고리즘](#그래프-탐색-알고리즘)
- [DFS(Depth-First Search): 깊이 우선 탐색](#dfsdepth-first-search-깊이-우선-탐색)
- [BFS(Breadth-First Search): 너비 우선 탐색](#bfsbreadth-first-search-너비-우선-탐색)
- [문제1: 타켓넘버](#문제1-타켓넘버)
- [문제2: 게임 맵 최단거리](#문제2-게임-맵-최단거리)

#


**⭐⭐⭐⭐ deque** </br>
**⭐⭐⭐ 스택/큐**

#


# **그래프 탐색 알고리즘**

- 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한번씩 방문한다.
- 대표적인 그래프 탐색 알고리즘으로는 DFS와 BFS가 있다.
- **DFS/BFS는 코딩 테스트에서 매우 자주 등장하는 유형**

# DFS(Depth-First Search): 깊**이 우선 탐색**

- 그래프에서 **깊은 부분을 우선적으로 탐색하는 알고리즘**이다.
- **스택** 자료구조(혹은 재귀 함수)를 이용한다.
- 동작 과정
    1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
    2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
    3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복한다.
![](https://velog.velcdn.com/images/miracle-21/post/7ac96789-1d49-408e-b1b0-e59782cc98b1/image.png)


```python
# DFS 함수 정의
def dfs(graph, v, visited):
    # 현재 노드를 방문 처리
    visited[v] = True
    print(v, end=' ')
    # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

# 각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트)
graph = [
  [],
  [2, 3, 8],
  [1, 7],
  [1, 4, 5],
  [3, 5],
  [3, 4],
  [7],
  [2, 6, 8],
  [1, 7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트)
visited = [False] * 9

# 정의된 DFS 함수 호출
dfs(graph, 1, visited)
>>> 1 2 7 6 8 3 4 5
```

# BFS(Breadth-First Search): **너비 우선 탐색**

- 그래프에서 **가까운 노드부터 우선적으로 탐색하는 알고리즘**이다.
- **큐 자료구조**를 이용한다.
    1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
    2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리한다.
    3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복한다.

![](https://velog.velcdn.com/images/miracle-21/post/879a3313-d967-4ae9-bb35-7cced4182557/image.png)

```python
from collections import deque

# BFS 함수 정의
def bfs(graph, start, visited):
    # 큐(Queue) 구현을 위해 deque 라이브러리 사용
    queue = deque([start])
    # 현재 노드를 방문 처리
    visited[start] = True
    # 큐가 빌 때까지 반복
    while queue:
        # 큐에서 하나의 원소를 뽑아 출력
        v = queue.popleft()
        print(v, end=' ')
        # 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True

# 각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트)
graph = [
  [],
  [2, 3, 8],
  [1, 7],
  [1, 4, 5],
  [3, 5],
  [3, 4],
  [7],
  [2, 6, 8],
  [1, 7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트)
visited = [False] * 9

# 정의된 BFS 함수 호출
bfs(graph, 1, visited)
>>> 1 2 3 8 7 4 5 6
```

# 문제1: 타켓넘버

![](https://velog.velcdn.com/images/miracle-21/post/520454a2-2ef8-477e-9d37-c5dbe3732e12/image.png)
```python
# BFS 풀이
from collections import deque
def solution(numbers, target):
    answer = 0
    queue = deque()
    n = len(numbers)
    queue.append([numbers[0],0])
    queue.append([-1*numbers[0],0])
    while queue:
        temp, idx = queue.popleft()
        idx += 1
        if idx < n:
            queue.append([temp+numbers[idx], idx])
            queue.append([temp-numbers[idx], idx])
        else:
            if temp == target:
                answer += 1
    return answer
```

**deque를 사용한 문제.**

# 문제2: 게임 맵 최단거리
![](https://velog.velcdn.com/images/miracle-21/post/d5514d2d-a84b-475c-817a-449e4d166de4/image.png)


```python
# 다른사람의 코드 참고
from collections import deque

def solution(maps):
    n = len(maps)
    m = len(maps[0])
    directions = [(1,0),(-1,0),(0,1),(0,-1)]
    q = deque([(0,0)])
    while q:
        x,y = q.popleft()
        for i in range(len(directions)):
            nx = x + directions[i][0]
            my = y + directions[i][1]
            if 0 <= nx < n and 0 <= my < m and maps[nx][my] == 1:
                maps[nx][my] = maps[x][y]+1
                q.append((nx,my))
    return maps[-1][-1] if maps[-1][-1] > 1 else -1
```

1. 맵 크기
    
    ```python
        n = len(maps) #행
        m = len(maps[0]) #열
    ```
    
2. 이동 방향
    
    ```python
    directions = [(1,0),(-1,0),(0,1),(0,-1)] #아래, 위, 오른쪽, 왼쪽
    ```
    
3. 시작 위치
    
    ```python
    q = deque([(0,0)])
    ```
    
4. 이동 가능 조건(맵 크기를 넘지 않아야 한다, 가보지 않은 곳이어야 한다)
    
    ```python
    x,y = q.popleft()
    for i in range(len(directions)):
        nx = x + directions[i][0] # 상,하
        my = y + directions[i][1] # 좌,우
    		# 상,하로 이동했을 때 맵 크기를 넘지 않아야 한다
    		# 좌,우로 이동했을 때 맵 크기를 넘지 않아야 한다.
    		# 이동했을 때 맵의 값이 1이어야 한다(0이거나, 이미 갔던 곳이면 안됨).
        if 0 <= nx < n and 0 <= my < m and maps[nx][my] == 1:
    ```
    
5. answer = 이동한 숫자 ⇒ 이미 지나간 곳은 몇 번째 이동인지 흔적 남기기
    
    ```python
     if 0 <= nx < n and 0 <= my < m and maps[nx][my] == 1:
          maps[nx][my] = maps[x][y]+1 # 이동한 위치 값(1)은 이동 횟수로 바꾼다.
          q.append((nx,my)) # q에 삽입, 다시 pop되어 반복된다.
    ```
    
6. 도착할 수 없는 경우에는 -1을 return한다.
    
    ```python
    # 맵 도착지점이 1인 경우는 아예 도착하지 못한 것이므로 -1을 return 한다.
    return maps[-1][-1] if maps[-1][-1] > 1 else -1
    ```
**deque를 사용한 문제.**


---
<이론 출처>

https://freedeveloper.tistory.com/