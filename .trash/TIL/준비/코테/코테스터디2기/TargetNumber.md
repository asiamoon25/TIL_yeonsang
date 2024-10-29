https://school.programmers.co.kr/learn/courses/30/lessons/43165

```java
package sail_phase2;
public class TargetNumber {
    /*
    n개의 음이 아닌 정수들이 있습니다.
    이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다.
    예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.
    -1+1+1+1+1 = 3
    +1-1+1+1+1 = 3
    +1+1-1+1+1 = 3
    +1+1+1-1+1 = 3
    +1+1+1+1-1 = 3
    사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.
    제한사항
    주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
    각 숫자는 1 이상 50 이하인 자연수입니다.
    타겟 넘버는 1 이상 1000 이하인 자연수입니다.
     */
    public static int solution(int[] numbers, int target) {
        /*
        DFS 를 사용한 해결 방법
        1. 재귀 함수 정의 : 현재 인덱스와 현재까지의 합을 인자로 받는 재귀 함수를 정의함.
        2. 종료 조건 : 모든 숫자를 사용했을 때 현재까지의 합의 타겟 넘버와 같으면 1을 반환하고, 그렇지 않으면 0을 반환
        3. 재귀 호출 : 현재 숫자를 더하거나 빼는 두 가지 경우에 대해 재귀적으로 함수를 호출함.
        4. 결과 합산 : 두 가지 경우의 결과를 합산하여 반환함.
         */
        return dfs(numbers,target, 0,0);
    }

    private static int dfs(int[] numbers, int target, int index, int sum){
        // 모든 숫자를 사용했을 때
        if(index == numbers.length){
            //현재까지의 합이 타겟과 같다면 1을 반환하여 경로를 카운트
            return sum == target ? 1 : 0;
        }
        // 현재 숫자를 더하는 경우
        int countWithAddtion = dfs(numbers, target, index + 1, sum + numbers[index]);

        //현재 숫자를 빼는 경우
        int countWithSubtraction = dfs(numbers, target, index + 1, sum - numbers[index]);
        // 두 경우의 결과를 합산하여 반환
        return countWithAddtion + countWithSubtraction;
    }

    public static void main(String[] args) {
        int[] numbers = {1,1,1,1,1};
        int target = 3;
        System.out.println(solution(numbers,target)); // 5
    }
}
```

DFS 알고리즘을 사용해서 해결

[[DFS(깊이 우선 탐색)]]


