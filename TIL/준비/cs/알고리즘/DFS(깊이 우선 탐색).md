
* 그래프란?
	* 선형구조
	* 비 선형구조
* 깊이 우선 탐색이란
	* 특징
	* 과정
* 깊이 우선 탐색 구현
	* 구현방법 1
	* 구현방법 2



## Graph 란?

그래프는 정점(Vertex)과 그 정점을 연결하는 간선(Edge)으로 구성된 자료구조임.
그래프는 선형 구조와 비선형 구조로 나눌 수 있음.

**선형구조**
![[Pasted image 20240616161404.png]]

* 하나의 자료 뒤에 하나의 자료가 존재하는 것
* 자료들 간의 앞뒤 관계가 1:1의 선형 관계
* 배열과 리스트가 대표적이고 더 나악서 스택, 큐도 이에 해당됨.
	* **배열** : 정적이고, 요소들이 연속적으로 배치된 선형 구조
	* **연결 리스트** : 동적이고, 요소들이 포인터로 연결된 선형 구조


**비선형 구조**
![[Pasted image 20240616161416.png]]

* 하나의 자료 뒤에 여러개의 자료가 존재할 수 있는 것
* 자료들 간의 앞뒤 관계가 1:n, 또는 n:n의 관계
* 트리와 그래프가 대표적이며 계층적 구조를 나타내기에 적합함.
	* **트리** : 계층적 관계를 나타내는 비선형 구조임. 루트에서 시작해 자식 노드로 분기됨.
	* **그래프** : 정점들이 간선으로 연결된 일반적인 비선형 구조. 방향성이 있는 유향 그래프와 없는 무향 그래프로 나뉘어짐.


## 깊이 우선 탐색이란?

DFS(Depth-First Search) 는 그래프 또는 트리의 모든 정점을 방문하는 탐색 알고리즘임.

시작 정점에서 출발하여 가능한 한 깊게 탐색한 후, 더 이상 갈 곳이 없으면 되돌아와서 다른 경로를 탐색함.

**특징**

* **재귀적 특성**
	* DFS 는 재귀를 통해 구현되는 경우가 많음. 현재 경로를 추적하고, 더 이상 방문할 장점이 없을 때 되돌아감.

* **스택사용**
	* DFS 는 스택을 사용함. 재귀 호출은 내부적으로 스택을 사용하며, 명시적으로 스택 자료구조를 사용할 수도 있음.

* **경로 탐색**
	* 깊게 탐색하여 경로를 찾음. 모든 경로를 탐색하므로 경로의 깊이 깊어질 수록 비효율적일 수 있음.

* **순환 탐지**
	* 그래프에 순환이 있는 경우 이를 탐지하여 무한 루프를 방지해야함.


**과정**

1. 시작 정점을 방문하고, 방문했다고 표시함.
2. 현재 정점에 인접한 정점들 중 방문하지 않은 정점을 선택하여 탐색을 계속함.
3. 더 이상 방문할 정점이 없으면 되돌아가며 다른 경로를 탐색함.
4. 모든 정점을 방문할 때까지 이 과정을 반복함.


## 깊이 우선 탐색 구현

2가지

### 재귀

* 재귀적 DFS 는 간단하고 직관적임. 현재 정점에서 시작하여 인접한 정점들을 재귀적으로 방문함.

```java
import java.util.*;
public class DFSRecursive{
	public static void main(String[] args) {
		// 그래프를 인접 리스트로 표현
		Map<Integer, List<Integer>> graph = new HashMap<>();
		graph.put(0, Arrays.asList(1,2));
		graph.put(1, Arrays.asList(0,3,4));
		graph.put(2, Arrays.asList(0,5,6));
		graph.put(3, Arrays.asList(1));
		graph.put(4, Arrays.asList(1));
		graph.put(5, Arrays.asList(2));
		graph.put(6, Arrays.asList(2));
		
		//방문한 정점을 기록하기 위한 배열
		boolean[] visited = new boolean[graph.size()];
		
		// DFS 탐색 시작(시작 정점은 0)
		dfs(graph, 0, visited);
	}
	
	public static void dfs(Map<Integer, List<Integer>> graph, int v, boolean[] visited) {
		//현재 정점을 방문했다고 표시
		visited[v] = true;
		System.out.println(v + " ");
		
		// 현재 정점에 연결된 모든 정점을 가져와서
		for(int neighbor : graph.get(v)) {
			//방문하지 않은 정점에 대해 재귀적으로 DFS 수행
			if(!visited[neighbor]) {
				dfs(graph, neighbor, visited);
			}
		}
	}
}
```

위 코드는 그래프를 인접 리스트로 표현하고, 재귀적으로 DFS 를 수행하여 모든 정점을 방문함.


### 스택

* 스택을 사용하여 DFS 를 구현하면 재귀 호출의 깊이 제한을 피할 수 있음. 스택을 사용하여 명시적으로 탐색 경로를 관리함.

```java
import java.util.*;

public class DFSIterative {
    public static void main(String[] args) {
        // 그래프를 인접 리스트로 표현
        Map<Integer, List<Integer>> graph = new HashMap<>();
        graph.put(0, Arrays.asList(1, 2));
        graph.put(1, Arrays.asList(0, 3, 4));
        graph.put(2, Arrays.asList(0, 5, 6));
        graph.put(3, Arrays.asList(1));
        graph.put(4, Arrays.asList(1));
        graph.put(5, Arrays.asList(2));
        graph.put(6, Arrays.asList(2));

        // 방문한 정점을 기록하기 위한 배열
        boolean[] visited = new boolean[graph.size()];

        // DFS 탐색 시작 (시작 정점은 0)
        dfs(graph, 0, visited);
    }

    public static void dfs(Map<Integer, List<Integer>> graph, int start, boolean[] visited) {
        Stack<Integer> stack = new Stack<>();
        stack.push(start);

        while (!stack.isEmpty()) {
            int v = stack.pop();

            if (!visited[v]) {
                visited[v] = true;
                System.out.print(v + " ");

                // 스택에 인접한 정점들을 추가 (방문하지 않은 정점만)
                for (int neighbor : graph.get(v)) {
                    if (!visited[neighbor]) {
                        stack.push(neighbor);
                    }
                }
            }
        }
    }
}
```


---

해당 방식은 뭔가 2개의 선택지에서 2가지 모두를 다 조회한다음에 결과를 내는 알고리즘인거 같음.