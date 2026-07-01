# 🎯 SSoT: Single Source of Truth

> 모든 데이터를 하나의 기준으로 통합해, 동일한 정보 위에서 판단할 수 있게 만드는 구조

---

## 4대 속성

```mermaid
flowchart TB
    ssot["SSoT<br/>단일 진실 공급원"]

    ssot --> c1["Centralization<br/>분산 데이터를 단일 플랫폼에 통합"]
    ssot --> c2["Consistency<br/>수정이 전체에 동시 반영"]
    ssot --> c3["Integrity<br/>언제든 동일한 기준으로 접근"]
    ssot --> c4["Accurate Decision<br/>의사결정 속도·정확도 동시 상승"]

    style ssot fill:#5c1a5c,stroke:#a855f7,stroke-width:4px
    style c1 fill:#1a3a5c,stroke:#00d4ff
    style c2 fill:#3a5c1a,stroke:#ffd93d
    style c3 fill:#5c3a1a,stroke:#ff8c00
    style c4 fill:#5c1a3a,stroke:#ff6b9d
```

---

## 데이터 계층이 SSoT 중심인 이유

> 결과 지표(매출·생산성)만으로는 "무엇이 일어났는지"만 알려줌
> **맥락(구조·관계·역사)** 이 있어야 "왜"를 알 수 있다

| 데이터 종류 | 보여주는 것 | 못 보여주는 것 |
|---|---|---|
| 정량 지표 | 결과 | 원인 |
| 메타데이터 | 맥락·관계 | 정량 수치 |
| **SSoT (계층 통합)** | **원인-결과 통합** | — |

<div class="small">

⚠️ **협업툴≠SSoT 함정**: Notion·Slack·Docs는 이벤트 로그만 남기고 계층 맥락이 없음 → 판단 근거로 작동 못함

</div>

---

# 🗂 Wiki Super Repo

```mermaid
graph TD
    super["hermes-wiki-super<br/>(super repo)"]

    super --> w1["hermes-wiki<br/>(Index + 운영)"]
    super --> w2["hermes-wiki-claude-code"]
    super --> w3["hermes-wiki-codex"]
    super --> w4["hermes-wiki-schedule"]
    super --> w5["hermes-wiki-portfolio"]
    super --> w6["hermes-slash-commands"]
    super --> w7["hermes-logs<br/>(변경 이력)"]

    w1 --> a1["architecture/"]
    w1 --> a2["analysis/"]
    w1 --> a3["infra/"]
    w1 --> a4["watchlist/"]

    style super fill:#5c1a5c,stroke:#a855f7,stroke-width:4px
    style w1 fill:#1a3a5c,stroke:#00d4ff
    style w7 fill:#5c1a3a,stroke:#ff6b9d
```

<div class="small">

**SSoT 원칙 적용**: `hermes-wiki`가 index 역할, submodules가 도메인 데이터 담당

</div>