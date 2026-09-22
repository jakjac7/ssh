# 서울부동산 1970 — UI/UX Screen Specification
## v0.1 — Landscape Mobile / Three.js 2.5D Visual System

- **문서 상태:** UX / Visual Direction Draft
- **기준 문서:** PRD v0.5 / GDD v0.4
- **플랫폼:** Mobile First — Android 우선, iOS 확장 가능
- **기본 방향:** 16:9 Landscape Safe Gameplay Area + Wide-device Responsive Extension
- **렌더링:** Three.js WebGL World + HTML/CSS HUD/Panel Hybrid
- **비주얼 제안:** 2D Retro Cartographic + Editorial UI + restrained 2.5D depth
- **핵심 원칙:** Complex Simulation, Simple Decision / City Changes the Rules / Competitive Integrity

> **이 문서의 목적**
>
> PRD/GDD에 정의된 시스템을 실제 모바일 화면과 상호작용으로 번역한다.  
> 타이틀 진입부터 Run Setup, 본게임, 거래, 뉴스, 5년 결산, Weekly Same-Seed Challenge, 최종 인생 엔딩까지의 Screen Architecture와 Visual System을 구현 가능한 수준으로 정의한다.

---

# 0. Executive Decision

## 0.1 권고 Visual Direction

《서울부동산 1970》의 메인 비주얼은 **픽셀아트가 아닌 2D Vector/Illustration 기반의 Retro Cartographic Editorial Style**을 권고한다.

정확히는 다음 조합이다.

- **옛 서울 지도 / 지형도**의 질감과 시대성
- **신문·부동산 장부·계약서**의 정보 디자인
- **교통 노선도** 수준의 단순하고 명확한 공간 그래픽
- Three.js의 Pan / Zoom / Layer / Line Animation / Sprite / 얕은 Depth를 활용한 **2.5D 도시 변화 연출**
- 숫자·계약·표·버튼은 WebGL 내부가 아니라 **HTML/CSS 기반 UI**를 우선

이를 이 문서에서는 임시로 **SEOUL LEDGER Visual System**이라 부른다.

## 0.2 Pixel Art를 Main Direction으로 권고하지 않는 이유

Pixel Art 자체가 나쁜 선택은 아니지만 본 프로젝트의 핵심 가치와 충돌하는 지점이 많다.

| 평가항목 | Pixel Art | Vector / Editorial + 2.5D |
|---|---:|---:|
| 옛 서울 시대감 | 4/5 | 5/5 |
| 지도 가독성 | 3/5 | 5/5 |
| 금융정보 가독성 | 3/5 | 5/5 |
| 35~59세 타깃 수용성 | 3/5 | 5/5 |
| 도시 변화 표현 | 4/5 | 5/5 |
| 제작비 통제 | 4/5 | 4/5 |
| Three.js 궁합 | 4/5 | 5/5 |
| 제품 차별성 | 3/5 | 5/5 |

Pixel Art는 캐릭터 RPG·인디게임 정서를 강화하지만, 이 게임의 핵심은 캐릭터 애니메이션이 아니라 **서울이라는 공간의 변화와 자산의 이동을 읽는 것**이다.

따라서 캐릭터를 도트로 움직이게 만들기보다 서울 지도와 문서 UI를 게임성의 전면에 둔다.

## 0.3 3D Full City를 권고하지 않는 이유

- 핵심 의사결정이 건물 감상이 아니라 **정보·위치·현금흐름 비교**임
- 18~40+ Node, 시대별 도시변화, 교통 레이어까지 3D 모델링 시 Asset Scope가 급증
- 모바일 WebGL 성능 부담
- 40~60대 포함 타깃에서 카메라 회전·Perspective는 가독성을 오히려 떨어뜨릴 수 있음
- 역사적 도시 재현 기대치를 불필요하게 높임

따라서 **평면 지도를 살아 움직이게 하는 수준의 2.5D**가 적정하다.

---

# 1. Product-to-Screen Translation Principles

PRD/GDD의 핵심 원칙을 화면 규칙으로 번역한다.

## 1.1 한 화면 = 하나의 핵심 질문

예:

- Run Setup: **어떤 인생으로 시작할 것인가?**
- 첫 집 선택: **어디서 살 것인가?**
- Node Detail: **여기에 시간과 돈을 쓸 가치가 있는가?**
- Property: **이 물건을 살 것인가, 임차할 것인가?**
- Contract: **이 거래 이후 내 상태가 감당 가능한가?**
- 5년 결산: **지난 5년의 선택이 맞았는가?**
- 엔딩: **근로소득을 자산소득으로 전환했는가?**

한 화면에 복수의 주의집중 목표를 만들지 않는다.

## 1.2 Map is the World

지도는 단순 배경이 아니라 본게임의 기본 Surface다.

- Home / Work는 지도 위에 항상 존재
- 교통·시세·학군·개발·내 자산은 동일 지도 위 Layer 전환
- 뉴스 이벤트는 지도로 돌아와 실제 시스템 변화로 확인
- 매수/매도 이후 해당 Node와 지도 아이콘이 즉시 변화
- 엔딩에서도 1970 → 종료연도의 서울 변화를 지도 위에서 재생

## 1.3 Context Panel, Not Menu Maze

Landscape에서 우측 30~34% 영역은 **고정 Context Panel**로 사용한다.

선택한 대상에 따라 내용만 바뀐다.

- Node 선택 → 지역정보
- Property 선택 → 매물정보
- Broker 선택 → 중개 관계 / 정보
- Bank 선택 → 금융
- Work 선택 → Career
- News 선택 → 기사 / 영향

별도 풀스크린 메뉴로 계속 이동하지 않는다.

## 1.4 Before / After 우선

복잡한 금융용어보다 선택 결과를 보여준다.

- 현금 `0.80Y → 0.14Y`
- 부채 `0.30Y → 1.00Y`
- 이자 `0.02Y → 0.08Y`
- 여유 `4 → 2`
- 통근 `65분 → 31분`

변화량이 의사결정의 중심이다.

## 1.5 World Language over Generic Game Currency

UI에 일반적인 보석/에너지 아이콘을 전면 배치하지 않는다.

- AP → **여유**
- Booster → 부모찬스 / 복덕방 인맥 / 은행원 인맥 / 연차 / 경제신문 / 계약 재검토
- Store → 가능하면 **신문가판대 / 생활지원 / 기록실** 등 맥락형 진입

## 1.6 Standard / Assisted Integrity

성과에 영향을 주는 지원 사용 전에는 항상 Run Mode 전환을 명확히 보여준다.

- Standard Ranked: 공식 Percentile / Leaderboard 가능
- Assisted: 지원 가능, 공식 Standard Percentile 제외
- 전환은 되돌릴 수 없음
- Result / Share에서 Assisted 표기를 숨기지 않음

---

# 2. Landscape Device Strategy

## 2.1 기준 해상도

디자인 기준 Logical Canvas:

`1600 × 900 (16:9)`

16:9는 실제 기기 비율을 강제하는 값이 아니라 **Guaranteed Safe Gameplay Area**로 사용한다.

## 2.2 Wide Device 대응

19.5:9 / 20:9 기기에서는 중앙 16:9 영역을 보존하고 좌우 Extra Area를 확장한다.

Extra Area 사용 가능:

- 지도 확장
- 뉴스 Ticker
- 친구/Challenge Mini Rank
- 장식적 지도 여백
- Context Panel의 보조정보

Extra Area에 두면 안 되는 요소:

- 핵심 Confirm CTA
- 현금 / 부채 / 여유
- Home / Work 식별
- 계약 위험 경고
- Standard / Assisted 표시

## 2.3 Safe Area

모든 Device Cutout / Gesture Area를 고려한다.

- 좌우 최소 Safety Padding: 32 logical px
- 상하 최소 Safety Padding: 20 logical px
- 핵심 CTA 최소 터치영역: 48×48 logical px 이상
- 타깃 40~60대를 고려해 작은 텍스트 남용 금지

---

# 3. Global Layout Grid

기본 본게임 화면을 다음처럼 구성한다.

```text
┌──────────────────────────────────────────────────────────────────────┐
│ TOP STATUS BAR  7~9%                                                │
│ 1975 | 현금 | 순자산 | 부채 | 연 이자 | 여유 | STANDARD            │
├───────────────────────────────────────────────┬──────────────────────┤
│                                               │                      │
│                                               │   CONTEXT PANEL      │
│                                               │     30~34%           │
│                THREE.JS MAP                   │                      │
│                  66~70%                       │                      │
│                                               │                      │
│                                               │                      │
├───────────────────────────────────────────────┴──────────────────────┤
│ BOTTOM LAYER / ACTION BAR  8~10%                                    │
└──────────────────────────────────────────────────────────────────────┘
```

## 3.1 Top Status Bar

항상 표시하는 핵심값:

- 현재연도
- 현금
- 순자산
- 부채
- 남은 여유
- Run Mode Badge

상황에 따라 표시:

- 연간 이자
- 근로소득
- 임대소득
- Challenge Timer가 아닌 Challenge ID/상태

## 3.2 Map Area

기본 66~70%.

표시 우선순위:

1. Home
2. Work
3. 현재 선택 Node
4. 내 보유자산
5. 교통 연결
6. 이벤트 변화
7. 정보 Freshness / 관심지역

## 3.3 Context Panel

고정 폭을 기본으로 하되 Fullscreen Sheet가 필요하면 확장 가능.

기본 구조:

```text
[대상명 / 시대명칭]
[핵심 한줄]

핵심지표 3~5개
────────────
상태 / 장점 / 위험
────────────
Primary CTA
Secondary CTA
```

## 3.4 Bottom Layer Bar

기본 Layer:

- 기본
- 교통
- 시세
- 학군
- 개발
- 내 자산

우측 Primary Progress CTA:

- `올해 마무리`
- `1976년으로`
- 상황에 따라 비활성/경고

---

# 4. Visual System — SEOUL LEDGER

## 4.1 Visual Keywords

- 지도
- 장부
- 경제신문
- 계약서
- 낡은 종이
- 교통노선
- 활판 인쇄
- 서울의 성장
- 기록
- 시간의 축적

## 4.2 하지 않을 것

- 과도한 픽셀 노이즈
- 모든 UI를 낡은 종이로 덮기
- 복고 효과 때문에 숫자 가독성을 희생
- CRT / VHS 효과 남용
- 과도한 세피아
- 1970년대를 무조건 갈색으로 표현
- 현대 모바일 금융앱처럼 너무 무균질하게 만들기

## 4.3 시대별 Surface 변화

Layout과 Interaction은 유지하고 Surface만 점진적으로 변화시킨다.

### 1970s
- 저채도 종이 Texture
- 흑/청/적 중심 제한 팔레트
- 활판·도장·수기 장부 느낌
- 도로·교통 표시 단순

### 1980s
- 인쇄 컬러 증가
- 지하철 노선색 존재감 상승
- 대단지/개발 표시가 지도에 증가

### 1990s
- 부동산 광고·신문 지면의 정보밀도 증가
- 가격표현이 정형화
- 지도 Label 증가

### 2000s
- 초기 디지털 부동산 정보화 느낌
- 표/리스트가 더 명확해짐
- 검색/거래사례 표기가 정돈

### 2010s~2020s
- 현대적 지도와 정보패널
- 종이 질감은 약해지고 디지털 UI 비중 증가
- 단, 전체 게임의 브랜드 Typography / Grid는 유지

## 4.4 시대변화의 목적

단순 스킨 교체가 아니다.

플레이어가 느껴야 하는 것:

> “서울뿐 아니라 정보를 얻는 방식도 현대화되었다.”

초기 중개 UI:

> “이 근방은 요즘 이 정도에 거래된다더군요.”

후기 중개 UI:

- 최근 거래사례
- 시세 범위
- 전세가율
- 거래량

---

# 5. Rendering Architecture

## 5.1 기본 분리

```text
<App Shell>
│
├─ WebGL Canvas / Three.js World
│  ├─ Terrain / River
│  ├─ Node Polygon
│  ├─ Road / Rail / Subway
│  ├─ Building / POI Sprite
│  ├─ Home / Work Marker
│  ├─ Asset Marker
│  ├─ Development Animation
│  └─ Event Effects
│
└─ HTML / CSS UI
   ├─ TopStatusBar
   ├─ ContextPanel
   ├─ BottomLayerBar
   ├─ NewsSheet
   ├─ ContractSheet
   ├─ ChapterResult
   ├─ ChallengeHub
   └─ Modal / Toast
```

## 5.2 Camera

권고:

- 기본은 **Orthographic-like top-down presentation**
- 실제 구현은 OrthographicCamera 우선 검토
- Tilt가 필요할 경우 극히 제한된 2.5D 연출용으로만 사용
- 카메라 회전은 사용자 조작에서 제외

플레이어 입력:

- 1 Finger Drag → Pan
- Pinch → Zoom
- Node Tap → Select
- Double Tap Node → Focus Zoom
- Long Press → 보조정보/툴팁은 P1 검토

## 5.3 Depth 사용 규칙

Depth는 “멋”보다 정보 우선.

사용:

- 개발지역 건물 Silhouette 상승
- 교량 생성
- 대단지 입주
- 지하철 노선 draw-on
- Home/Work Marker elevation

비사용:

- 모든 건물을 실제 3D로 모델링
- 자유 카메라 회전
- 현실적 Shadow Simulation

## 5.4 Performance Guardrail

- 지도 Static Geometry는 Batch
- 반복 Marker / Building은 Sprite 또는 Instancing 검토
- 시대 Texture는 해상도 Cap 설정
- 애니메이션은 이벤트 시점 중심, 상시 Particle 남용 금지
- Low-end Android 기준 FPS와 Memory를 M3에서 별도 Gate 설정

---

# 6. Master Screen Map

전체를 13개 Screen Family로 구분한다.

| ID | Screen Family | 핵심 질문 | 빈도 |
|---|---|---|---|
| S01 | Splash / Title | 이 세계에 들어갈 것인가 | 세션 시작 |
| S02 | Main Lobby | 어디서 이어갈 것인가 | 매 세션 |
| S03 | Run Setup | 어떤 인생 / 어떤 규칙인가 | Run 시작 |
| S04 | Opening 1970 | 어디서 일하고 어디서 살 것인가 | Run 시작 |
| S05 | Main Map | 올해 무엇을 할 것인가 | 핵심 |
| S06 | Node / Broker | 어디를 조사할 것인가 | 매우 빈번 |
| S07 | Property Detail | 이 물건은 가치가 있는가 | 빈번 |
| S08 | Contract / Finance | 이 거래를 감당할 것인가 | 핵심 피크 |
| S09 | News / Event | 세상이 어떻게 바뀌었는가 | Turn별 |
| S10 | Year End | 올해 결과는 어땠나 | Turn별 |
| S11 | 5-Year Chapter | 지난 5년 전략은 맞았나 | 5 Turn |
| S12 | Weekly Challenge | 같은 조건에서 나는 몇 등인가 | Live Ops |
| S13 | Final Life Ending | 어떤 인생을 만들었나 | Run 종료 |

---

# 7. S01 — Splash / Title

## 7.1 목적

- 1970년 서울의 “아직 완성되지 않은 도시”를 첫인상으로 각인
- 부동산 앱이 아니라 게임임을 전달
- 후반부 현대 서울과 대비되는 시작점 확보

## 7.2 화면구성

```text
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│                 1970 SEOUL MAP                               │
│                                                              │
│                     서울부동산                               │
│                       1970                                   │
│                                                              │
│          월급쟁이로 시작해 서울에서 살아남아라               │
│                                                              │
│                     [ 화면을 터치 ]                          │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

## 7.3 Visual

- 한강과 구도심을 중심으로 한 1970 Base Map
- 남동부는 상대적으로 비어 보이게
- 버스 1대 정도의 느린 Sprite 이동
- 종이 Texture는 미세하게
- 타이틀 등장 시 과도한 Logo Animation 금지

## 7.4 Sound

- 짧은 인쇄기 / 종이 넘김 / 도심 ambience 혼합
- 음악은 장엄함보다 관찰·회고 톤

## 7.5 Interaction

- Tap → S02 Main Lobby
- 첫 실행이면 Tap → 짧은 Brand Intro 후 S03

---

# 8. S02 — Main Lobby

## 8.1 목적

- 이어하기를 최우선
- Weekly Challenge와 새 Run을 명확히 노출
- Store가 게임 전면을 점유하지 않음

## 8.2 Layout

왼쪽 약 65%:
- 마지막 저장시점 서울 지도
- Home / Work / 대표 자산

오른쪽 약 35%:

```text
서울부동산 1970

1985 · 과장
순자산 7.8Y
대치 20평 자가

[ 이어서 살기 ]

새 인생
이번 주의 서울
기록실
생활지원 / 신문가판대
설정
```

## 8.3 States

### No Save
- `새 인생` Primary
- `이번 주의 서울` Secondary

### Existing Campaign
- `이어서 살기` Primary
- 최근 Chapter 진행률 표시

### Challenge Active
- 작은 Newspaper Badge
- `이번 주 기록: 상위 18%`

## 8.4 Monetization Entry

`상점`이라는 Generic Label 대신 P0.5에서 다음 중 하나 A/B 검토:

- 생활지원
- 신문가판대
- 지원센터

단, 소비자 오인을 막기 위해 진입 후 실제 구매 화면에서는 가격·상품성격을 명확히 표시한다.

---

# 9. S03 — Run Setup

## 9.1 Step 1 — Archetype

질문:

> **누구의 인생을 살아볼까요?**

카드:

- 신혼 직장인
- 과장
- 부장

권고 Visual:
- 얼굴 중심 Character Illustration보다 책상/사원증/월급봉투/서류가방 등 Still Life
- 자기투영 가능성 유지

각 카드 핵심값:

- 시작나이
- 소득
- 신용
- 남은 생애
- 한줄 특성

## 9.2 Step 2 — Run Mode

### 자력으로 살아보기
`STANDARD RANKED`

- 동일조건 공식 비교
- Percentile 등록
- 성과형 지원 사용 불가

### 도움을 받아 살아보기
`ASSISTED`

- 부모지원·인맥·연차·재도전 가능
- 공식 Standard Percentile 제외

## 9.3 Standard → Assisted 설명

짧게:

> 플레이 중 지원을 사용하면 해당 Run은 Assisted로 전환됩니다.  
> 캠페인과 엔딩은 정상 진행되지만 공식 Standard 순위에서는 제외됩니다.

## 9.4 Step 3 — Scenario

P0:
- 1970 기본 시나리오

P1/Paid:
- 다른 시작연도
- 경제위기 Scenario
- 직업군 Scenario

## 9.5 Confirm

마지막 화면:

```text
1970 · 과장
STANDARD

시작연봉   X
신용       보통
남은기간   XX년

[ 1970년으로 ]
```

---

# 10. S04 — Opening 1970

## 10.1 목표

복잡한 Tutorial 대신 **직장 공개 → 첫 집 선택**으로 게임 규칙을 체험시킨다.

## 10.2 Sequence

### Beat 1
검은 화면 / 신문 인쇄음

> **1970년 3월**

### Beat 2

> 당신은 서울의 한 회사에 취직했습니다.

지도 Zoom-in.

`★ 직장: 종로`

### Beat 3
지도 Zoom-out.

거주 후보 3~4개 활성.

예:

| 후보 | 주거 | 통근 | 초기자금 | 특징 |
|---|---|---:|---:|---|
| 성북 | 월세 | 42분 | 낮음 | 가까움 |
| 영등포 | 전세 | 55분 | 높음 | 자금 묶임 |
| 영동 | 월세 | 87분 | 낮음 | 멀지만 개발 여지 |

## 10.3 첫 선택 UI

Map Marker를 선택하면 우측 Context Panel이 갱신.

Primary CTA:

`여기서 시작하기`

Confirm 시:

- Home Marker 생성
- Work→Home 통근선 표시
- 여유 차감 예상 보여주기

## 10.4 Tutorial Policy

- 설명 말풍선 최대 1~2줄
- `다음`을 반복하는 8단계 Tutorial 금지
- 실제 선택과 동시에 학습

---

# 11. S05 — Main Map / Core Game

## 11.1 Base Wireframe

```text
┌────────────────────────────────────────────────────────────────────────┐
│ 1975   현금 0.42Y   순자산 1.83Y   부채 0.71Y   여유 ●●●○○   STANDARD │
├────────────────────────────────────────────────┬───────────────────────┤
│                                                │ 종로                  │
│                                                │                       │
│                                                │ 교통 ★★★★            │
│                                                │ 직장 ★★★★★           │
│                  SEOUL MAP                     │ 학군 ★★              │
│                                                │ 개발 ★★              │
│        🏠 HOME                 ★ WORK           │                       │
│                                                │ 최근 정보: 1년 전     │
│                                                │                       │
│                                                │ [조사하기]            │
├────────────────────────────────────────────────┴───────────────────────┤
│ 기본 │ 교통 │ 시세 │ 학군 │ 개발 │ 내 자산                 [올해 마무리] │
└────────────────────────────────────────────────────────────────────────┘
```

## 11.2 Map Layer Behaviors

### 기본
- 지형
- Node 이름
- Home / Work
- 주요 시설

### 교통
- 버스 / 철도 / 지하철 / 교량
- 활성 전/후 노선 차이 명확히

### 시세
- 정확한 Heatmap보다 정보신선도와 인지 시세를 함께 표현
- 정보가 오래되면 색이 흐려지거나 범위 Pattern으로 표시

### 학군
- 0~5 지수
- 시대별 변화가 보임

### 개발
- 계획 / 공사 / 완료 구분
- 루머와 확정은 아이콘 형태를 다르게

### 내 자산
- 보유주택
- 임대중
- 거주중
- 대출위험

## 11.3 Node Select

Tap Node:

- 카메라가 과도하게 이동하지 않고 가벼운 Focus
- Border Highlight
- 우측 Context Panel 업데이트

## 11.4 Home / Work

항상 시각적으로 구분.

- Home: 집 형태 Marker
- Work: 별 / 사원증 / 오피스 Marker
- 색만으로 구분하지 않고 형태도 다르게

## 11.5 Year Progress CTA

`올해 마무리` 활성 조건:

- 필수 상태 이상 없음
- 계약 Confirm 중 아님
- 해결해야 할 강제매각/거주공백이 없음

위험이 있어도 진행 가능한 경우:

`경고와 함께 진행`

---

# 12. S06 — Node / Broker Detail

## 12.1 Node Context Panel

예:

```text
영동
현재 행정명칭: ○○

교통      ★★
직장      ★
학군      ★
개발      ★★★★
지형      평지

시세정보: 2년 전
인지범위: 넓음

[지역 조사]  여유 1
[복덕방 방문] 여유 1
```

## 12.2 Information Freshness

숫자만 표시하지 않고 상태어 병기:

- 최신
- 양호
- 오래됨
- 불확실
- 매우 오래됨

## 12.3 Broker View

```text
영동 중앙복덕방
관계: ●●○○○

최근 거래 2건
급매 정보 없음
수수료 우대 없음

[매물 보기]
[관계 쌓기]
```

## 12.4 Assisted Context

Standard에서 Booster CTA를 누르면 즉시 효과를 주지 않는다.

예:

`복덕방 인맥 사용`

→ 전환 확인 Sheet:

> 이 지원을 사용하면 현재 Run이 **ASSISTED**로 전환되며 공식 Standard Percentile에서 제외됩니다.

[취소] [Assisted로 전환하고 사용]

---

# 13. S07 — Property Detail

## 13.1 구조

Map 위 Context Panel 또는 Large Side Sheet.

```text
대치 A아파트 25평
중층 · 2군 · 1984년
방3 / 욕1

매매        1.42Y
전세        0.88Y
월세        보증 0.15Y / 연 0.04Y

정보        1년 전

장점
+ 학군
+ 교통

주의
- 구축
- 소형

[매수]
[전세입주]
[월세입주]
[자세히]
```

## 13.2 Property Art

실제 건물 3D View를 기본으로 하지 않는다.

추천:
- 단지/주택유형의 시대별 2D Silhouette
- 사진풍보다 인쇄 일러스트 풍
- 주택유형을 즉시 식별할 정도의 형태 차이

## 13.3 Price Confidence

정보 Freshness에 따라 가격 표시가 달라짐.

예:

최신:
`1.38~1.45Y`

오래됨:
`대략 1.2~1.6Y`

정확한 Fair Value는 노출하지 않는다.

---

# 14. S08 — Contract / Finance

## 14.1 이 화면의 중요도

본게임에서 가장 강한 Decision Peak 중 하나다.

- 구매
- 전세입주
- 월세입주
- 대출
- 매도

모두 **Before / After Sheet** 형태로 통일한다.

## 14.2 Buy Contract Wireframe

```text
┌──────────────────────────────────────────────────────┐
│ 대치 A아파트 25평 — 매수                            │
│                                                      │
│ 매매가                         1.42Y                  │
│                                                      │
│                  현재          계약 후               │
│ 현금             0.80Y    →    0.14Y                │
│ 부채             0.30Y    →    1.00Y                │
│ 연 이자          0.02Y    →    0.08Y                │
│ 여유                4     →       2                  │
│                                                      │
│ ⚠ 금리 +2%p 시 연봉 대비 이자부담 24%               │
│                                                      │
│ [취소]                              [계약하기]       │
└──────────────────────────────────────────────────────┘
```

## 14.3 Risk Summary

최대 3개 우선 노출.

예:

- `현금 여유가 매우 낮아집니다.`
- `금리상승에 민감합니다.`
- `거주면적이 현재 필요규모보다 작습니다.`

세부 계산은 `자세히`에서.

## 14.4 Contract Animation

Confirm 후:

- 도장 찍는 짧은 애니메이션
- 지도 해당 Property에 내 자산 Marker 생성
- 현금/부채 값 Top Bar에서 Count transition

과도한 Celebration 금지. 자산 취득의 무게감을 유지.

## 14.5 Undo Context

Assisted에서 계약 재검토권이 있으면 Commit 직후 제한시간식 UX보다 **명시적 1회 CTA**를 짧게 노출.

- `계약 재검토권 사용`
- 사용시 Snapshot 복원
- RNG reroll 금지

---

# 15. S09 — News / Event

## 15.1 뉴스는 시스템 변경의 설명장치

단순 Flavor Text로 끝내지 않는다.

Flow:

`NEWS → WHAT CHANGED → MAP CHANGE`

## 15.2 Newspaper Sheet

```text
────────────────────────────────────────
서울경제일보                  1974년 ○월

서울지하철 1호선 개통

[시대 사진/일러스트]

도심과 주요 생활권의 이동시간이 줄어들기 시작했다.

게임 변화
종로 ↔ 영등포 이동비용 감소
관련 Node 교통지수 상승

[지도에서 보기]
────────────────────────────────────────
```

## 15.3 정보 등급 Visual

- 확정: 실선 / 도장
- 관측: 일반 Newspaper
- 루머: 점선 Border / 물음표 Stamp
- 노이즈: 신뢰도 낮음 명시

색상 하나로만 구분하지 않는다.

## 15.4 Map Reveal

`지도에서 보기`:

- Sheet 축소
- 카메라 관련 위치 Focus
- 노선/교량/단지 Animation
- 영향 Node Pulse

---

# 16. S10 — Year End

## 16.1 목표

1년마다 플레이 흐름을 끊지 않는 짧은 피드백.

권장 노출시간 2~4초 + Tap Skip.

## 16.2 Layout

```text
1976 → 1977

연봉          +8%
자산가치      +12%
임대소득      +0.04Y
이자          -0.06Y

순자산
1.42Y  →  1.76Y

[1977 시작]
```

## 16.3 Auto Highlight

올해 가장 큰 변화 1개만 큰 글씨.

예:

> **첫 임대소득이 발생했습니다.**

또는

> **금리상승으로 이자부담이 커졌습니다.**

---

# 17. S11 — 5-Year Chapter Settlement

## 17.1 역할

- 장기 플레이의 Reward Moment
- 전략 피드백
- AI 비교
- Share Loop
- 다음 5년 기대 형성

## 17.2 Stage 1 — City Before / After

```text
1970                                      1975
[MAP BEFORE]      → 변화 애니메이션 →     [MAP AFTER]
```

교통·개발·행정 변화 2~3개만 강조.

## 17.3 Stage 2 — Asset Result

```text
1975 자산결산

나                    AI 김과장
순자산 2.8Y           2.4Y
자산소득 0.12Y        0.08Y
부채 0.9Y             0.5Y

STANDARD
동일조건 상위 31%
```

Assisted라면:

`ASSISTED · 지원 3회 사용`

공식 Percentile 대신:

- AI Raw Score 비교
- 개인 Best

## 17.4 Stage 3 — Interpretation

### 가장 잘한 선택
> 1972 영등포 전세 진입

### 가장 큰 위험
> 신용대출 비중 38%

### 다음 5년 주의
> 금리 환경이 악화될 가능성이 있습니다.

최대 3 Card.

## 17.5 Stage 4 — Share

Primary:
`내 1975년 공유하기`

Secondary:
`다음 5년 시작`

공유이미지는 9:16 / 1:1 별도 Render 가능하되 게임 내부 화면은 Landscape 유지.

---

# 18. S12 — Weekly Same-Seed Challenge

## 18.1 Visual Theme

신문 1면 / 특별판 스타일.

## 18.2 Challenge Hub

```text
이번 주의 서울

1970 종로 직장인
월급은 적고, 강남은 멀다.

시작 현금  0.25Y
직장       종로
기간       1970~1980
Seed       KR-1970-W39

[도전하기]

내 최고기록
상위 18%

친구 기록
1. 김과장     3.82Y
2. 도꾸야마   3.61Y
3. 나         3.55Y
```

## 18.3 Integrity

- 공식 Leaderboard = Standard only
- Challenge Version 표시
- 유료 Membership 때문에 Standard Retry 수에서 우위 발생 금지

## 18.4 Retry Screen

Run 종료 후:

- `같은 Seed 재도전`
- `기록 공유`
- `친구 기록 보기`

전략학습을 위해 Standard 재도전 자체를 Paywall로 잠그지 않는다.

## 18.5 Share CTA

Share Card에서 상대가 바로 같은 Seed를 열 수 있어야 한다.

표시:

- Seed
- 시작조건
- 결과
- Percentile
- `같은 조건으로 도전`

---

# 19. S13 — Final Life Ending

## 19.1 엔딩의 목적

점수표가 아니라 **서울의 변화와 플레이어 인생을 하나의 Timeline으로 합친다.**

## 19.2 Ending Sequence

### Beat 1 — Back to 1970

1970 지도.

> 성북 월세  
> 종로 출근

### Beat 2 — Timeline Playback

지도 위에서 연도가 흐른다.

예:

- 1976 영등포 전세
- 1983 대치 20평 구축 매수
- 1991 25평 갈아타기
- 2004 오피스텔 월세 2채
- 2013 은퇴

각 시점에서 Home / Asset Marker가 이동·증가.

동시에:

- 노선 추가
- 교량 추가
- 도시 확장
- 대단지 등장

### Beat 3 — 2026 / Age 80

최종 서울 Map.

큰 숫자는 3개 중심.

```text
최종 순자산        28.4Y
연간 자산소득      0.82Y
동년배              상위 18%

근로소득 의존도     0%
```

Assisted:

```text
ASSISTED RUN
지원 사용 4회
공식 Standard Percentile 미등록
```

## 19.3 Final Question

> **회사가 없어도 살아갈 수 있었습니까?**

이 질문은 게임의 장기 Brand Promise와 직접 연결한다.

## 19.4 1970 vs Ending Map Slider

엔딩 마지막 Interaction:

```text
1970   |████████░░░░░░░|   2026
```

Drag 시:

- 도로
- 지하철
- 한강 교량
- 주요 단지
- 업무지
- 행정 경계

가 단계적으로 바뀐다.

이 화면은 Store Screenshot / Trailer에도 활용 가능한 Hero Feature로 본다.

## 19.5 Final CTA

- `내 인생 공유하기`
- `같은 조건 다시 살기`
- `다른 인생 시작`
- `기록실`

---

# 20. Supporting Screens

## 20.1 Portfolio / 내 자산

지도에서 `내 자산` Layer 선택 또는 Top Bar 순자산 Tap.

표시:

- 자산목록
- 현재가 인지범위
- 대출
- 세입자
- Equity
- 연간 Cash Flow

정렬:

- 가치
- 수익률
- 부채
- 지역

## 20.2 Career

Work Marker Tap.

```text
현재 직장
종로 · ○○상사

연봉        0.42Y
직급        과장
근속        7년
신용        양호

최근
1974 승진
1976 연봉동결

[이직 제안 보기]
```

## 20.3 Bank

- 대출 가능액
- 적용금리
- 기존부채
- 연 이자부담

은행원 인맥은 이 화면 맥락에서 노출.

## 20.4 Record Room

- Completed Runs
- Standard / Assisted Filter
- Best Percentile
- Challenge History
- Final Life Cards
- 주요 인생 Timeline

---

# 21. Monetization UX Integration

## 21.1 원칙

과금은 Store에서만 존재하지 않고 **필요한 순간의 Context**에서 자연스럽게 노출한다.

단, 구매압박이 Core Decision을 가리지 않는다.

## 21.2 부모찬스

노출 Context:

- 초기자본 선택
- 현금 부족
- 강제매각 직전

UI:

```text
부모에게 도움을 요청하시겠습니까?

현금 +X
Run당 사용 제한

⚠ 사용 시 ASSISTED로 전환됩니다.

[취소] [부모찬스 사용]
```

## 21.3 연차 하루

여유가 부족한 시점:

> **올해는 시간이 부족합니다.**

- 다음해로 넘어가기
- 연차 하루 사용 `여유 +1`
- Rewarded 획득 경로가 있다면 선택 표시

## 21.4 경제신문

지역정보가 오래되었을 때:

- 직접 조사
- 복덕방 방문
- 경제신문으로 정보 갱신

Core 행동을 삭제하지 않고 비용을 줄이는 선택.

## 21.5 Rewarded Ad

Power Reward 수령 전:

1. Standard → Assisted 전환 안내
2. 승인
3. 광고
4. 성공 Callback
5. Reward 적용

광고 실패 시 게임 상태가 변하면 안 된다.

---

# 22. Navigation Architecture

## 22.1 Top-level

```text
TITLE
  ↓
LOBBY
  ├─ Continue Campaign
  ├─ New Run
  ├─ Weekly Challenge
  ├─ Record Room
  └─ Support / Store
```

## 22.2 Campaign

```text
RUN SETUP
  ↓
OPENING
  ↓
MAIN MAP
  ├─ NODE
  │   ├─ BROKER
  │   └─ PROPERTY
  │        └─ CONTRACT
  ├─ BANK
  ├─ CAREER
  └─ NEWS
  ↓
YEAR END
  ↓
(5년마다) CHAPTER RESULT
  ↓
MAIN MAP
  ↓
FINAL ENDING
```

## 22.3 Back Button Rules

Android Back:

- Context Detail → Main Context
- Sheet → Sheet Close
- Main Map에서 Back → Pause/System Sheet
- 계약 Confirm 이후 상태를 OS Back으로 롤백하지 않음

---

# 23. Motion Language

## 23.1 Motion의 목적

- 도시가 변한다
- 자산이 이동한다
- 시간이 흐른다

## 23.2 사용 권고

- 노선 Draw-on
- 교량 Fade/Build
- 건물 Silhouette 상승
- Map Label 시대명칭 교체
- 자산 Marker 이동
- 숫자 Count transition
- 신문 Sheet Drop / Fold
- 계약서 Stamp

## 23.3 금지

- 모든 버튼 Bounce
- 과도한 Particle Celebration
- 슬롯머신형 숫자 애니메이션
- 부동산 매수 시 폭죽
- 무의미한 3D Camera Orbit

---

# 24. Typography / Information Hierarchy

## 24.1 Hierarchy

1. 현재 선택/질문
2. 핵심값
3. 변화량
4. 위험/주의
5. 세부정보

## 24.2 숫자

금액과 Percentile은 Tabular Figure 지원 Font 권고.

예:

- `0.42Y`
- `28.4Y`
- `상위 18%`

소수점 자릿수는 화면별 통일.

## 24.3 시대 Font

완전한 시대별 Font 교체는 금지.

- UI 본문 Font는 일관
- Headline / Newspaper에만 시대감 있는 Display Font 사용

가독성 우선.

---

# 25. Iconography

아이콘은 색보다 형태로 구분한다.

필수:

- Home
- Work
- Bank
- Broker
- School
- Rail/Subway
- Bus
- Bridge
- Construction
- Apartment
- Detached House
- Villa / Row House
- Office-tel
- Rent / Jeonse / Own
- Loan Risk
- Freshness
- Standard
- Assisted

권고 Style:

- 2D Flat / Print pictogram
- 지나치게 둥근 현대 SaaS icon 금지
- 선굵기 일정

---

# 26. Accessibility

타깃 연령을 고려해 P0부터 반영.

- 색맹 대응: 색 + Pattern / Shape
- Font Scale 옵션
- 최소 Contrast 기준 확보
- 작은 지도 Label 확대 시 자동 증대
- 숫자 변화에 색만 쓰지 않고 화살표/부호 사용
- 중요한 위험은 아이콘 + 텍스트 병기
- Motion Reduce 옵션 P1 검토

---

# 27. Telemetry — Screen / UX

기존 KPI Funnel에 Screen Event를 연결한다.

## 27.1 Core

- `title_enter`
- `lobby_enter`
- `new_run_start`
- `run_mode_selected`
- `first_work_reveal`
- `first_home_selected`
- `map_layer_used`
- `node_selected`
- `broker_open`
- `property_open`
- `contract_open`
- `contract_confirm`
- `year_end`
- `chapter_result`
- `share_card_open`
- `share_complete`
- `final_ending_start`
- `final_ending_complete`

## 27.2 UX Diagnostics

- Context Panel 평균 체류
- Back/Close 반복률
- Property→Contract 전환률
- Contract Cancel 이유
- Map Layer 사용률
- 특정 Node 과도한 반복 Tap
- Zoom/Pan 사용빈도

## 27.3 BM

- `assisted_conversion_prompt`
- `assisted_conversion_accept`
- `booster_context_impression`
- `booster_use`
- `rewarded_offer`
- `rewarded_complete`
- `store_open`
- `purchase_start`
- `purchase_complete`

---

# 28. Screen QA Gates

## 28.1 Layout

- 16:9에서 핵심 UI 잘림 0
- 20:9에서 핵심 UI가 Extra Area에만 의존하는 케이스 0
- Cutout 기기 CTA 가림 0

## 28.2 Map

- Home / Work 항상 식별 가능
- Layer 전환 후 선택상태 유지
- Node Label overlap 기준 정의
- 시대변경 후 행정명칭/지도 ID 정합성

## 28.3 Contract

- Before/After 계산값 Economy Engine과 100% 일치
- Cancel 시 상태변경 0
- Confirm 중복탭으로 이중거래 0

## 28.4 Standard / Assisted

- Standard에서 성과형 Booster 효과 적용 0
- 전환 Confirm 없이 Assisted 변경 0
- Assisted 결과의 Standard 표기 0
- Share Card Run Mode 오표기 0

## 28.5 Challenge

- Seed / Version 표시 일치
- 공식 Leaderboard Assisted 유입 0
- Share Deep Link로 동일 Challenge 복원

## 28.6 Accessibility

- 주요 상태 Color-only 표현 0
- 최소 Tap Target 위반 0
- 큰 Font Scale에서 핵심 CTA 겹침 0

---

# 29. MVP Screen Build Priority

## M3-A — Visual Proof

먼저 아래 6개를 High-fidelity Mock으로 만든다.

1. **Title**
2. **Run Setup**
3. **Main Map**
4. **Property + Contract**
5. **5-Year Settlement**
6. **Final Ending**

이 6장이 전체 Visual Direction을 결정한다.

## M3-B — Playable UX

- Opening
- Node / Broker
- News
- Year End
- Career / Bank

## M4.5 — Growth / BM UX

- Weekly Challenge
- Standard / Assisted Conversion
- Booster Context
- Rewarded Ad Flow
- Share Deep Link
- Record Room

---

# 30. Asset Scope — MVP Estimate

캐릭터 애니메이션보다 지도·문서·아이콘에 집중한다.

## 30.1 Map

- 서울 Base Map 1970
- 한강 / 주요 수계
- Node Polygon 18~22
- 주요 Road / Bridge / Rail
- 시대 Event Overlay

## 30.2 POI / Property

최소:

- 단독주택
- 연립주택
- 빌라
- 아파트 Low/Mid/High-rise
- 오피스텔
- 회사
- 학교
- 은행
- 복덕방
- 시장
- 공장
- 공사현장
- 버스
- 차량
- 지하철/철도

## 30.3 Editorial

- Newspaper Frame 시대별 2~3종
- Contract Sheet
- Ledger / Record Card
- Stamp / Seal
- Share Card Template

## 30.4 UI

- Status Icons
- Layer Icons
- Standard / Assisted Badge
- Freshness State
- Risk State

---

# 31. Prototype Visual A/B Candidates

Visual Direction 자체도 Greybox 이후 최소 3안 비교를 권고한다.

## A — Pure Cartographic

- 가장 미니멀
- 지도와 정보 우선
- 제작 효율 최고

위험:
- 게임보다 지도앱처럼 보일 수 있음

## B — Cartographic + Editorial — **권고안**

- 지도 + 신문 + 계약서 + 장부
- 시대감과 게임성이 균형

위험:
- Texture와 Decor를 남용하면 가독성 저하

## C — Cartographic + Pixel Accent

- World는 Vector
- 차량/사람/POI 일부만 Pixel-like Sprite

장점:
- 인디게임 감성 추가

위험:
- 스타일 혼합이 어색해질 수 있음

**기본안은 B로 진행하고, C는 제한적 Accent로만 실험한다.**

---

# 32. Visual North Star

게임의 최종 인상은 다음 한 문장으로 정의한다.

> **“1970년의 낡은 서울 지도를 펼쳐 놓고, 한 직장인의 장부를 적어가며 2026년의 서울까지 살아가는 게임.”**

이 비주얼은 단지 복고풍이어서는 안 된다.

플레이어가 매 5년마다 느껴야 하는 것은:

1. **서울이 커졌다.**
2. **내 이동범위가 달라졌다.**
3. **내 주거가 달라졌다.**
4. **월급보다 자산이 중요해졌다.**
5. **처음 펼쳤던 1970 지도와 전혀 다른 세계가 되었다.**

따라서 UI/Visual의 최우선 Hero Feature는 **도시와 인생의 동시 변화**다.

---

# 33. Open Questions

## Visual

1. 1970 Base Map을 어느 정도 실지도 형태로 단순화할지
2. 지도 Top-down 90° vs 약한 2.5D Tilt를 어느 화면까지 허용할지
3. 시대 Surface Change를 몇 단계로 나눌지
4. 실제 사진자료 사용 여부와 저작권 정책
5. 신문·지도 Texture의 역사 고증 강도
6. Property Illustration의 추상화 레벨
7. Pixel Accent를 일부 POI/Vehicle에 허용할지

## UX

8. Context Panel 고정폭 vs 상황별 확장폭
9. Landscape 한손 사용을 어디까지 고려할지
10. Quick Scenario에서 Year End를 얼마나 Skip 가능하게 할지
11. 계약화면의 상세 금융정보 Depth
12. Map Label 자동충돌 처리 방식
13. 초기 Tutorial의 최소 개입량

## Growth

14. Weekly Challenge를 Lobby의 어느 우선순위에 둘지
15. Standard→Assisted 전환 문구 A/B
16. Booster Context 노출 빈도
17. Share Card 비율 9:16 / 1:1 / 16:9 중 우선순위

---

# 34. Next Deliverables

이 문서 승인 후 다음 순서로 진행한다.

### D1 — High-Fidelity Key Screen Mock
- Title
- Run Setup
- Main Map
- Property / Contract
- 5-Year Settlement
- Final Ending

### D2 — Component Inventory
- Status Bar
- Context Panel
- Sheet
- Card
- Badge
- Map Marker
- Layer Button
- Risk Alert

### D3 — Three.js Map Prototype
- Pan / Zoom
- Node Select
- Home / Work
- Transport Layer
- Event Line Animation
- 1970→1975 Map Delta

### D4 — Visual Bible v0.1
- Typography
- Palette
- Grid
- Texture
- Icon
- Motion
- Era Surface Rules

---

**Version:** UI/UX Screen Specification v0.1  
**Based on:** PRD v0.5 / GDD v0.4  
**Recommended Visual Direction:** 2D Retro Cartographic + Editorial UI + Three.js 2.5D Map  
**Next:** 6 Key Screen High-Fidelity Mock → Three.js Map Prototype → Visual Bible
