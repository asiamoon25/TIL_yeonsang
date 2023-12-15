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
	**Tracked**
		Commit을 한 번이라도 실행하여 추적이 
	