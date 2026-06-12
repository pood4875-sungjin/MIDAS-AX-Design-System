# PRD — MIDAS AX Design System (Intro Site)

> AX (Agent eXperience) 인터페이스를 짓기 위한 디자인 시스템 소개 사이트.
> 동시에, **"시안 → AI 추출 → 시스템·사이트 동반 진화"** 워크플로우를 검증한 케이스 스터디.

---

## 0. 메타

| | |
|---|---|
| **작성자** | 김성진 |
| **상태** | v1.0 · 회고형 PRD (구축 완료 후 정리) |
| **작성일** | 2026-06-12 |
| **프로젝트 기간** | 1일 (구축) + 추가 다듬기 (진행 중) |
| **Repo** | https://github.com/pood4875-sungjin/MIDAS-AX-Design-System |
| **Live** | https://pood4875-sungjin.github.io/MIDAS-AX-Design-System/ |
| **Stack** | Pure HTML / CSS / JS · Figma · Claude Code · MCP |

---

## 1. 요약 (Executive Summary)

MIDAS 의 AX 인터페이스 컨벤션을 정리한 디자인 시스템과, 그 시스템을 **AI 와 함께 만들고 발전시키는 새로운 작업 방식**을 동시에 검증한 프로젝트.

기존엔 디자인 시스템을 먼저 정의하고 → 화면을 만드는 단방향 흐름이었지만, 이번에는 **좋은 시안을 먼저 만들고 → Claude Code 가 시스템을 추출하고 → 시스템·사이트를 동반 발전**시키는 방향을 시도. 그 결과 디자인 시스템 셋업 시간이 4일 → 4시간으로 **약 8배 단축**되었으며, 같은 시스템에서 6가지 시각적으로 다른 화면(Sandbox A~F)을 생성해 시스템 유연성도 검증했다.

부수적으로 도달한 결론: **디자인 시스템은 AI 에게 "설계도" 역할을 한다.** 이 통찰을 케이스 스터디 페이지(`/process3/`)와 발표 덱(22 슬라이드) 으로 정리했다.

---

## 2. 배경 & 문제 정의

### 2.1 배경

디자인 시스템과 화면은 서로가 서로를 필요로 한다. **시스템이 있어야 화면을 만들기 쉽고, 화면을 만들어야 어떤 시스템이 필요한지 알 수 있다.** 그래서 대부분의 프로젝트에서는 두 작업이 병렬로 진행된다.

하지만 화면이 구체화될수록 **시스템·디자인·개발 모두 반복적으로 수정**되는 일이 발생한다. 익숙하지만 늘 비효율적이라고 느껴왔다.

### 2.2 문제 정의

1. **단방향 워크플로우의 한계** — "시스템 정의 → 화면 설계" 순서는 책에선 깔끔하지만, 현실에선 끝없는 수정 반복.
2. **AI 협업 시 정보 손실** — Figma 시안 → 코드로 옮기는 과정에서 디자인 의도가 살아남지 못함. 디자인 시스템이 "정리되지 않은 데이터" 라 AI 가 추측에 의존.
3. **시스템 도큐먼테이션의 무게** — 토큰·컴포넌트·페이지 가이드 문서를 사람이 일일이 작성하는 비용. 변경이 잦으면 문서가 따라가지 못함.

### 2.3 질문

> - 굳이 처음부터 디자인 시스템을 정의할 필요가 있을까?
> - 좋은 시안을 먼저 만들고, AI 가 거기서 디자인 시스템을 추출하면 어떨까?
> - 시안이 바뀌면 시스템도 같이 업데이트되면 어떨까?

---

## 3. 목표 / 비목표

### 3.1 목표 (Goals)

| # | 목표 | 검증 방법 |
|---|---|---|
| G1 | **Claude Code 로 실제 사이트를 구축할 수 있는가** | Figma 시안만으로 디자이너가 직접 다중 페이지 사이트 구축 |
| G2 | **시안만으로 디자인 시스템을 생성할 수 있는가** | 토큰을 하나씩 정의하지 않고 시안에서 자동 추출 |
| G3 | **생성된 시스템은 실제로 활용 가능한가** | 추가 화면(Sandbox 6안)·재사용성·확장성 검증 |
| G4 | **새 워크플로우의 정량적 가치 증명** | 시스템 셋업 시간 단축율, 일치율 비교 |

### 3.2 비목표 (Non-goals)

- 모바일 레이아웃 (데스크탑 전용)
- 다국어 (한국어/영문 혼용만)
- 인증·서버·DB (정적 사이트)
- 새 디자인 토큰 체계 발명 (기존 MIDAS 컨벤션 활용)
- 풀 e2e 테스트 자동화

---

## 4. 사용자 / 페르소나

| 페르소나 | 니즈 | 주요 사용 페이지 |
|---|---|---|
| **AX 인터페이스 디자이너** | 컴포넌트·패턴·토큰을 빠르게 참조하고 싶다 | `/foundation/` · `/components/` · `/pattern/` |
| **AX 개발자** | 컴포넌트의 시각·인터랙션 명세를 코드에서 그대로 쓰고 싶다 | `/system/components.html` · `/system/audit.html` |
| **디자인 시스템 운영자** | 시스템의 일관성·커버리지를 점검하고 싶다 | `/system/audit.html` · `/system/foundation.html` |
| **잠재적 사용자 / 발표 청중** | "왜 AI 시대에 디자인 시스템이 중요한가" 를 이해하고 싶다 | `/process3/` (케이스 스터디) |

---

## 5. 사용 시나리오

1. **컴포넌트 빠른 참조** — GNB → Components → 원하는 카테고리(Inputs 등) → 컴포넌트 상세 상태 확인.
2. **토큰 일관성 점검** — Audit 페이지에서 토큰 커버리지(어떤 페이지가 어떤 토큰을 쓰는지) 한눈에.
3. **새 패턴 학습** — Pattern 페이지에서 Agentic UI · Embedded UI · Automation UI 의 예시를 참조.
4. **시스템 유연성 검증** — Sandbox 6안(System A·B·C / Free D·E·F) 갤러리에서 같은 시스템으로 다른 룩이 가능한지 확인.
5. **케이스 스터디 공유** — Footer/Hero 의 process3 링크로 "어떻게 구축했는가" 와 인사이트 공유.

---

## 6. 범위 (In Scope / Out of Scope)

### 6.1 In Scope (v1.0)

- ✅ 메인 페이지 (Hero + Pattern 3-up + FAQ)
- ✅ Foundation 페이지 (Color Scheme · Dimension · Text · Effect)
- ✅ Components 카탈로그 (12 컴포넌트: Actions / Inputs / Chat / Surface / Feedback)
- ✅ Pattern 페이지 (Agentic UI · Embedded UI · Automation UI)
- ✅ System 자체 문서 (`/system/`: foundation · layout · components · audit)
- ✅ Sandbox 6안 (System A·B·C + Free D·E·F)
- ✅ 케이스 스터디 (`/process3/`) + 인사이트 통합 섹션
- ✅ GNB · SNB · TOC · Footer · Page Grid
- ✅ 다크 모드 (`tokens.css` light/dark 모두 정의)
- ✅ 검색 (페이지 전체 콘텐츠 인덱싱)
- ✅ GitHub Pages 배포

### 6.2 Out of Scope (v1.0)

- ❌ 모바일/태블릿 반응형
- ❌ 다국어 i18n
- ❌ 인증/사용자별 페이지
- ❌ 컴포넌트 동작 데모(런타임 상태)
- ❌ React/Vue 컴포넌트 라이브러리 (HTML/CSS 만)
- ❌ Figma 플러그인 / 토큰 자동 sync

### 6.3 향후 고려 (v1.1+)

- 🔜 Foundation · Components 페이지 디테일 보강 (Pattern Overview 구조 적용)
- 🔜 onsite-system 패턴 흡수 (두 번째 적용 사례)
- 🔜 컴포넌트별 코드 스니펫 복사 버튼

---

## 7. 기능 요구사항 (Functional Requirements)

### 7.1 페이지 / 정보 구조

| ID | 요구사항 | 상태 |
|---|---|---|
| F-01 | 메인 페이지에 Hero · Pattern 3-up · FAQ 노출 | ✅ |
| F-02 | Foundation 4 카테고리 (Color / Dimension / Text / Effect) 페이지 | ⏳ 디테일 보강 중 |
| F-03 | Components 12 종 페이지 (5 카테고리 × N) | ⏳ 디테일 보강 중 |
| F-04 | Pattern 3 카테고리 (Agentic / Embedded / Automation) 페이지 | ✅ |
| F-05 | System 자체 문서 4 페이지 (foundation/layout/components/audit) | ✅ |
| F-06 | Sandbox 6안 (A~F) + 비교 갤러리 | ✅ |
| F-07 | 케이스 스터디 페이지 (`/process3/`) | ✅ |

### 7.2 레이아웃 / 내비

| ID | 요구사항 | 상태 |
|---|---|---|
| F-10 | GNB 72px · blur 16 · bg 88% · top sticky | ✅ |
| F-11 | SNB 180px · sticky top+56 · 4-state hover/active | ✅ |
| F-12 | TOC 160px · smooth scroll + scroll-spy active 표시 | ✅ |
| F-13 | Footer margin-top 200 + badge | ✅ |
| F-14 | Page Grid (`--no-toc`, `--full` variant) | ✅ |
| F-15 | Section 간 160px 패딩 (margin collapse 방지) | ✅ |

### 7.3 컴포넌트

| ID | 요구사항 | 상태 |
|---|---|---|
| F-20 | Buttons 3 sizes (LG/MD/SM) — `.btn-pill`, `.btn-pill--md/sm`, `.btn-text` | ✅ |
| F-21 | Card 패밀리 — `.card-grid`, `.p-card`, `.gallery-card` | ✅ |
| F-22 | FAQ — 인라인 SVG 토글 + currentColor + 45° 회전 | ✅ |
| F-23 | Hero — char-by-char wave 애니메이션 | ✅ |
| F-24 | 페이지 그라데이션 (top: Figma 50:27838 · bottom: 111:4832) | ✅ |

### 7.4 검색·인터랙션

| ID | 요구사항 | 상태 |
|---|---|---|
| F-30 | 페이지 전체 콘텐츠 검색 (정적 인덱스: `scripts/build-search-index.js`) | ✅ |
| F-31 | 다크 모드 토글 + localStorage 저장 | ✅ |
| F-32 | 키보드 접근성 (포커스 / 키보드 내비) | ✅ |

---

## 8. 비기능 요구사항 (Non-functional)

| 분류 | 요구사항 | 결정 |
|---|---|---|
| **빌드** | 빌드 도구 없음 (Pure HTML/CSS/JS) | ✅ |
| **배포** | GitHub Pages 자동 배포 | ✅ |
| **로컬** | `file://` 환경에서도 동작 (모든 경로 상대경로) | ✅ |
| **로딩** | CDN 폰트 (Pretendard) · 정적 자산 / 외부 의존 최소 | ✅ |
| **다크모드** | tokens.css 에서 light/dark 동시 정의 (`--color-*` 매핑 표 참조) | ✅ |
| **접근성** | 키보드 내비 / 포커스 가시화 / 대비 AA 이상 | ✅ |
| **호환성** | 데스크탑 모던 브라우저 (Chrome / Safari / Edge 최신 2 버전) | ✅ |
| **확장성** | 컴포넌트 추가 시 `system/components.html` 한 곳에 명세 추가 → 모든 페이지 일관 | ✅ |

---

## 9. 성공 지표 (Success Metrics)

### 9.1 정량

| 지표 | 목표 | 결과 |
|---|---|---|
| 디자인 시스템 셋업 시간 | < 1일 | **4시간 (목표 초과 달성)** — 기존 4일 대비 **8× 단축** |
| 시안 → 시스템 추출 자동화율 | > 70% | **약 80%** (Color · Typography · Spacing · Radius · Motion · Component 구조 자동) — Hover/Active/Disabled/Focus 같은 상태는 추가 작업 필요 |
| 같은 시스템으로 시각언어 다른 화면 생성 | 3안 이상 | **6안 (System A·B·C + Free D·E·F)** |
| 페이지 수 | ≥ 8 페이지 | **15+ 페이지** (foundation/components/pattern/system × 4·sandbox × 6·process) |

### 9.2 정성

- ✅ **디자이너 단독으로 사이트 구축 가능** (개발자 핸드오프 없이 1일 안에 라이브)
- ✅ **시스템과 사이트 동반 진화 패턴 확인** — 단방향이 아닌 순환 흐름이 실제로 더 자연스러움
- ✅ **AI 가 디자인 의도를 그대로 옮기는 조건 식별** — "디자인 시스템 = AI 의 설계도" 라는 결론 도출

---

## 10. 일정 / 마일스톤

| 단계 | 기간 | 결과물 |
|---|---|---|
| **M1** Figma 시안 제작 | (사전) | 디자인 시스템 사이트 시안 |
| **M2** Claude + MCP 연결 | ~1h | MCP 통해 Figma 노드 직접 읽기 |
| **M3** 디자인 시스템 생성 | ~1h | Color/Typography/Spacing/Radius/Motion 토큰 + Semantic 구조 자동 추출 |
| **M4** 시스템 고도화 | ~1h | 버튼 상태·카드 패턴·레이아웃 규칙·예외 케이스 보완 |
| **M5** 페이지 구축 | ~4h | Main · Foundation · Components · Layout · Pattern · Audit · Sandbox 페이지 |
| **M6** 베리에이션 테스트 | ~1h | Sandbox 6안 (System A·B·C + Free D·E·F) |
| **M7** 케이스 스터디 정리 | (이후) | `/process2/` → `/process3/` 통합 + 인사이트 섹션 |
| **M8** 발표 덱 제작 | (이후) | 22장 풀버전 deck (`ppt-template/decks/midas-ax-process3.html`) |

**총 구축 시간: 약 1일.** 이후 디테일 보강·페이지 추가는 별도.

---

## 11. 리스크 / 가정

### 11.1 리스크

| 리스크 | 영향 | 완화 방안 |
|---|---|---|
| **MCP 의존** — MCP 없으면 Claude 가 시안을 추측, 정확도 급락 | 高 | MCP 연결 상태를 워크플로우 첫 단계에 못박음. 연결 안 되면 작업 보류. |
| **AI 생성물의 검수 비용** | 中 | 작은 단위(토큰 → 컴포넌트 → 레이아웃 → 페이지)로 나눠 단계마다 검수 |
| **시스템과 시안의 sync drift** | 中 | 시안 변경 시 재추출 → 시스템 자동 갱신 패턴 채택 |
| **inverse 토큰 다크모드 뒤집힘** | 低 | Pricing Featured / CTA Banner 등 "항상 다크 강조" 영역은 고정 `#1B1C1E` 사용 |
| **Foundation/Components 페이지 작업 미완료** | 中 | v1.1 에서 Pattern Overview 구조로 보강 (현재 in_progress) |

### 11.2 가정

- 디자이너가 Figma 시안을 "잘" 정리해 둔다는 전제 (네이밍·Auto Layout·컴포넌트 변수)
- Claude Code 와 MCP 가 정상 연결되어 있음
- 사용자는 데스크탑 환경
- 모던 브라우저 사용

---

## 12. 의존성 / 산출물

### 12.1 외부 의존

- **Figma** — 디자인 시안 단일 출처(SoT)
- **Claude Code + MCP** — 시안 추출 / 코드 생성
- **GitHub Pages** — 배포
- **Pretendard (CDN)** — 한글 폰트

### 12.2 핵심 산출물

| 산출물 | 위치 |
|---|---|
| **메인 사이트** | https://pood4875-sungjin.github.io/MIDAS-AX-Design-System/ |
| **System 자체 문서** | `/system/` (foundation/layout/components/audit) |
| **Sandbox 6안** | `/sandbox/` |
| **케이스 스터디** | `/process3/` |
| **두 번째 적용 사례** | https://pood4875-sungjin.github.io/midas-onsite-system/ (WIP) |
| **발표 덱** | `~/ppt-template/decks/midas-ax-process3.html` (22장) |
| **PRD (이 문서)** | `PRD.md` |
| **토큰 명세 SoT** | `DESIGN-SYSTEM.md` |
| **개발 컨벤션** | `CLAUDE.md` |

---

## 13. 결과 회고 (Retrospective)

### 13.1 작업하며 발견한 3가지

1. **시스템은 다듬어가며 완성된다** — 시안으로 한 번에 추출할 수 있지만, 실제 페이지를 만들어가다 보면 빠진 규칙·새 패턴이 계속 발견된다.
2. **화면은 작은 단위부터 쌓아 올린다** — 페이지 전체를 한 번에 만들면 컴포넌트 해석 오차·간격 불일치 발생. 토큰 → 컴포넌트 → 레이아웃 → 페이지 순으로 차근차근.
3. **Claude 는 작은 단위에서 더 정확하다** — 큰 문제 한 번에 해결할 때보다 작은 단위로 나눠 해결할 때 훨씬 정확. 작은 단위부터 쌓는 방식이 원본 시안 일치율 가장 높았다.

### 13.2 결국 깨달은 핵심 — 왜 AI 구축에 디자인 시스템이 필요한가

**디자인 시스템 자체가 AI 에게 "설계도" 역할을 한다.** 세 가지 관점으로 정리:

| | 비유 | 메시지 |
|---|---|---|
| **01 계층** | 자재 4 단계 (콘크리트→공간→자재용도→건물 전체) | 디자인 시스템은 Compositions / Components / Semantic Tokens / Primitive Tokens 의 4층 구조 |
| **02 설계도** | 자재만 있음 ↔ 설계도와 함께 | Primitive 만으로는 AI 가 무엇을 만들지 모름. 설계도(시스템 전체) 가 필요 |
| **03 도면** | 평면도 + 마감 시방서 + 자재 명세서 | 설계도 안에는 HTML(구조) · CSS(스타일) · JSON(토큰 의미) 세 도면이 들어 있다 |

→ 잘 정리된 설계도가 있어야 AI 가 디자인 의도를 그대로 코드로 옮긴다.

### 13.3 향후 개선 방향

- Foundation · Components 디테일 보강 (in_progress)
- 컴포넌트 코드 스니펫 복사 인터랙션
- Figma → 토큰 자동 sync 파이프라인 (현재는 수동)
- onsite-system 패턴 흡수 / 양 사이트 공통화 가능 부분 식별

---

## 부록 A — 핵심 토큰 요약

전체는 `DESIGN-SYSTEM.md` 및 `css/tokens.css` 참조.

- **Layout**: `--container-max: 1400px` / `--snb-width: 180px` / `--gnb-height: 72px`
- **Color**: light/dark 동시 정의 — `--color-label-strong`, `--color-background`, `--color-inverse-background` 등 (전체 매핑 표는 `CLAUDE.md` 참조)
- **Typography**: `.t-h1` 28/1.33/600/-0.5px · `.t-h3` 22/1.08/600/-0.427px · `.t-body-sm` 15/1.47/500/0.144px
- **Spacing / Radius / Motion**: `--space-{2..8}` 8/12/16/24/40/60 · `--radius-{sm,md,lg}` 8/12/24 · `--duration-{fast,normal,slow}` 120/240/400ms

## 부록 B — 컨벤션·함정

전체는 `CLAUDE.md` 참조. 검증된 함정 6 가지:

1. inverse-bg 다크모드 뒤집힘 — 고정 hex 사용
2. Grid auto-flow 깨짐 — `grid-template-areas` 로 절대위치
3. SNB 스크롤바 위치 — `.snb__inner` 로 calc + margin-inline + padding-right 처리
4. Hero CTA 다중 버튼 — `display: flex; justify-content: center` 필수
5. section 간격 — `padding-top: 160px` (margin 아님)
6. 상대경로 사용 — file:// 호환

---

> **이 PRD 는 회고형(Retrospective PRD)** 입니다. 구축 완료 후 정리된 문서로, 새 기능·v1.1 변경 시 별도 PRD-amendment 또는 인라인 업데이트로 관리합니다.
