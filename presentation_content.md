# ColH PD apo Binder — BindCraft Top 5

발표자: 강현호 · 일자: 2026-05-21 · 미팅 진행 보고

---

## Slide 1 — Title

- 제목: ColH PD apo Binder 설계 진행 보고
- 부제: BindCraft 1st trial (apo, hotspot A533/A423) → AF3 cross-validation → Top 5
- 한 줄 메시지: 101개 binder를 AF3 cross-prediction으로 검증해 cloning/스크리닝할 top 5 확정

---

## Slide 2 — 한 줄 요약 (Big Numbers)

핵심 숫자 3개:

- **101** — BindCraft accepted (apo 1st trial)
- **37 / 101** — AF3 ipTM ≥ 0.8 (high confidence)
- **Top 5** — BC + AF3 양쪽 통과 후보, cloning 진입

서술: ColH PD apo form(4ar1_apo)을 타깃으로 BindCraft 1차 trial을 돌려 101개 accepted binder 확보. 101개 전부 AF3 cross-prediction으로 재검증한 뒤 top 5를 정량·시각 양면에서 비교해 cloning + 발현 스크리닝 진행 후보 확정.

---

## Slide 3 — 노선 변경: RFdiffusion → BindCraft

두 컬럼 비교:

**RFdiffusion + ProteinMPNN + AF3 (기존)**
- backbone 생성 → 서열 디자인 → AF3 검증 3단 분리
- num_designs 1000+ 필요, 후보 거르기 후행
- ColH PD 1~4차 시도에서 accepted 0~1개
- hotspot 지정 가능하나 길이/구조 제어 약함

**BindCraft (현재 채택)**
- end-to-end (AF2 hallucination + MPNN + filter 통합)
- hotspot/길이/helix bias 단일 설정으로 제어
- filter 만족 design만 accepted로 저장
- ColH PD apo 1st trial: **101 accepted** (단일 trial)

각주: 교수님 예상 질문 — "RFdiffusion으로 한 번이라도 돌렸나" → ColH는 1~5차 trial 시도, 누적 15개. BindCraft 전환 후 단일 trial 101개.

---

## Slide 4 — Modular Assembly 설계

구성 모듈 (단일 폴리펩타이드 아닌 독립 발현 후 SpyTag/SpyCatcher 결합):

| 모듈 | 구성 | 기능 |
|---|---|---|
| CU (full) | ST – AD – PD – ABD | 활성화 후 콜라겐 분해 |
| Binder | SC – linker – binder – His6 | PD cleft 마스킹 |
| PD 단독 | His – PD | BLI/IP 단독 평가용 |

작동 원리:
- **활성화 전 (tethered)**: Ceff ~mM ≫ Kd ~μM → binder가 PD 덮어 활성 OFF
- **MMP 절단 후 (활성)**: Ceff → 0, 체내 농도 nM ≪ Kd → binder 해리 → PD 활성 복원

선택 이유:
- IB 회피 (단일 폴리펩타이드 위험 회피)
- 변수 분리 (각 모듈 독립 평가)
- binder 스크리닝 용이

---

## Slide 5 — Tag/Linker 설계

세 가지 발현 형태:

| 형태 | 구성 |
|---|---|
| ST-CU-twin strep | MGSS-ST(13aa)-GSGESGSG-CU 본체-twin strep |
| PD-twin strep | M-PD(active domain)-twin strep |
| Binder-His | M-SC-linker-binder-His6 |

핵심:
- SpyTag(ST) = 13aa peptide, SpyCatcher(SC)와 covalent 결합
- 기존 Ferritin vector primer 재사용 불가 → 신규 primer 4쌍 설계 완료 (260428)

---

## Slide 6 — BindCraft trial 종합

Trial별 accepted 개수:

| Trial | Target | Hotspot | Length | Accepted |
|---|---|---|---|---|
| 1차 (holo) | 4ARF | A533, A444, A423 | 40-80 | 0 |
| 2차 | 4ARF | A533, A423 | 60-120 | 1 |
| 3차 (short) | 4ARF | A533, A423 | 30-45 | 0 |
| 4차 (nohot) | 4ARF | 없음 | 40-60 | 0 |
| 5차 | 4ARF | A533, A423 | 60-120 | 14 |
| **apo 1차 (현재)** | **4ar1_apo** | A533, A423 | 60-120 | **101** |

핵심 변경: **holo → apo form** 전환.
- holo (inhibitor bound) → cleft 닫혀있음, binder 접근 표면 좁음
- apo (자유 상태) → cleft 열려있음, hotspot 도달 용이
- 결과: accepted **약 7배 증가** (14 → 101)

---

## Slide 7 — AF3 cross-prediction 검증

방법: 101개 BindCraft accepted를 AF3로 재예측 (독립 검증)
- AF3는 AF2 multimer와 다른 weight → BindCraft 자체 confidence와 무관
- 두 모델 모두 같은 결합 모드 예측 = cross-prediction 통과

신뢰 구간:
- AF3 ipTM ≥ 0.8 → confident (선택 추진)
- 0.6 ≤ ipTM < 0.8 → gray (참고)
- ipTM < 0.6 → failed (배제)

**101개 분포 (실제 차트로 그릴 것 — bar chart)**:
- high (≥0.8): **37**
- mid (0.6-0.8): **19**
- low (<0.6): **45**

지표 통계:
- AF3 ipTM: min 0.16, mean 0.63, max 0.94
- AF3 i_pae: min 4.52, mean 13.12, max 26.64

메시지: 절반 가까이(45/101) low confidence → **BindCraft 단독 신뢰는 위험**. 상위 37개를 후보군으로 진행, top 5 우선 cloning.

---

## Slide 8 — Top 10 정량 비교 표

(BC = BindCraft, AF3 = cross-prediction)

| Rank | Design | Len | BC i_pTM | AF3 ipTM | dG | Hot_RMSD | Helix% | AF3 rank |
|---|---|---|---|---|---|---|---|---|
| 1 | l96_s354818_mpnn2 | 96 | **0.90** | **0.93** | -63.5 | 1.35 | 78 | 6 |
| 2 | l78_s205703_mpnn16 | 78 | 0.89 | 0.89 | -70.3 | 1.72 | 67 | 20 |
| 3 | l68_s564178_mpnn11 | 68 | 0.88 | 0.68 | -58.1 | 1.21 | 81 | 50 |
| 4 | l77_s998973_mpnn13 | 77 | 0.87 | 0.72 | -45.5 | 1.04 | 86 | 48 |
| 5 | l88_s170448_mpnn6 | 88 | 0.87 | **0.89** | -64.3 | 1.40 | 79 | 21 |
| 6 | l113_s776041_mpnn2 | 113 | 0.87 | 0.92 | -52.1 | 1.18 | 89 | 4 |
| 7 | l77_s998973_mpnn14 | 77 | 0.86 | 0.49 | -46.4 | 1.05 | 86 | 69 |
| 8 | l109_s693003_mpnn7 | 109 | 0.86 | 0.94 | -54.8 | 1.32 | 88 | — |
| 9 | l109_s648895_mpnn14 | 109 | 0.86 | 0.92 | -49.2 | 1.27 | 84 | — |
| 10 | l113_s776041_mpnn8 | 113 | 0.86 | 0.89 | -53.0 | 1.19 | 88 | — |

색상 강조:
- Rank 1: BC + AF3 양쪽 최상위, dG -63.5 → **최우선 추진**
- Rank 2, 5: BC top + AF3 ≥ 0.89 → 동반 추진
- Rank 3, 4: BC 높지만 AF3 떨어짐 → 관찰 후 결정

---

## Slide 9 — Top 5 Overview (이미지 + 표)

ChimeraX 렌더 5장 (회색 surface = target ColH PD, 무지개 cartoon = binder N→C, 빨간 sticks = hotspot ASN83/ALA193 = 입력 A423/A533):

- renders/binder1_render.png — Rank 1 l96_s354818, i_pTM 0.90/0.93, dG -63.5
- renders/binder2_render.png — Rank 2 l78_s205703, i_pTM 0.89/0.89, dG -70.3
- renders/binder3_render.png — Rank 3 l68_s564178, i_pTM 0.88/0.68, dG -58.1
- renders/binder4_render.png — Rank 4 l77_s998973, i_pTM 0.87/0.72, dG -45.5
- renders/binder5_render.png — Rank 5 l88_s170448, i_pTM 0.87/0.89, dG -64.3

PAE 비교 (BindCraft 디자인 단계 vs AF3 cross-validation):
- plots/binder{1..5}_bc_pae.png — BindCraft PAE 5장
- plots/binder{1..5}_af3_pae.png — AF3 PAE 5장

---

## Slide 10 — Top 5 Interactive Structure (NGL Viewer)

별도 인터랙티브 슬라이드 — NGL Viewer + Rank 1~5 버튼.
PDB: structures/binder{1..5}_complex.pdb
조작: 드래그 회전 / 휠 줌 / Shift+드래그 이동
표시: target chain A = gray surface, binder chain B = rainbow N→C, hotspot A83/A193 = red sticks

각 binder 상세 정보 (버튼 전환 시 우측 패널 업데이트):
| Rank | Name | Len | BC i_pTM | AF3 ipTM | dG | Hot_RMSD |
|---|---|---|---|---|---|---|
| 1 | l96_s354818_mpnn2 | 96 | 0.90 | 0.93 | -63.5 | 1.35 |
| 2 | l78_s205703_mpnn16 | 78 | 0.89 | 0.89 | -70.3 | 1.72 |
| 3 | l68_s564178_mpnn11 | 68 | 0.88 | 0.68 | -58.1 | 1.21 |
| 4 | l77_s998973_mpnn13 | 77 | 0.87 | 0.72 | -45.5 | 1.04 |
| 5 | l88_s170448_mpnn6 | 88 | 0.87 | 0.89 | -64.3 | 1.40 |

---

## Slide 11 — 다음 단계: Cloning + 발현 스크리닝

Phase 1 진행 상태 (체크리스트 / 진행률):

1. ColH cloning (ST-CU-twin strep, PD-twin strep) — **60%** (gene 도착, DH5α transformation 완료, mini prep/PCR 대기)
2. Binder gene 합성 주문 (top 5, T7+terminal 포함) — 10% (합성 방법 확립 중)
3. Binder-His cloning (SC-linker-binder-His6) — 0% (gene 합성 후 GA cloning)
4. Col 활성 test 확립 — 0% (binder masking 평가 기반)
5. PD ↔ Binder IP screening (1차 거름) — 0%
6. PD BLI (top 5 → top 20 확장 결정) — 0% (Kd 정량)

목표 발현 수율 (이 기준 충족 시 다음 단계 진입):

| 모듈 | 목표 수율 | 비고 |
|---|---|---|
| PD-twin strep | ≥ 5 mg/L | BLI/IP에 필요 |
| ST-CU-twin strep | ≥ 2 mg/L | masking 평가 |
| SC-binder-His | ≥ 10 mg/L | IP 1차 필터링용, 양 많이 필요 |

---

## Slide 12 — 마무리: Q&A

데이터 출처:
- BindCraft ranking: ColH_PD_apo_bindcraft_ranking.csv (101 designs)
- AF3 cross: ColH_PD_apo_AF3_ranking.csv (101 jobs)
- Target: 4ar1_apo.pdb chain A, hotspot A423/A533 (출력 PDB에서 A83/A193, BindCraft 잔기 재번호 특성)

---

## 디자인 지시

- **톤**: 학술 미팅, 데이터 강조. 너무 화려하지 않게
- **추천 스타일**: Swiss Modern 또는 Paper & Ink (frontend-slides 빌트인)
- **차트**: ASCII 막대 절대 X. 실제 차트 (Chart.js 등)로:
  - Slide 7 분포: 가로 막대 (high/mid/low 색 구분)
  - Slide 8 Top 10: 가능하면 i_pTM scatter 또는 dot plot
- **숫자 강조**: Slide 2 big numbers는 큰 폰트로 시각적 강조
- **이미지**: Slide 9의 5장 PNG는 grid 정렬, 각각 캡션
- **인터랙티브**: Slide 10은 NGL Viewer (vanilla JS, CDN), Rank 1~5 버튼
- **글자 잘림 절대 금지** — 풀스크린 1920×1080 기준 모든 텍스트 가시
