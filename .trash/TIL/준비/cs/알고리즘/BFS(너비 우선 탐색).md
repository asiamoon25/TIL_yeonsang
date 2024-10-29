
## BFS 란?

![[Pasted image 20240616230809.png]]

* 너비 우선 탐색(Breadth-First Search)은 그래프나 트리에서 시작 정점으로부터 모든 인접 정점을 먼저 방문한 후, 그 다음으로 가까운 정점들을 방문하는 방식으로 탐색하는 알고리즘.
* 주로 최단경로를 찾는데 유용하며, 큐 자료구조를 사용해 구현됨.


## 특징

1. **최단경로 탐색**
	* BFS 는 최단경로를 찾는 데 적합함. 동일 가중치 그래프에서 최단 경로를 찾는 데 사용됨. 

2. **Queue 사용**
	* BFS 는 Queue 자료구조를 사용하여 구현됨.

3. **레벨 탐색**
	* 동일한 레벨에 있는 정점들을 먼저 탐색한 후, 다음 레벨로 이동함.

4. **방문 기록**
	* 방문한 정점을 기록하여, 동일 정점을 여러 번 방문하지 않도록 함.


## 과정

1. **시작 정점 방문**
	* 시작 정점을 큐에 삽입하고 방문했다고 표시함.

2. **큐에서 정점 꺼내기**
	* 큐에서 정점을 꺼내 그 정점에 인접한 모든 정점을 탐색함.

3. **인접 정점 삽입**
	* 인접한 정점 중 방문하지 않은 정점을 큐에 삽입하고 방문했다고 표시함.

4. **반복**
	* 큐가 빌 때까지 2번과 3번 과정을 반복함.



## 구현

* BFS 를 구현하는 방법은 큐를 사용하는 방법.

**인접 리스트를 사용**
```java
public class BFSExample {
	public static void main(String[] args) {
		// 그래프를 인접리스트로 표현
		Map<Integer, List<Integer>> graph = new HashMap<>();
		graph.put(0, Arrays.asList(1,2));
		graph.put(1, Arrays.asList(0,3,4));
		graph.put(2, Arrays.asList(0,5,6));
		graph.put(3, Arrays.asList(1));
		graph.put(4, Arrays.asList(1));
		graph.put(5, Arrays.asList(2));
		graph.put(6, Arrays.asList(2));
		
		// 방문한 정점을 기록하기 위한 배열
		boolean[] visited = new boolean[graph.size()];
		
		//BFS 탐색 시작 (시작 정점 0)
		bfs(graph, 0 ,visited);
	}
	
	public static void bfs(Map<Integer, List<Integer>> graph, int start, boolea[] visited) {
		Queue<Integer> queue = new LinkedList<>();
		queue.add(start);
		visited[start] = true;
		
		while(!queue.isEmpty()) {
			int v = queue.poll();
			System.out.print(v + " ");
			
			for(int neighbor : graph.get(v)) {
				if(!visited[neighbor]) {
					queue.add(neighbor);
					visited[neighbor] = true;
				}
			}
		}
	}
}
```

위 코드는 인접 리스트로 그래프를 표현하고, BFS 를 통해 모든 정점을 탐색하는 콛,

**인접 행렬을 사용**

* 인접 행렬을 사용하여 그래프를 표현하고, 큐를 사용하여 BFS 를 구현함.
```java
public class BFSExample{
	public static void main(String[] args) {
		// 그래프를 인접 행렬로 표현
		int[][] graph = {
			{0, 1, 1, 0, 0, 0, 0}, 
			{1, 0, 0, 1, 1, 0, 0}, 
			{1, 0, 0, 0, 0, 1, 1}, 
			{0, 1, 0, 0, 0, 0, 0}, 
			{0, 1, 0, 0, 0, 0, 0}, 
			{0, 0, 1, 0, 0, 0, 0}, 
			{0, 0, 1, 0, 0, 0, 0}
		};
		
		// 방문한 정점을 기록하기 위한 배열
		boolean[] visited = new boolean[graph.length];
		
		bfs(graph, 0, visited);
	}
	
	public static void bfs(int[][] graph, int start, boolean[] visited) {
		Queue<Integer> queue = new LinkedList<>();
		queue.add(start);
		visited[start] = true;
		
		while(!queue,isEmpty()) {
			int v = queue.poll();
			System.out.print(v + " ");
			
			for(int i = 0; i < graph.length; i++) {
				if(graph[v][i] == 1 && !visited[i]) {
					queue.add(i);
					visited[i] = true;
				}
			}
		}
	}
}
```

위 코드는 인접 행렬로 그래프를 표현하고, BFS를 통해 모든 정점을 탐색하는 코드임.



**BFS** 는 그래프나 트리의 모든 정점을 방문하는 데 사용하는 탐색 알고리즘임.

큐를 사용하여 구현하며, 최단 경로를 찾는 데 적합함. BFS 의 주요 특징은 동일한 레벨에 있는 정점들을 먼저 탐색하고, 모든 경로를 너비 우선으로 탐색한다는 점임.

BFS는 인접 리스트와 인접 행렬 두 가지 방법으로 구현할 수 있으며, 두 방법 모두 큐를 사용하여 탐색을 진행함.

