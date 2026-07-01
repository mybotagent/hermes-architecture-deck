# ⚡ Hermes Architecture Deck

> Hermes 시스템 아키텍처를 mermaid 다이어그램과 함께 풀어내는 슬라이드 덱

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://mybotagent.github.io/hermes-architecture-deck/)
[![Reveal.js](https://img.shields.io/badge/Reveal.js-5.1-blue)](https://revealjs.com/)
[![mermaid](https://img.shields.io/badge/mermaid-10.9-ff3670)](https://mermaid.js.org/)

## 🎯 무엇인가?

위키(`mybotagent/hermes-wiki`)의 architecture/ + analysis/ + infra/ 페이지를 슬라이드로 변환한 결과물입니다.

- **28장 슬라이드** (8개 섹션)
- **10개 mermaid 다이어그램** (flowchart, gantt, quadrantChart)
- **키보드 네비**: ← → 슬라이드 이동, ↑↓ vertical 이동, ESC overview, F 풀스크린

## 🚀 빠른 시작

### 로컬에서 보기

```bash
git clone https://github.com/mybotagent/hermes-architecture-deck.git
cd hermes-architecture-deck
python3 -m http.server 8000
# → http://localhost:8000
```

### 온라인에서 보기

🌐 **https://mybotagent.github.io/hermes-architecture-deck/**

## ⌨️ 키보드 단축키

| 키 | 동작 |
|---|---|
| `←` `→` | 슬라이드 이동 |
| `↑` `↓` | Vertical 슬라이드 이동 |
| `Space` | 다음 슬라이드 |
| `ESC` | Overview 모드 |
| `F` | 풀스크린 |
| `S` | 발표자 노트 |
| `B` | 슬라이드 일시정지 (검은 화면) |

## 📚 슬라이드 구성

```
S0  Hero (3)              — 시스템 한눈에
S1  Hermes vs 챗봇 (4)    — 7부품 + 기억 + Skill 복리
S2  Hybrid AI Stack (4)   — 비용제로 + 최고성능 + 무오염
S3  Pipeline (3)          — 매일 23:30 CST 자동 분석
S4  LangGraph (3)         — Bull/Bear/Risk → Decision
S5  Cron Jobs (3)         — 9개 크론 + 셀프힐링
S6  SSoT + Wiki (3)       — 단일 진실 + 7 submodule
S7  Outro (3)             — 가치 + 다음 단계
```

## 🛠 기술 스택

- **[Reveal.js 5.1](https://revealjs.com/)** — 슬라이드 엔진
- **[mermaid.js 10.9](https://mermaid.js.org/)** — 다이어그램
- **GitHub Pages** — 정적 호스팅
- **GitHub Actions** — 자동 배포

## 🔗 관련 저장소

| 저장소 | 용도 |
|---|---|
| [mybotagent/hermes-wiki](https://github.com/mybotagent/hermes-wiki) | 원본 콘텐츠 (Karpathy LLM Wiki) |
| [mybotagent/hermes-wiki-super](https://github.com/mybotagent/hermes-wiki-super) | Wiki super repo (모든 submodule 통합) |
| [mybotagent/trade-pipeline](https://github.com/mybotagent/trade-pipeline) | LangGraph 파이프라인 코드 |

## 📜 라이선스

MIT License

## 🤖 빌드

이 슬라이드는 [Hermes Agent](https://github.com/mybotagent)로 자동 생성되었습니다.
원본: [`DESIGN.md`](./DESIGN.md)