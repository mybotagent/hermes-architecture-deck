# ⚡ Hermes 시스템 해부

## 챗봇에서 **직원**으로

<sub>Architecture Deck v1 · 2026-07-01</sub>

Note:
환영합니다. 이 슬라이드는 Hermes Agent 시스템의 아키텍처를 풀어냅니다.
위키(mybotagent/hermes-wiki)의 architecture/, analysis/, infra/ 페이지를 시각화한 결과물입니다.

---

## TL;DR

<div class="tldr">

**3가지 핵심**

- 🧠 **두뇌 + 인격 + 기억** = 헤르메스의 7가지 부품 (챗봇엔 없는 장기)
- ⚙️ **12 업무 × 3원칙** = 비용제로 + 최고성능 + 데이터 무오염
- 🔄 **자동화 루프** = 매일 23:30 CST 분석 → 매월 5일 검증

**숫자 요약**: 7부품 · 12업무 · 9크론 · 28슬라이드 · 10다이어그램

</div>

---

## 📑 목차

| # | 섹션 | 슬라이드 |
|:-:|---|:-:|
| S0 | Hero | 0.1 ~ 0.3 |
| **S1** | **Hermes vs 챗봇** | 1.1 ~ 1.4 |
| **S2** | **Hybrid AI Stack** | 2.1 ~ 2.4 |
| **S3** | **Pipeline System** | 3.1 ~ 3.3 |
| **S4** | **LangGraph 5단계** | 4.1 ~ 4.3 |
| **S5** | **Cron Jobs** | 5.1 ~ 5.3 |
| **S6** | **SSoT + Wiki** | 6.1 ~ 6.3 |
| **S7** | **Outro** | 7.1 ~ 7.3 |

**키보드**: `←` `→` 이동 · `ESC` overview · `F` 풀스크린