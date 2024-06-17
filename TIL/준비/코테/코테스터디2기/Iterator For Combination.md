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

