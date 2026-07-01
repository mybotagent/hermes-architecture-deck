# Hermes Architecture Deck — DESIGN.md

> **wiki → GitHub Pages 슬라이드 (Reveal.js + mermaid + 키보드 네비)**

| 항목 | 값 |
|---|---|
| **목적** | Hermes 시스템 아키텍처를 mermaid 다이어그램 위주 슬라이드로 시각화 |
| **대상** | 본인 복습 + 외부 공유 (FastCampus 강좌 스타일) |
| **GitHub** | `mybotagent/hermes-architecture-deck` (public, GitHub Pages 호스팅) |
| **최종 URL** | `https://mybotagent.github.io/hermes-architecture-deck/` |
| **상태** | 🚧 DESIGN 단계 (구현 전) |

---

## 1. 목표 & 비목표

### ✅ 목표
- Hermes 시스템 7부품 / Hybrid AI Stack / Pipeline / SSoT / Wiki 구조를 mermaid 다이어그램과 함께 강의 슬라이드로 변환
- GitHub Pages에 자동 배포 (wiki push → 슬라이드 갱신)
- 키보드 좌우(←→) 네비게이션, 풀스크린, 발표자 노트(보너스)
- wiki 콘텐츠를 단일 진실 공급원(SSoT)으로 — 위키 수정 시 슬라이드 자동 반영

### ❌ 비목표
- 동영상 렌더링 (Remotion 별도 검토 — 본 스코프 아님)
- LMS 기능 (퀴즈, 진도 추적)
- 멀티 유저/인증
- 모바일 최적화 (우선 데스크탑 키보드 UX)

---

## 2. 타겟 사용자

| 그룹 | 사용 시나리오 |
|---|---|
| **본인 (1차)** | 시스템 복습, 새 기능 추가 시 구조 점검 |
| **외부 개발자/학습자 (2차)** | Hermes가 어떤 시스템인지 빠르게 이해 |
| **강의/블로그 첨부 (3차)** | URL 공유만으로 시각적 설명 |

---

## 3. 기술 스택 결정

| 영역 | 선택 | 이유 |
|---|---|---|
| **슬라이드 엔진** | **Reveal.js 5.x** | 사실 표준, 마크다운 직접 지원, 키보드 내장, GitHub Pages 정적 배포 용이 |
| **다이어그램** | **mermaid.js 10.x (CDN)** | 위키에서 작성한 mermaid 그대로 재사용, Reveal.js mermaid 플러그인 |
| **테마** | Reveal 기본 `black` + 커스텀 오버레이 | 가독성 우선, 브랜드 색 강조 |
| **빌드 도구** | **없음 (직접 HTML 편집)** | 위키 md → 슬라이드 변환은 Python 스크립트 1회성 |
| **호스팅** | **GitHub Pages** | 무료 HTTPS, 자동 배포, 커스텀 도메인 가능 |
| **CI/CD** | GitHub Actions | wiki repo push → 슬라이드 빌드 → Pages 배포 |

### 왜 Reveal.js 인가?
- Slidev 대비 단순함 (Vue 의존 X)
- Custom HTML 대비 검증됨 (10+년 표준)
- mermaid 플러그인 공식 지원

---

## 4. 사이트 구조

### 디렉토리 레이아웃
```
hermes-architecture-deck/                  # GitHub repo
├── index.html                            # Reveal.js 진입점
├── slides/                               # 섹션별 슬라이드
│   ├── 00-hero.md
│   ├── 01-hermes-vs-chatbot.md
│   ├── 02-7-components.md
│   ├── 03-skill-compound.md
│   ├── 04-hybrid-stack.md
│   ├── 05-pipeline-timeline.md
│   ├── 06-langgraph-flow.md
│   ├── 07-cron-schedule.md
│   ├── 08-ssot.md
│   ├── 09-wiki-super.md
│   └── 99-outro.md
├── assets/
│   ├── css/custom.css                    # 브랜드 색, 폰트 오버레이
│   └── img/                              # 다이어그램 export (PNG fallback)
├── scripts/
│   └── build_slides.py                   # wiki md → 슬라이드 md 변환기
├── .github/workflows/
│   └── pages.yml                         # GitHub Actions: 빌드 + 배포
├── README.md
├── DESIGN.md                             # 이 문서
└── CNAME                                 # (선택) 커스텀 도메인
```

### 진입 흐름
```
사용자 브라우저
  → https://mybotagent.github.io/hermes-architecture-deck/
    → index.html (Reveal.js)
      → 10개 섹션, ~28 슬라이드
        → ← → 키보드 네비
```

---

## 5. 슬라이드 구성 (28장)

### Section 0: Hero (3장)
| # | 제목 | 핵심 메시지 | mermaid |
|:-:|---|---|:-:|
| 0.1 | Title | "Hermes 시스템 해부 — 챗봇에서 직원으로" | — |
| 0.2 | TL;DR | 7부품 + 5단계 + 4속성 + 9크론 | — |
| 0.3 | 목차 | 8개 섹션 네비 | — |

### Section 1: Hermes vs 챗봇 (4장)
| # | 제목 | 핵심 | mermaid |
|:-:|---|---|:-:|
| 1.1 | 챗봇의 한계 | 매 세션 태초 마을 | — |
| 1.2 | **7가지 부품 다이어그램** | 두뇌·인격·기억·매뉴얼·손발·채널·알람 | ✅ |
| 1.3 | 기억의 두 층위 | 수첩(2KB) + 벡터 검색 | ✅ |
| 1.4 | **Skill 복리 순환** | 시행착오→매뉴얼→빠름→더 많은 경험 | ✅ |

### Section 2: Hybrid AI Stack (4장)
| # | 제목 | 핵심 | mermaid |
|:-:|---|---|:-:|
| 2.1 | 3대 원칙 | 비용 제로 + 최고 성능 + 데이터 오염 방지 | — |
| 2.2 | **12 업무 매핑 매트릭스** | 콘텐츠/개발/보안/지식 4분류 | ✅ |
| 2.3 | 로컬 vs 클라우드 결정 트리 | 민감도 기반 분기 | ✅ |
| 2.4 | 도구 생태계 | Ollama·Hermes·Obsidian·Notion·Canva·Higgsfield | — |

### Section 3: Pipeline System (3장)
| # | 제목 | 핵심 | mermaid |
|:-:|---|---|:-:|
| 3.1 | 매일 23:30 CST 자동 실행 | 24종목 → 포트폴리오 → Discord | — |
| 3.2 | **시간표 타임라인 (Gantt)** | 06:30 / 07:00 / 18:30 / 19:00 / 23:30 | ✅ |
| 3.3 | 데이터 저장 구조 | captured → filtered → decisions → portfolio | ✅ |

### Section 4: LangGraph 5단계 (3장)
| # | 제목 | 핵심 | mermaid |
|:-:|---|---|:-:|
| 4.1 | Bull/Bear/Risk → Decision | 9종목 × 5 calls = 45 calls | — |
| 4.2 | **5단계 플로우차트** | Context → Bull → Bear → Risk → Decision | ✅ |
| 4.3 | 비용 ($0.054/회) | DeepSeek 기반 합리적 비용 | — |

### Section 5: Cron Jobs (3장)
| # | 제목 | 핵심 | mermaid |
|:-:|---|---|:-:|
| 5.1 | 9개 크론 + deliver 패턴 | origin 권장, 위험 패턴 회피 | — |
| 5.2 | **KST 타임라인 (24h)** | 평일/월말/매주 | ✅ |
| 5.3 | Self-Healing Watchdog | 404 → 자동 origin patch | — |

### Section 6: SSoT + Wiki (3장)
| # | 제목 | 핵심 | mermaid |
|:-:|---|---|:-:|
| 6.1 | **SSoT 4대 속성** | Centralization/Consistency/Integrity/Decision | ✅ |
| 6.2 | HR 데이터가 SSoT 중심인 이유 | 원인 = HR, 결과 = 매출 | — |
| 6.3 | **Wiki Super Repo 트리** | hermes-wiki + 7 submodules | ✅ |

### Section 7: Outro (3장)
| # | 제목 | 핵심 | mermaid |
|:-:|---|---|:-:|
| 7.1 | 시스템 = 두뇌 + 인격 + 기억 | 재학습 비용 Zero | — |
| 7.2 | 다음 단계 | 위키 → 슬라이드 자동 파이프라인 확장 | — |
| 7.3 | Q&A + 링크 | github repo URL, 위키 URL | — |

**총 28장, mermaid 다이어그램 10개**

---

## 6. Mermaid 다이어그램 10개 목록

| ID | 이름 | 타입 | 원본 wiki |
|:-:|---|---|---|
| D1 | 7가지 부품 | `flowchart` | architecture/hermes-vs-chatbot |
| D2 | 기억 두 층위 | `flowchart LR` | architecture/hermes-vs-chatbot |
| D3 | Skill 복리 순환 | `flowchart LR` (loop) | architecture/hermes-vs-chatbot |
| D4 | 12 업무 매핑 | `quadrantChart` 또는 table | architecture/hybrid-ai-stack |
| D5 | 로컬/클라우드 결정 트리 | `flowchart TD` | architecture/hybrid-ai-stack |
| D6 | Pipeline 시간표 | `gantt` | analysis/pipeline-system-overview |
| D7 | 데이터 저장 흐름 | `flowchart LR` | analysis/pipeline-system-overview |
| D8 | LangGraph 5단계 | `flowchart LR` | analysis/langgraph-pipeline |
| D9 | Cron KST 타임라인 | `gantt` | infra/cron-jobs |
| D10 | Wiki Super 트리 | `graph TD` | repos/hermes-wiki-super |

---

## 7. 위키 → 슬라이드 변환 파이프라인

### 원리
wiki md 파일의 mermaid 블록 + 핵심 문단을 추출 → 슬라이드 마크다운으로 emit

### 입력
- `~/.hermes/wiki/architecture/*.md`
- `~/.hermes/wiki/analysis/pipeline-system-overview.md`
- `~/.hermes/wiki/analysis/langgraph-pipeline.md`
- `~/.hermes/wiki/infra/cron-jobs.md`
- `~/.hermes/wiki/repos/hermes-wiki-super.md`

### 출력
- `slides/XX-name.md` (Reveal.js 호환)

### 변환 규칙 (Python `build_slides.py`)
1. YAML frontmatter 무시 (제목만 추출)
2. `##` 헤딩 → 슬라이드 분리점
3. ```mermaid 블록 → 그대로 보존 (Reveal.js mermaid 플러그인이 렌더)
4. 표는 그대로, 너무 크면 핵심 행만 발췌
5. 위키 링크 `[[...]]` → 제거 (슬라이드는 standalone)

### 실행
```bash
python3 scripts/build_slides.py \
  --wiki ~/.hermes/wiki \
  --out slides/
```

---

## 8. GitHub Actions 자동 배포

### workflow: `.github/workflows/pages.yml`
```yaml
name: Build & Deploy Slides
on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Python
        uses: actions/setup-python@v5
        with: { python-version: '3.11' }
      - name: Build slides from wiki (optional sync)
        run: python3 scripts/build_slides.py
      - name: Deploy to Pages
        uses: actions/deploy-pages@v4
        with:
          artifact_name: github-pages
```

### wiki 동기화 옵션 (Phase 2)
- **Option A**: hermes-wiki push → webhook → 이 repo API 트리거
- **Option B**: 이 repo Actions에서 cron으로 매주 wiki pull → 빌드
- **초기**: Option B (단순함) — 매주 일요일 04:00 KST

---

## 9. Phase 분할 (구현 순서)

| Phase | 범위 | 산출물 | 의존성 |
|:-:|---|---|---|
| **P1** | Repo 골격 + Hero 3장 | GitHub repo, index.html, 00-hero | — |
| **P2** | Section 1 (Hermes vs 챗봇 4장) + D1~D3 mermaid | 01~04 슬라이드 | P1 |
| **P3** | Section 2 (Hybrid AI Stack 4장) + D4~D5 | 05~08 슬라이드 | P2 |
| **P4** | Section 3+4 (Pipeline+LangGraph 6장) + D6~D8 | 09~14 슬라이드 | P3 |
| **P5** | Section 5+6 (Cron+SSoT 6장) + D9~D10 | 15~20 슬라이드 | P4 |
| **P6** | Outro 3장 + 커스텀 CSS + 키보드 단축키 | 21~23 슬라이드 | P5 |
| **P7** | GitHub Actions + Pages 활성화 + 첫 배포 | 공개 URL | P6 |
| **P8** | Wiki 자동 동기화 (Phase 2) | webhook 또는 cron | P7 |

각 Phase 끝나면 Discord 스레드에 진행 상황 보고.

---

## 10. Linear 이슈 매핑

| Linear 티켓 | Phase | 제목 |
|---|---|---|
| HAD-1 | P1 | Repo 골격 + Reveal.js 진입점 |
| HAD-2 | P2 | Hermes vs 챗봇 섹션 (4장) |
| HAD-3 | P3 | Hybrid AI Stack 섹션 (4장) |
| HAD-4 | P4 | Pipeline + LangGraph 섹션 (6장) |
| HAD-5 | P5 | Cron + SSoT 섹션 (6장) |
| HAD-6 | P6 | Outro + 커스텀 스타일링 |
| HAD-7 | P7 | GitHub Pages 배포 + 자동화 |
| HAD-8 | P8 | Wiki 자동 동기화 파이프라인 |

각 Phase가 끝날 때마다 Linear 이슈 상태 업데이트.

---

## 11. 위험 & 제약

| 위험 | 영향 | 완화 |
|---|---|---|
| mermaid CDN 의존 (오프라인 불가) | 낮음 | GitHub Pages 자체가 인터넷 필요, 인지하고 진행 |
| Reveal.js + mermaid 플러그인 호환성 | 중간 | 공식 플러그인 사용, fallback PNG export 가능 |
| 위키 구조 변경 시 슬라이드 깨짐 | 중간 | build_slides.py가 빌드 시 lint, 깨진 섹션 경고 |
| GitHub Pages public repo 필요 | 낮음 | 위키는 private지만 슬라이드는 public OK |
| mermaid `gantt` 문법 까다로움 | 낮음 | D6/D9는 P5에서 신중히 작성 |

---

## 12. 가치 검증

- **본인**: 시스템 한눈에 복습 가능 (5분)
- **외부**: Hermes를 30분 강의로 설명 가능
- **자산화**: 위키 ↔ 슬라이드 양방향 (Phase 8)
- **확장성**: 다른 시리즈 (가치투자, 솔로프레너)도 같은 템플릿 재사용

**결론**: MVP(P1~P7)만으로도 가치 충분. P8(자동 동기화)는 nice-to-have.

---

## 13. 다음 액션

1. ✅ DESIGN.md 사용자 검토 (지금)
2. ⏸ 승인 시 → Linear 이슈 HAD-1~8 일괄 생성
3. ⏸ GitHub repo `mybotagent/hermes-architecture-deck` 생성 (public, Pages 활성화)
4. ⏸ P1 시작 (index.html + Hero 3장)

---

*작성: 2026-07-01 / Hermes Agent / DESIGN 단계*