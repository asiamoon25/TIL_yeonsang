
https://leetcode.com/problems/smallest-number-in-infinite-set/


_예지님 번역.._
당신은 모든 자연수를 갖는 수열을 가지고 있습니다 .[1,2,3,4,5…] SmallestInfiniteSet 클래스를 구현하시오 SmallestInfiniteSet() : 양수의 자연수만 들어갈 수 있도록 SmallestInfiniteSet 를 초기화 합니다 . int popSmallest() 무한 수열에서 가장작은 Integer 를 리턴하고 제거합니다 . void addBasck(int num) : 무한수열에 있지 않은 자연수 num 을 무한수열에 추가합니다 .


```java
package sail_phase2;

import java.util.PriorityQueue;

public class SmallestInfiniteSet {
    PriorityQueue<Integer> q;
    int i = 1;
    public SmallestInfiniteSet() { // 모든 양의 정수를 포함하도록 초기화
        q = new PriorityQueue<>();
    }

    public int popSmallest(){
        if(q.size() == 0) {
            return i++;
        }
        return q.poll();
    }
    public void addBack(int num) {
        if(num < i && !q.contains(num)){
            q.add(num);
        }
    }
}
```


![[Pasted image 20240525124021.png]]

처음 푼걸로 하면

```java
public class SmallestInfiniteSet {

	PriorityQueue<Integer> q = new PriorityQueue<>();
	public SmallestInfiniteset() {
		for(int i = 1; i <= 1000; i++) {
			q.add(i);
		}
	}
	public int popSmallest() {
		int min = 0;
		if(!q.isEmpty()){
			min = q.poll();
		}
		return min;
	}

	public void addBack(int num) {
		if(!q.contains(num)) {
			q.add(num);
		}
	}
}
```

위 방식으로 생성자 초기화 시 48ms 로 증가함.