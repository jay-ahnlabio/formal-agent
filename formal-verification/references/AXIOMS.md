# AXIOMS v2 (Invariants & Rules)

> 이 파일은 프로젝트 전체를 관통하는 **절대적인 규칙**을 정의합니다.
> 임의로 변경될 수 없으며, Fact/Rule/불변의 진리(Invariants)를 포함합니다.

---

## 1. Tech Stack (Facts)

> 프로젝트에 맞는 언어를 적용하되, 명시된 도구는 반드시 사용

| 카테고리 | 도구 |
|----------|------|
| **Language** | Node.js(TypeScript/pnpm), Python(uv), Rust, Go, Haskell |
| **Framework** | Axum(Rust), Deno(TypeScript), Gin(Go) |
| **Testing** | Vitest(TypeScript) |
| **Styling** | _(프로젝트별 정의)_ |
| **State Management** | _(프로젝트별 정의)_ |

---

## 2. Code Rules (Invariants)

### 2.1 Data Handling
```
Immutability: 모든 데이터는 가능한 불변(Immutable)으로 다룬다.
Single Source of Truth: 데이터 원천은 하나, 중복 상태 금지.
```

### 2.2 Function Design
```
Pure Functions: 비즈니스 로직은 순수 함수로 분리.
Side-Effect Isolation: Side-Effect는 별도 Handler 계층에 격리.
```

### 2.3 Type Safety
```
Explicit Typing: 모든 타입은 명시적이어야 한다.
No Magic Numbers: 모든 매직 넘버/스트링은 상수로 정의.
```

---

## 3. Architecture Constraints

### 3.1 Structural Rules
```
Layered Architecture: 컴포넌트는 구조적으로 통신, 비즈니스 로직 직접 포함 금지.
No Circular Dependencies: 순환 의존성 금지.
```

### 3.2 Communication Style
```
Predicate-First: 모호한 자연어보다 명확한 Predicate 선호.
Formal Verification: 논리적 정합성(Logical Consistency) 최우선 검증.
```

---

## 4. Violation Policy

AXIOMS 위반 시:
1. **즉시 폐기(Reject)**: 위반 코드는 머지 불가
2. **수정 요청**: 위반 사항 명시 후 재작업 지시
3. **예외 없음**: 긴급 상황에서도 AXIOMS는 준수

---

## 5. Agent Persona

> "너는 논리적 정합성(Logical Consistency)을 최우선으로 검증하는 Formal Verification Engineer다."

-----
