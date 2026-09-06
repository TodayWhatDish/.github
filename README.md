# 오늘 뭐멍냥

<br/>

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-vec-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

<br/>

개·고양이 사료·간식을 반려동물 프로필(축종/체급/알러지)에 맞춰 추천하는 RAG 기반 서비스입니다.
정형 필터(SQL)로 먼저 거르고, 그 후보 위에서만 LLM이 최종 추천을 고릅니다 — 토큰 낭비와 축종/알러지 오조합을 막기 위한 구조입니다.

## 저장소

| 저장소 | 역할 |
|---|---|
| [`dev-data-embed`](https://github.com/TodayWhatDish/dev-data-embed) | **백엔드.** 더미 데이터 파이프라인(CSV → SQLite → 임베딩)과 그 위에서 도는 FastAPI 서비스 |
| [`dev-web`](https://github.com/TodayWhatDish/dev-web) | **프론트엔드.** 관리자 대시보드 + 고객용 페이지. 정적 HTML/Vanilla JS, `dev-data-embed`의 FastAPI를 직접 호출 |

## 구조

```
dev-web (정적 JS, :3000)  --HTTP-->  dev-data-embed FastAPI (:8000)
                                          │
                                          ├─ pet_reco.db (SQLite + sqlite-vec)
                                          └─ LLM (LangChain: Anthropic / 로컬 Ollama)
```

`dev-web`은 자체 백엔드가 없습니다 — 모든 데이터는 `dev-data-embed`의 FastAPI가 원본입니다.

## 라이선스

`dev-data-embed`는 Apache-2.0, `dev-web`은 MIT — 각 저장소의 `LICENSE`를 따릅니다.
