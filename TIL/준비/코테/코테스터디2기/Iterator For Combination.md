https://leetcode.com/problems/iterator-for-combination/description/

**번역**

다음은 CombinationIterator 클래스를 설계하는 문제입니다:  

```text
CombinationIterator(string characters, int combinationLength):  
문자열 characters와 정수 combinationLength를 인수로 받아 객체를 초기화합니다.  
characters는 정렬된 중복되지 않는 소문자 영어 문자들로 구성됩니다.  
  
next():  
combinationLength 길이의 다음 조합을 사전식 순서로 반환합니다.  
  
hasNext():  
다음 조합이 존재할 경우에만 true를 반환합니다.  
이 문제를 해결하기 위해 클래스를 설계하고 구현해야 합니다.
```


```java
public class CombinationIterator {

    private List<String> combinations;
    private int index;

    public CombinationIterator(String characters, int combinationLength) {
        this.combinations = new ArrayList<>();
        this.index = 0;
        generateCombinations(characters, combinationLength, 0, new StringBuilder());
    }


    private void generateCombinations(String characters, int combinationLength, int start, StringBuilder current) {
        if (current.length() == combinationLength) {
            combinations.add(current.toString());
            return;
        }
        for (int i = start; i < characters.length(); i++) {
            current.append(characters.charAt(i));
            generateCombinations(characters, combinationLength, i + 1, current);
            current.deleteCharAt(current.length() - 1);
        }
    }

    public String next() {
        if (hasNext()) {
            return combinations.get(index++);
        }
        return null;
    }

    public boolean hasNext() {
        return index < combinations.size();
    }
}
```



1. 필드 선언
```java
private List<String> combinations;
private int index;
```

* `combinations` : 생성된 조합을 저장할 리스트
* `index` : 현재 반환할 조합의 인덱스


2. 생성자

```java
public CombinationIterator(String characters, int combinationLength) {
	this.combinations = new ArrayList<>();
	this.index = 0;
	generateCombinations(characters, combinationLength, 0, new StringBuilder());
}
```

* 문자열 `characters` 와 조합의 길이 `combinationLength` 를 인수로 받아 초기화함.
* `generateCombination` 메서드를 호출하여 모든 조합을 생성함.

3. 조합 메서드 (DFS 사용)
```java
private void generateCombinations(String characters, int combinationLength, int start, StringBuilder current) {
	if(current.length() == combinationLength) {
		combinations.add(current.toString());
		return;
	}
	for(int i = start; i < characters.length(); i++) {
		// 현재 문자를 추가
		current.append(characters.charAt(i));
		// 재귀 호출
		generateCombinations(characters, combinationLength, i+1, current);
		//백트래킹
		current.deleteCharAt(current.length() -1);
	}
}
```

* `current.length()` 가 `combinationLength` 와 같아지면 현재 조합을 리스트에 추가하고 종료함.
* 그렇지 않으면, 시작 인덱스부터 문자를 하나씩 추가하고, 재귀적으로 다음 문자를 처리함.
* 추가한 문자를 제거(백트래킹)하여 다음 조합을 생성할 준비를 함.

4. 다음 조합 반환
```java
public String next() {
	if(hasNext()){
		return combination.get(index++);
	}
	return null;
}
```

* `hasNext()` 가 true 일 경우, 현재 인덱스의 조합을 반환하고 인덱스를 증가시킴

5. 다음 조합이 있는지 확인
```java
public boolean hasNext() {
	return index < combinations.size();
}
```

* 현재 인덱스가 조합 리스트 크기보다 작은지 확인하여 다음 조합이 있는지 확인함.



## 왜 DFS?

모든 가능한 조합을 탐색할 수 있기 때문.
재귀적으로 각 문자를 선택하거나 선택하지 않는 방식으로 조합을 생성하는 데 적합함. DFS 를 사용하면 백트래킹을 통해 조합 생성을 간단하게 구현할 수 있음.