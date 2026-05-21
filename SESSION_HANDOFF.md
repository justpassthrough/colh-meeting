# ColH 미팅 발표 — Session Handoff (2026-05-21 → 내일)

## 📁 작업 위치

```
C:\Users\Andy\OneDrive\Desktop\Fire\de_novo\Claude_code_output\colh-meeting-v2\
├── presentation.html        ← 단일 HTML 발표 파일 (메인)
├── structures/              ← top 5 PDB
├── renders/                 ← ChimeraX 5장
├── plots/                   ← BC + AF3 PAE/pLDDT 20장
├── presentation_content.md  ← 원본 콘텐츠 (참고용)
├── top5_stats.json          ← 백업 데이터
└── SESSION_HANDOFF.md       ← 이 파일
```

## 🎬 현재 상태

- **16장 슬라이드** (Electric Studio 스타일 + 인터랙티브)
- **사용 스킬**: `frontend-slides` (Claude Code plugin, zarazhangrui/frontend-slides)
- **인터랙티브**: Slide 7 Chart.js bar chart, Slide 10 NGL Viewer (Rank 1~5 버튼)
- **발표 일정**: 2026-05-22 오후 (대상: 교수님 + 랩 미팅)

## 📋 슬라이드 구조 (16장)

| # | 제목 | 핵심 |
|---|---|---|
| 1 | Title — Two-panel split | 101 / 37 / Top 5 |
| 2 | 한 줄 요약 | 3개 big numbers + narrative |
| 3 | RFdiff → BindCraft 노선 변경 | 좌우 비교 |
| 4 | Modular Assembly | 모듈 표 + 메커니즘 |
| 5 | Tag / Linker 설계 | seg 색상 분할 |
| 6 | BindCraft Trial 종합 | 6개 trial 표 + pivot callout (14→101) |
| 7 | AF3 Cross-prediction | **Chart.js bar** + 통계 |
| 8 | Top 10 정량 비교 | 큰 표, top 5 강조 |
| 9 | Top 5 Overview | ChimeraX 5장 + PAE 그리드 |
| 10 | Top 5 Interactive | **NGL Viewer** + Rank 1~5 버튼 |
| 11 | Cloning 진행 (100% / 80% / 0% ×4) | 6 step 진행률 + 목표 수율 |
| 12 | Binder Gene 설계 | Vector-His8-TEV-binder 구조 + overhang |
| 13 | Validation Workflow | **7 step 표준 + 약점 2곳 강조** |
| 14 | MARCO Trial 종합 | 13개 trial 표 + A508 hit |
| 15 | MARCO Top 10 | i_pTM 0.69~0.76, 추천 ★ 2개 |
| 16 | Q&A | data sources |

## 🚀 서버 띄우기 (NGL viewer 작동 필수)

```bash
cd "C:\Users\Andy\OneDrive\Desktop\Fire\de_novo\Claude_code_output\colh-meeting-v2"
python -m http.server 4000
```

브라우저: `http://localhost:4000/presentation.html`

## 🌐 GitHub Pages 셋업 (어디서든 접근, 5~10분)

```bash
cd "C:\Users\Andy\OneDrive\Desktop\Fire\de_novo\Claude_code_output\colh-meeting-v2"
git init
git add .
git commit -m "ColH meeting presentation"
gh repo create colh-meeting --public --source=. --push
gh api -X POST /repos/:owner/colh-meeting/pages -f source.branch=main -f source.path=/
```

배포 후: `https://<github-username>.github.io/colh-meeting/presentation.html`

## 🎨 디자인 시스템

- **스타일**: Electric Studio (`frontend-slides` preset)
- **컬러**: 화이트 배경 + 검은 텍스트 + 블루 액센트 `#4361ee`
- **폰트**: Manrope (display 800, body 400/500), JetBrains Mono (data)
- **다크 패널 사용처**: Slide 1 bottom, Slide 6 pivot callout, Slide 11 yield, Slide 12 overhangs, Slide 16 footer

## ⚠️ 발표 직전 점검

- F11 풀스크린에서 16장 모두 글자 잘림 확인
- Slide 7 chart 그려지는지
- Slide 10 NGL — Rank 1~5 버튼 클릭 시 PDB 전환 확인
- Slide 16 (Q&A) — 폰트 정상 적용 확인
- 인터넷 연결 (Google Fonts, Chart.js CDN, NGL CDN 로딩 필요)

## 🔄 내일 이어가기 — 한 줄 명령

새 Claude Code 세션 열고:

```
C:\Users\Andy\OneDrive\Desktop\Fire\de_novo\Claude_code_output\colh-meeting-v2\presentation.html
이어서 작업하자. SESSION_HANDOFF.md 먼저 읽어. Slide N의 ___ 부분 고치고 싶어.
```

## 📝 내일 수정 후보 (Andy 검토 사항)

- 슬라이드 순서 재배치?
- 일부 콘텐츠 문구 다듬기
- 강조하고 싶은 메시지 보강 — 어디?
- (필요시) GitHub Pages 배포

## ⚙️ 알려진 함정 (다음 Claude가 알아야)

1. **CSS 셀렉터 변경 시 trailing space 유지 필수**: `#s14 .qa-main` (자손 셀렉터)와 `#s14.qa-main` (복합 셀렉터)는 완전히 다른 의미. `#sN ` → `#sM ` 변경 시 반드시 trailing space 포함. (이번 세션에서 2번 깨졌음)
2. **NGL은 HTTP 서빙 필수**: `file://` 프로토콜로는 PDB CORS 실패
3. **BindCraft 출력 PDB 잔기 재번호**: 4ar1 A423/A533 = 출력 PDB의 A83/A193 (offset 340)
4. **Slidev 백업 폴더 존재**: `../colh-meeting/` (fallback, 현재 사용 안 함)
