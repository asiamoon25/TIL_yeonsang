![[Pasted image 20240111160833.png]]
![[Pasted image 20240111160849.png]]

![[Pasted image 20240111160859.png]]



### data
* external
	타사 소스(불변 데이터) 에서 추출한 데이터. 
* interim
	외부 데이터를 사용할 수 있는 경우 src/data 디렉터리의 스크립트를 사용하여 기능 엔지니어링을 위해 로드하는 데이터
* Processed
	다양한 기계 학습 기술을 사용하여 변환된 데이터. src 폴더에 있는 기능 폴더는 데이터를 모델링 할 준비가 되도록 다양한 변환을 수행. 모델의 학습 시간을 단축하기 위해 처리된 데이터를 유지하는 것이 좋음
* raw
	데이터의 로컬 하위 집합 복사본이 있으면, 작업을 수행할 정적 데이터 집합이 있음.
	또한 네트워크 대기 시간문제로 인한 워크플로 중단을 극복함. => 이 데이터는 변경 불가능한 것으로 간주되어야 함. 외부 데이터가 없으면 src/data 에 있는 스크립트에 의해 다운로드된 데이터임.

### model

기계 학습 모델 학습을 위해 src/models의 스크립트를 사용함. 앙상블을 구축하거나 비교하기 위해 모델을 다른 모델과 함께 복원하거나 재사용해야 할 수 있으며 배포할 모델을 결정할 수 있음.
이를 위해 훈련된 모델을 파일(보통 피클 형식) 에 저장하면 해당 파일이 이 디렉터리에 저장된다.

### notebook
Jupyter 노트북은 프로토 타이핑, 탐색 및 결과 전달에 탁월하지만 장기적인 성장에는 좋지 않으며 재현성에 대해서는 덜 효과적 일 수 있음.
노트북은 Notebooks/explorations 나 Notebooks/PoC 와 같은 하위 폴더로 나뉠 수 있음. 
좋은 이름 지정 규칙을 사용하면 각 노트북을 채우는 것을 구별하는 데 도움이 된다. 

유용한 템플릿은 단 게가 순서 지정 메커니즘으로 사용되는 것은 다음과 같다.

**"<step>-<user>-<descriotion>.ipnyb" (01-kpy-eda.ipynb)**

### 


