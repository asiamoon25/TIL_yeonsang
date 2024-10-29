

```java
import java.util.*;
public class HIndex {
	public static int solution(int[] citations) {  
		int answer = 0;  
		  
		/*  
		index 0 value 6 => 1편의 논문에서 인용된 횟수 6번 1 >= 6 ? false
		*/  
		Arrays.sort(citations);  
		  
		for(int i = 0; i < citations.length; i++){  
			int h = citations.length - i;  
			  
			if(citations[i] >= h) {  
				answer = h;  
				break;  
			}  
		}  
		  
		return answer;  
	}  
  
	public static void main(String[] args) {  
		int[] citations = {3,0,6,1,5}; // 65310  
		System.out.println(solution(citations));
	}
}
```