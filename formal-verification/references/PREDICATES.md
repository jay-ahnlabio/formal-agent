# PREDICATES v2 (Specs & Logic Contracts)

> 이 파일은 시스템의 **동작 방식(Behavior)**과 **데이터 구조(Type)**를 정의합니다.
> 입력/출력, 상태 변화에 대한 논리적 계약서입니다.

---

## 1. Ontology (Type Definitions)

> 데이터의 형상(Shape)을 Haskell-like Pseudo ADT로 정의
> 하나의 정의로 다이어그램, 유효성 검사, TS 타입 모두를 파생

### 1.1 Template

```haskell
-- 상태 머신 예시: 각 상태가 필요로 하는 데이터를 명시
data EntityStatus
  = Initial                    -- 초기 상태
  | Processing Context         -- 처리 중 (Context 필수)
  | Completed Result           -- 완료 (Result 필수)
  | Failed Error               -- 실패 (Error 필수)

data Context = Context {
  id        :: UUID,
  timestamp :: DateTime,
  metadata  :: Map String Value
}
```

### 1.2 Defined Types

<!-- 여기에 프로젝트별 타입 정의 추가 -->

```haskell
-- Example: User Domain
data UserStatus
  = Guest                       -- 비로그인
  | PendingVerification Email   -- 이메일 인증 대기
  | Active UserProfile          -- 활동 중
  | Banned Reason               -- 정지됨

data UserProfile = UserProfile {
  id    :: UUID,
  email :: Email,
  role  :: Role
}

data Role = User | Admin
```

---

## 2. Functional Predicates (Behaviors)

> Gherkin 문법으로 시스템의 논리적 계약 정의
> "상태 전이(State Transition)"를 설명

### 2.1 Template

```gherkin
Feature: [기능명]
  As a [역할]
  I want [목표]
  So that [이유]

  Scenario: [정상 케이스]
    Given [초기 상태]
    And [추가 조건]
    When [행동]
    Then [예상 결과]

  Scenario: [엣지 케이스]
    Given [초기 상태]
    When [예외 행동]
    Then [예외 처리 결과]
```

### 2.2 Defined Features

<!-- 여기에 프로젝트별 Feature/Scenario 추가 -->

```gherkin
Feature: User Registration
  As a guest user
  I want to create an account
  So that I can access member features

  Scenario: Successful Registration
    Given a guest user with valid email "test@example.com"
    And password meets complexity requirements
    When user submits registration form
    Then user status changes to PendingVerification
    And verification email is sent

  Scenario: Duplicate Email
    Given a guest user with email "existing@example.com"
    And email already exists in system
    When user submits registration form
    Then registration fails with "EMAIL_ALREADY_EXISTS" error
```

---

## 3. System Constraints

> 기술적 제약사항 및 불변식(Invariants)

### 3.1 Performance Constraints

```
Response Time: API 응답 < 200ms (95th percentile)
Throughput: 동시 접속 100명 처리
Memory: 프로세스당 512MB 이하
```

### 3.2 Error Handling

```
Async Operations: 모든 비동기 요청은 try-catch 또는 Result Pattern 사용
Timeout: 외부 API 호출 시 5초 타임아웃 필수
Retry: 일시적 실패 시 최대 3회 재시도 (exponential backoff)
```

### 3.3 Type Invariants

```haskell
-- Type Class Laws처럼 동작해야 하는 제약조건
invariant: forall u :: UserProfile. length(u.email) < 255
invariant: forall u :: UserProfile. u.id is unique
invariant: forall r :: Role. r in {User, Admin}
```

---

## 4. Verification Checklist

신규 Feature 추가 시:

- [ ] Ontology에 관련 Type 정의 완료
- [ ] 정상 케이스 Scenario 작성
- [ ] 엣지 케이스 Scenario 작성 (최소 1개)
- [ ] System Constraints 영향 분석
- [ ] 테스트 코드로 Scenario 검증 가능 확인

-----
