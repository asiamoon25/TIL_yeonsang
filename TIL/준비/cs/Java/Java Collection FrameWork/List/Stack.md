---
sticker: emoji//1f929
---

#JavaCollectionFramework #List

## Stack 이란?

* 후입선출(LIFO, Last In First Out) 원칙에 따라 작동하는 기본적인 데이터 구조 -> 가장 마지막에 추가된 항목이 가장 먼저 제거됨.
* 함수 호출, 실행 취소 메커니즘, 구문 분석, 깊이 우선 탐색(DFS) 과 같은 알고리즘에 유용함.

## 특징
* 후입선출
	스택에 가장 마지막으로 추가된 요소가 가장 먼저 제거됨.
* 접근 제한
	맨 위의 요소만 직접 접근할 수 있으며, 그 아래에 있는 요소들에게는 직접 접근할 수 없음. 데이터의 순서를 엄격하게 관리
* 다양한 활용
	함수의 호출 및 반환, 깊이 우선 탐색, 구문 분석, 역폴란드 계산기, 실행 취소 기능 등에 활용됨.
* 단순한 구조
	구현이 간단하며, 데이터를 추가하거나 제거하는 연산이 빠름.


## 메서드
1. **push** : 스택의 맨 위에 요소를 추가함. 이 연산을 동해 스택에 새로운 데이터가 저장됨. `push(e)`
2. **pop** : 스택의 맨 위에 있는 요소를 제거하고 그 값을 반환함. 스택이 비어 있을 때 이 메서드를 호출하면 오류가 발생하거나 특정 값을 반환할 수 있음(구현에 따라 다름) `pop()`
3. **peek** or **top** : 스택의 맨 위에 있는 요소를 제거하지 않고 반환함. 스택을 변경하지 않고 맨위의 요소를 확인 할 수 있음.
4. **isEmpty()** : 스택이 비어 있는지 확인함. 스택에 요소가 없으면 `true` 없으면 `false` 를 반환함. `isEmpty()`
5. **size** : 스택에 저장된 요소의 총 수를 반환함. 스택의 크기를 알아내는 데 사용됨. `size()`

