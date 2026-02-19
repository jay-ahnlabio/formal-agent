# KNOWLEDGE v2 (Execution State & Change Log)

> 이 파일은 프로젝트의 **현재 진행 상황**과 **변경 이력**을 추적합니다.
> AI에 의해 상태 자동 업데이트 권장

---

## Update Rules

### Append-Only 원칙
```
✅ 허용: 새 항목 추가, 상태 표시 변경
❌ 금지: 기존 타임스탬프 수정, 완료 기록 삭제, 로그 내용 수정
```

### 상태 표기법

| 상태 | 표기 | 설명 |
|------|------|------|
| 미완료 | `[ ]` | 아직 진행 안 함 |
| 완료 | `[x]` | 정상 완료 |
| 롤백 | `[🔄]` | 완료 후 되돌림 |
| 취소 | `[⏹]` | 더 이상 진행 안 함 |
| 추가 | `(추가: HH:MM)` | 나중에 추가된 항목 |

### 타임스탬프 형식
```
완료 시: - [x] YYYY-MM-DD HH:MM | 작업 내용
롤백 시: - [🔄] YYYY-MM-DD HH:MM | 롤백 사유
```

---

## 1. Current Context

> 현재 작업 상태 요약

- **Last Action:** _(마지막 수행 작업)_
- **Current Focus:** _(현재 집중 영역)_
- **Blockers:** _(있다면 차단 요소)_

---

## 2. Active Tasks

> 현재 진행 중인 작업들

### [Task ID]: Task Name

**Phase:** `Analysis` | `Spec` | `Test` | `Implement` | `Verify`

#### Checklist
- [ ] 작업 항목 1
- [ ] 작업 항목 2
- [ ] 작업 항목 3

#### Log (최신순)
```
YYYY-MM-DD HH:MM - 작업 내용
```

---

## 3. Completed (DONE)

> 검증 완료된 작업들 (Facts)

### YYYY-MM-DD

- [x] YYYY-MM-DD HH:MM | 완료된 작업 1
- [x] YYYY-MM-DD HH:MM | 완료된 작업 2

---

## 4. Backlog (TODO)

> 해결해야 할 목표들

### Priority: High
- [ ] 높은 우선순위 작업 1

### Priority: Medium
- [ ] 중간 우선순위 작업 1

### Priority: Low
- [ ] 낮은 우선순위 작업 1

---

## 5. Change Log Template

> 복잡한 작업의 상세 이력 기록용

```markdown
## [Issue/PR Number]: 작업명

### Summary
- 변경 목적:
- 영향 범위:

### Timeline
| 시각 | 상태 | 내용 |
|------|------|------|
| HH:MM | 시작 | 작업 시작 |
| HH:MM | 완료 | Phase 1 완료 |
| HH:MM | 롤백 | 사유: ... |
| HH:MM | 완료 | 최종 완료 |

### Files Changed
- `path/to/file1.ts` - 변경 내용 요약
- `path/to/file2.ts` - 변경 내용 요약

### Notes
- 특이사항이나 향후 참고 사항
```

-----
