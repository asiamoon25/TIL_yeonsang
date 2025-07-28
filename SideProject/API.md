● � 백엔드 API 명세서

  프론트엔드 코드 분석 결과, 다음과 같은 API들이 필요합니다:

  � 1. 핵심 블로그 API

  포스트 관련

  GET    /api/posts                     # 포스트 목록 (페이지네이션)
  GET    /api/posts/featured            # 메인 페이지용 추천 포스트
  GET    /api/posts/{slug}              # 포스트 상세 조회
  GET    /api/posts/{slug}/related      # 관련 포스트
  POST   /api/posts/{postId}/views      # 조회수 증가

  카테고리 & 태그

  GET    /api/categories                # 카테고리 목록
  GET    /api/categories/{slug}         # 카테고리 상세
  GET    /api/categories/{slug}/posts   # 카테고리별 포스트

  GET    /api/tags                      # 태그 목록
  GET    /api/tags/popular              # 인기 태그
  GET    /api/tags/{slug}/posts         # 태그별 포스트

  검색 기능

  GET    /api/search                    # 통합 검색 (필터링 지원)
  GET    /api/search/suggestions        # 검색 자동완성

  � 2. 댓글 시스템 API

  GET    /api/posts/{postId}/comments   # 댓글 목록 (트리 구조)
  POST   /api/posts/{postId}/comments   # 댓글 작성
  PUT    /api/comments/{id}             # 댓글 수정
  DELETE /api/comments/{id}             # 댓글 삭제

  � 3. 사용자 액션 API

  POST   /api/newsletter/subscribe      # 뉴스레터 구독
  POST   /api/contact                   # 문의 메시지 전송
  POST   /api/upload/image              # 이미지 업로드

  ⚡ 4. 관리자 API

  인증

  POST   /api/admin/login               # 관리자 로그인
  POST   /api/admin/logout              # 로그아웃
  GET    /api/admin/profile             # 프로필 조회

  포스트 관리

  GET    /api/admin/posts               # 관리용 포스트 목록
  POST   /api/admin/posts               # 새 포스트 작성
  PUT    /api/admin/posts/{id}          # 포스트 수정
  DELETE /api/admin/posts/{id}          # 포스트 삭제
  PATCH  /api/admin/posts/bulk          # 일괄 작업

  댓글 관리

  GET    /api/admin/comments            # 모든 댓글 관리
  PATCH  /api/admin/comments/{id}/approve  # 댓글 승인
  DELETE /api/admin/comments/{id}       # 댓글 삭제

  대시보드

  GET    /api/admin/stats               # 블로그 통계
  GET    /api/admin/recent-posts        # 최근 포스트
  GET    /api/admin/recent-comments     # 최근 댓글
  GET    /api/admin/analytics           # 상세 분석

  기타 관리

  GET    /api/admin/subscribers         # 구독자 목록
  GET    /api/admin/contacts            # 문의 목록
  POST   /api/admin/categories          # 카테고리 생성/수정
  POST   /api/admin/tags                # 태그 생성/수정

  � 표준 응답 형태

  목록 조회 응답

  {
    "data": [...],
    "pagination": {
      "currentPage": 1,
      "totalPages": 10,
      "totalCount": 100
    }
  }

  단일 조회 응답

  {
    "id": "1",
    "title": "포스트 제목",
    "content": "내용...",
    "createdAt": "2024-01-15T00:00:00Z"
  }

  � 우선순위

  1단계 (필수)

  - 포스트 CRUD
  - 카테고리/태그 조회
  - 기본 검색
  - 관리자 로그인

  2단계 (중요)

  - 댓글 시스템
  - 파일 업로드
  - 대시보드 통계

  3단계 (부가)

  - 뉴스레터
  - 고급 분석
  - 문의 관리


----
# Admin API

� 우선순위 높음

  1. GET /api/admin/stats - 대시보드 통계 데이터
  2. GET /api/admin/posts/recent?limit=5 - 최근 포스트 목록
  3. GET /api/admin/comments/recent?limit=5 - 최근 댓글 목록
  4. GET /api/admin/posts - 포스트 목록 (페이징, 필터링, 검색)
  5. POST /api/admin/posts - 새 포스트 생성
  6. GET /api/admin/posts/{id} - 개별 포스트 조회 (편집용)
  7. PUT /api/admin/posts/{id} - 포스트 수정
  8. DELETE /api/admin/posts/{id} - 포스트 삭제
  9. GET /api/admin/categories - 카테고리 목록

  � 우선순위 중간

  10. PATCH /api/admin/posts/bulk - 포스트 일괄 작업
  11. POST /api/admin/upload/image - 이미지 업로드

  � 우선순위 낮음 (미래 확장용)

  12. GET /api/admin/comments - 댓글 관리
  13. PATCH /api/admin/comments/{id}/status - 댓글 상태 변경
  14. DELETE /api/admin/comments/{id} - 댓글 삭제
  15. GET /api/admin/analytics - 분석 데이터
  16. GET /api/admin/subscribers - 구독자 관리
  17. GET /api/admin/settings - 설정 관리
  18. PUT /api/admin/settings - 설정 수정
