* 형상 관리 도구
	버전 관리 도구라고도 함.
	과거 작업 내역과 현재 작업 내역, 그리고 변경점을 확인할 수 있도록 만들어진 도구

* SVN과의 차이점 
	* SVN 는 중앙 서버 저장소에서 소스코드와 히스토리를 저장하는 형태, git 은 여러 서버 저장소와 여러 로컬 저장소에 분산해서 저장할 수 있다는 점이 있다.
	  서버가 고장나더라도 로컬 저장소를 통해 중앙 저장소를 복구할 수 있음.

* local,remote 및 origin, upstream
	* local
		사용자의 컴퓨터 폴더..
	* remote
		소스코드를 저장하고 공유할 수 있는 원격 저장소(GitHub, GitLab, Bitbucket)
		**remote(upstream)** 은 소스코드 원형이 기록된 서버 저장소,
		**remote(origin)** 은 원형을 복제해서 만든 내 서버 저장소
		**local**은 remote(origin)을 토대로 내 PC 에 저장해 놓은 저장소


* Git Status (파일 상태)
	작업 중인 파일은 local에서 4가지의 상태를 나타냄.
	Untracked, Unmodified, Modified, Staged
	![[Pasted image 20231215102539.png]]
	
	**Untracked**
		폴더에 파일이 새로 생성되는 경우
	**Unmodified(Tracked)**
		Commit을 한 번이라도 실행하여 추적이 가능한 상태
	**Modified(Tracked)**
		Working Directory 에서 파일을 수정이나 제거하는 경우 Modified 상태로 변경
	**Staged(Tracked)**
		Unmoidifed나 Modified 상태에서는 git add 명령어를 통해 Stage 로 올린 것
	-> git commit 명령어로 GIt 저장소에 히스토리인 Commit 으로 반영되며, 반영된 파일들은 Unmodified(Tracked) 로 변경 됨.

* Git Branch
	2개의 작업을 동시에 할 때, Branch 를 통해 쉽게 할 수 있음.
	독립적인 작업 공간 생성이 가능함.
	
	마지막 지점인 HEAD 에서 A 라는 Branch 를 생성 및 작업하고 Commit 을 한 이후 (HEAD는 A 마지막 작업 지점으로 변경)에 작업 이전인 원래 HEAD 위치로 돌아와서 B라는 Branch를 생성 및 작업을 하면 A작업 내역과 B 작업 내역을 동시에 확인 할 수 있음.
	
	Branch A , Branch B 를 하나의 Branch 로 합치는 작업을 Merge 라고도 함. 필요에 따라 A에서 B를 merge 하거나 반대 상황도 가능함.