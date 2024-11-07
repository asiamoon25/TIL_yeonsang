## BFS 의 기본 개념

1. **큐(Queue)** 를 이용해 노드를 방문함. 큐는 FIFO(First In First Out) 자료구조로, 먼저 들어온 노드부터 처리됨.
2. 시작 노드를 큐에 삽입하고 방문 처리를 함.
3. 큐에서 노드를 하나  꺼내 해당 노드와 인접한 모든 노드를 검사함.
	1. 인접 노드가 아직 방문하지 않았다면, 그 노드를 큐에 삽입하고 방문 처리를 함.
4. 큐가 빌 때까지 위 과정을 반복함.


## 장점 과 특징
* **최단 경로 탐색** 에 유리함. 모든 간선의 비용이 동일할 때, BFS 는 시작 노드에서 목표 노드까지의 최단 경로를 찾을 수 있음.
* **모든 노드 방문** : BFS 는 특정 노드가 목표 노드인지를 발견할 때까지 전체 노드를 탐색하므로 연결된 모든 노드를 차례로 탐색함.
* **시간  복잡도** 는 $O(V+E)$ , 여기서 $V$ 는 노드 수, $E$ 는 간선 수임.


## 알고리즘 예시
```python
from collections import deque

def bfs(graph, start) : 
	visited = [] # 방문한 노드 목록
	queue = deque([start]) # 탐색 시작 노드를 큐에 삽입

	while queue:
		node = queue.popleft() # 큐에서 노드 하나를 꺼내기
		if node not in visited:
			visited.append(node) # 방문 기록 추가
			# 인접 노드를 큐에 추가(방문하지 않은 노드만)
			queue.extend([n for n in graph[node] if n not in visited])
	return visited

# 그래프 예시(딕셔너리 형태)
graph = { 
		 'A': ['B', 'C'], 
		 'B': ['A', 'D', 'E'], 
		 'C': ['A', 'F'], 
		 'D': ['B'], 
		 'E': ['B', 'F'], 
		 'F': ['C', 'E'] 
}

print(bfs(graph, 'A'))
# 출력 : ['A', 'B', 'C', 'D', 'E', 'F']
```


## BFS 활용 사례
* **최단 경로 찾기**
* **웹 크롤링**
* **소셜 네트워크 분석**

BFS는 방문할 노드를 순차적으로 탐색하므로, 재귀적 방법보다는 큐를 이용해 반복문으로 구현하는 것이 일반적