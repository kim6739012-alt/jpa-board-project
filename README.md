# JPA 게시판 프로젝트

이 프로젝트는 **Spring Boot + JPA** 기반의 간단한 게시판 웹 애플리케이션입니다.  
회원 기능, 게시글, 댓글 CRUD, 관리자 대시보드, OKR 관리 등 **웹 서비스의 기본 요소들을 전반적으로 다룹니다.**

---

## 사용 기술 스택

- Java 17  
- Spring Boot  
- Spring Data JPA  
- Thymeleaf  
- MySQL  
- Maven

---

## 테스트용 계정

| 역할     | ID         | PW     |
|----------|------------|--------|
| 관리자   | admin      | 1234   |
| 일반회원 | kim807     | 1234   |

---

## 주요 기능 요약

### 사용자 기능

- **회원가입**: 이름, 아이디, 비밀번호 입력  
- **로그인 / 로그아웃**: 세션 기반 인증 처리  
- **내 정보 페이지**: 회원가입 직후 바로 확인 가능  
- **게시글 작성**: 로그인한 사용자만 가능  
- **게시글 목록**: 전체 조회, 내가 쓴 글만 보기 필터링 가능  
- **게시글 상세 보기**: 댓글 작성 및 수정/삭제 가능  
- **게시글 검색 기능**: 제목, 작성자, 내용으로 상세 검색 가능  
- **좋아요 기능**: 다른 사람이 작성한 글에 좋아요, 싫어요 투표 가능  
- **댓글 기능**:  
  - 대댓글 지원  
  - 본인이 작성한 댓글/대댓글만 삭제 가능  

---

### 관리자 기능

- **대시보드**: 회원 수, 게시글 수, 댓글 수  
- **회원 목록 관리**: 회원 전체 조회 및 삭제  
- **게시글 목록 관리**: 게시글 전체 조회 및 삭제  
- **댓글 목록 관리**: 댓글 전체 조회 및 삭제  

---

### 🆕 OKR 기능

- **OKR 관리**: 사용자별 목표(Objective) 및 핵심 결과(Key Result) 등록    
- **핵심 결과 개수 제한**: 최소 3개, 최대 5개 등록 가능  
- **OKR 목록 화면**: 작성한 OKR 전체 확인 가능, 설명 및 핵심 결과 함께 표시  
- **목표 추가 버튼**: OKR 리스트 페이지에서 새 목표를 추가할 수 있는 버튼 제공  
- **메인 페이지 이동 버튼**: OKR 리스트에서 메인으로 돌아가기 버튼 제공  
- **삭제 시 리다이렉트 처리**: OKR 삭제 후 자동으로 리스트 페이지로 이동  

#### ➕ 확장 기능

- **핵심 결과 진행률 관리**  
  - **BINARY**: 완료/미완료 토글  
  - **NUMERIC**: 현재 값 입력하여 진행 상황 업데이트  
  - **MILESTONE**: 마일스톤 완료 +1 버튼 지원  
- **D-Day 표시**: Objective 마감일까지 남은 일수 표시  
- **일일 체크 기능**: 오늘의 핵심 결과 실천 여부 기록 가능  
- **주간 체크 기능**:  
  - 한 주(월~일) 단위로 KR 체크 내역을 테이블로 확인  
  - 날짜별 체크 여부를 버튼 클릭으로 토글 가능  
  - 주간 진행 상황을 **일자별 완료율 그래프**로 시각화  

---

## 프로젝트 구조

```plaintext
src
 └─ main
     ├─ java
     │   └─ com.example.start
     │       ├─ controller       # 요청 처리 컨트롤러 (AdminController, UserController, PostController, CommentController, ObjectiveController, KeyResultController, WeeklyOKRController)
     │       ├─ dto              # DTO 객체 (PostForm, CommentForm, ObjectiveForm, KeyResultForm, KeyResultResponse, ObjectiveResponse)
     │       ├─ entity           # JPA 엔티티 (User, Post, Comment, Objective, KeyResult, DailyCheck)
     │       ├─ enums            # 열거형 타입 (ReactionType, KRType)
     │       ├─ repository       # 데이터 접근 레이어 (UserRepository, PostRepository, CommentRepository, ObjectiveRepository, KeyResultRepository, DailyCheckRepository)
     │       ├─ service          # 서비스 인터페이스
     │       └─ service.impl     # 서비스 구현체 (PostServiceImpl, CommentServiceImpl, ObjectiveServiceImpl, DailyCheckServiceImpl ...)
     └─ resources
         ├─ templates
         │   ├─ admin
         │   │   ├─ dashboard.html
         │   │   ├─ user-list.html
         │   │   ├─ post-list.html
         │   │   └─ comment-list.html
         │   ├─ okr
         │   │   ├─ list.html
         │   │   ├─ weekly.html
         │   │   ├─ create.html
         │   │   └─ edit.html
         │   ├─ login.html
         │   ├─ main.html
         │   ├─ post-detail.html
         │   ├─ post-edit.html
         │   ├─ post-form.html
         │   ├─ post-list.html
         │   ├─ signup.html
         │   └─ user-info.html
         └─ application.properties
```

---

## 실행 방법

1. MySQL에서 `boarddb` 데이터베이스 생성  
2. `application.properties`에서 DB 연결 정보 확인  
3. 프로젝트 빌드 및 실행  

```bash
# macOS / Linux
./mvnw spring-boot:run

# Windows
mvnw.cmd spring-boot:run
```

4. 브라우저에서 http://localhost:8080 접속  

---

## 시연 예시

1. 회원가입 → 로그인  
2. 게시글 작성 → 댓글 작성  
3. OKR 작성 (Objective + Key Result 3~5개)  
4. 오늘의 KR 체크 (일일 체크)  
5. 주간 체크 페이지 → 각 요일별 진행 상황 확인 → 그래프에서 진행률 시각화  
6. 관리자 로그인 → 회원/게시글/댓글 관리
