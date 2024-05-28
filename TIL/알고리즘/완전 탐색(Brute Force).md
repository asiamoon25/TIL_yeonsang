---
sticker: emoji//1f91a
---

## 완전탐색이란?

모든 경우의 수를 시도하는 방법
* 상대적으로 구현이 간단하고, 해가 존재하면 항상 찾게 됨.
* 경우의 수에 따라 실행 시간이 비례하기 때문에 입력 값의 범위가 작은 경우 유용.

## 특징

1. 단순성, 직관성 : 복잡한 알고리즘을 고안하기 전에 초기 접근 방법으로 사용할 수 있으며, 문제의 해법을 이해하는 데 도움이 됨.
2. 확실한 정답 도출 : 모든 가능한 경우를 검토하기 때문에, 해답이 존재한다면 반드시 찾을 수 있음.

## 유형

1. 반복문을 이용한 탐색 : 가장 간단한 형태로, 모든 가능한 경우를 반복문을 사용해 순차적으로 탐색함.
2. 재귀를 이용한 탐색 : 복잡한 문제에서 여러 조건에 따라 분기가 필요할 때 유용함. 재귀적으로 문제를 작은 단위로 나누어 해결함.
3. 순열과 조합을 이용한 탐색 : 특정 아이템의 모든 순열이나 조합을 생성하각 경우에 대해 문제의 조건을 충족하는지 검사함.
4. 비트마스크를 이용한 탐색 : 아이템의 포함 여부를 비트로 표현하여, 모든 조합의 가능성을 탐색함.



## 예시
**주어진 리스트의 모든 부분집합 출력**

```java
import java.util.ArrayList;
import java.util.List;

public class SubsetFinder {
    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        List<List<Integer>> subsets = findSubsets(nums);
        for (List<Integer> subset : subsets) {
            System.out.println(subset);
        }
    }

    public static List<List<Integer>> findSubsets(int[] nums) {
        List<List<Integer>> subsets = new ArrayList<>();
        subsets.add(new ArrayList<>()); // 공집합 추가

        for (int num : nums) {
            List<List<Integer>> newSubsets = new ArrayList<>();
            for (List<Integer> subset : subsets) {
                List<Integer> newSubset = new ArrayList<>(subset); // 현재 부분집합을 새로운 리스트로 복사
                newSubset.add(num); // 현재 숫자 추가
                newSubsets.add(newSubset); // 새로운 부분집합을 newSubsets에 추가
            }
            subsets.addAll(newSubsets); // 모든 새 부분집합을 기존 부분집합 리스트에 추가
        }

        return subsets;
    }
}
```

위 코드는 각 요소를 순차적으로 검토하면서 기존의 모든 부분집합에 현재 요소를 추가한 새로운 부분집합을 생성함.

