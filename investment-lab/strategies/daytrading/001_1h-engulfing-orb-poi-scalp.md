# 전략 후보: 1H Engulfing Bias + 15분 Opening Range Breakout + POI Retest Scalping

- 상태: 1차 추출 완료
- 출처: Trade with Pat, “3 Step BEGINNER Scalping Strategy (500 Trade BACKTEST)”
- URL: https://www.youtube.com/watch?v=kFyD3H6I1I8
- 원문 transcript: `02_raw_transcripts/youtube/YT-06_kFyD3H6I1I8_3-step-beginner-scalping.txt`
- 자산군: 원 영상은 Forex, NASDAQ, Gold 예시. 국내주식/코인 적용은 별도 검증 필요.
- 시간대: 원 전략은 뉴욕장 기준 09:30~11:00 ET. 국내주식/코인은 장 시작 후 첫 15분 ORB로 변환 가능.

## 1. 핵심 아이디어

장 시작 전 1시간봉 2개로 당일 세션 방향성(bias)을 정하고, 장 시작 후 첫 15분 박스의 방향성 돌파를 확인한 뒤, 즉시 추격하지 않고 수요/공급 구간 또는 지지/저항 재테스트에서 진입하는 스캘핑/단타 전략입니다.

## 2. 매수 조건

### Step 1: 세션 방향성 필터
- 1시간봉 기준 07:00 캔들과 08:00 캔들을 확인합니다. 원 영상 기준 UTC-4, 뉴욕 세션 전.
- 08:00 캔들이 07:00 캔들을 감싸는 bullish engulfing이면 해당 세션은 매수만 고려합니다.
- bearish engulfing이면 매수는 배제하고 매도만 고려합니다.

### Step 2: Opening Range Breakout
- 5분봉 기준 장 시작 후 09:30~09:45, 즉 첫 15분의 고가/저가를 박스로 표시합니다.
- 매수 bias일 때 가격이 opening range 상단을 종가 기준으로 돌파/마감해야 합니다.
- 매도 bias일 때 가격이 opening range 하단을 종가 기준으로 이탈/마감해야 합니다.

### Step 3: POI 재진입
- 돌파 직후 추격 진입하지 않고, 가격이 관심구간(POI)으로 되돌림을 줄 때 진입합니다.
- 매수 POI 후보:
  - 돌파를 만든 수요구간(demand zone)
  - 직전 저항이 지지로 전환된 레벨
  - fair value gap 또는 구조 돌파를 동반한 캔들 구간
- 되돌림 후 POI에서 반응하고, 추가 bullish engulfing 등 모멘텀 확인이 있으면 진입 신뢰도를 높입니다.

## 3. 매도 조건

매수 조건의 대칭입니다.

- 1시간봉 07:00/08:00 bearish engulfing으로 세션 매도 bias 설정
- 5분봉 09:30~09:45 opening range 하단 종가 이탈
- 공급구간(supply zone), 직전 지지→저항 전환 레벨, FVG 등으로 반등 시 숏 진입

## 4. 청산/리스크 관리

- 손절: 매수는 opening range 하단 또는 demand zone 하단 아래. 매도는 range 상단 또는 supply zone 상단 위.
- 익절: 좌측 차트에서 확인되는 supply/demand 또는 큰 반응이 있었던 지지·저항 구간.
- 원 영상 예시의 R/R: 약 2.1~2.3R 사례 제시.
- 시간 종료: 원 전략은 09:30~11:00 ET 집중. 11시 이후에는 진입하지 않거나, 이미 설정된 손절/익절만 유지하는 형태로 설명됨.

## 5. 백테스트 가능성 평가

| 항목 | 평가 | 구현 난이도 |
|---|---:|---:|
| 1H engulfing bias | 높음 | 낮음 |
| 15분 opening range 고저가 | 높음 | 낮음 |
| range 종가 돌파/이탈 | 높음 | 낮음 |
| POI: 직전 저항→지지/지지→저항 | 중간 | 중간~높음 |
| POI: demand/supply zone | 중간~낮음 | 높음 |
| POI: fair value gap | 중간 | 중간 |
| 재테스트 후 engulfing 확인 | 높음 | 낮음~중간 |
| discretionary TP 레벨 | 낮음 | 높음 |

## 6. 백테스트용 규칙화 초안

### 보수형 기계화 버전
1. 기준 타임프레임: 1H, 실행 타임프레임: 5m.
2. 장 시작 전 2개 1H 캔들로 engulfing 판단.
3. 장 시작 후 첫 15분 고가/저가 계산.
4. bias 방향으로 5m 종가가 opening range를 돌파하면 신호 대기 상태 진입.
5. 진입가:
   - 매수: 돌파 후 첫 pullback에서 opening range 상단 ± x bps 또는 직전 돌파 캔들의 50% 되돌림에 limit/market 진입.
   - 매도: 하단 이탈 후 첫 pullback에서 opening range 하단 ± x bps 또는 이탈 캔들의 50% 되돌림.
6. 손절: opposite side of opening range 또는 ATR 기반 buffer.
7. 익절: 고정 2R, 또는 1.5R/2R/3R grid 비교.
8. 시간 필터: 장 시작 후 90분 이내 진입만 허용.

### 재량형 원전략에 가까운 버전
- POI를 supply/demand/FVG/flip level로 탐지하는 별도 알고리즘 필요.
- 익절은 좌측 구조 레벨 기반이므로 룰 정의가 추가로 필요합니다.

## 7. 국내주식/코인 적용 아이디어

### 국내주식
- 1H bias: 08:00/09:00 데이터가 없으므로 전일 종가~당일 장초반 구조로 대체 필요.
- 후보 변환:
  - 전일 마지막 60분봉 + 당일 09:00~10:00 60분봉은 늦어짐.
  - 대신 전일 종가 대비 갭 방향 + 첫 5/15분봉 body engulfing으로 단축형 bias 생성.
- opening range: 09:00~09:15 KST.

### 코인
- 24시간장이므로 “세션”을 임의 지정해야 합니다.
- 후보 세션:
  - 한국 오전 09:00 리셋
  - 미국 주식 개장 22:30/23:30 KST
  - 런던/뉴욕 겹치는 시간
- 코인은 변동성 regime별 성과 차이가 클 수 있어 ATR/거래량 필터 필요.

## 8. 리스크/반대 시나리오

- opening range 돌파 후 재테스트 없이 추세가 진행되면 미체결이 많아질 수 있습니다.
- POI 정의가 재량적이면 백테스트에서 과최적화/후견지명 편향 위험이 큽니다.
- 장초반 뉴스·갭·유동성 이벤트에서 range 돌파가 속임수로 끝날 수 있습니다.
- 영상의 “500회 백테스트”는 원자료가 공개된 것은 아니므로 독립 검증 전까지 주장으로만 취급해야 합니다.

## 9. 다음 검증 질문

- 1H engulfing bias가 실제로 첫 90분 방향성 예측력을 가지는가?
- ORB 단독 대비 bias 필터를 추가했을 때 승률/기대값이 개선되는가?
- POI retest를 단순 OR 상단/하단 retest로 대체해도 성과가 유지되는가?
- TP를 구조 레벨 대신 고정 R-multiple로 바꿨을 때 성과가 안정적인가?
