---
sticker: lucide//settings
---
**Set**
* 중복된 요소를 저장하지 않고, 요소의 저장 순서를 유지하지 않는 특징을 가짐.
* Set 의 구현체로 HashSet, LinkedHashSet, TreeSet 이 있음.
	**중복된 요소 걸러내는 법**
	* equals() 와 hashCode() 를 사용
		1. 객체를 저장하기 전에 해시 코드를 호출해서 해시코드를 얻어냄.
		2. Set 에 저장되어 있는 요소들의 해시코드와 비교
		3. 만약 같은 해시코드가 있다면 equals() 메소드로 두 객체를 비교
		4. equals() 메소드가 true 가 나오면 중복으로 판단하여 저장하지 않음.