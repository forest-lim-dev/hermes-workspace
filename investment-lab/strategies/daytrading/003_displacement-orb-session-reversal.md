# 전략 후보: Displacement ORB + Asia/London Session Reversal

## 1. 출처
- 채널/작성자: Trade with Pat
- 제목: “The ONLY Day Trading Strategy I'll use ALL 2026 (Backtested 1000 Times)”
- URL: https://www.youtube.com/watch?v=E3McKlAp3qk
- 수집일: 2026-04-25
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/E3McKlAp3qk.txt`

## 2. 전략 요약
- 한 문장: 뉴욕장 첫 15분 opening range를 기준으로 강한 종가 돌파와 demand/supply 또는 FVG 되돌림을 기다리되, 아시아 박스와 런던 방향성을 이용해 뉴욕 reversal 방향만 선별하는 ORB 전략입니다.
- 자산군: 원 영상은 Forex/지수 CFD 성격. 국내주식·코인은 세션 정의를 바꿔 실험 필요.
- 시간프레임: 세션 분석 15m, ORB/진입 5m.
- 전략 유형: 양방향 전략, ORB + liquidity sweep + reversal.

## 3. 매수 조건
1. 아시아 세션이 비교적 좁은 range를 형성합니다.
2. 런던 세션에서 아시아 저점 유동성을 sweep하고 하방으로 강한 push가 발생합니다.
3. 뉴욕 세션에서 reversal long bias를 설정합니다. 단, 런던이 아시아 상·하단을 모두 sweep한 경우 continuation 가능성이 있어 bias를 약화하거나 제외합니다.
4. 뉴욕 정규장 09:30~09:45 첫 15분 캔들의 고가/저가를 opening range로 표시합니다.
5. 5분봉에서 range 상단을 강한 body와 종가로 돌파해야 합니다. wick 돌파만으로는 무효입니다.
6. 돌파 과정에서 demand zone 또는 fair value gap이 생성되어야 합니다.
7. 가격이 demand/FVG로 되돌아와 지지 반응을 보이고, 가능하면 bullish engulfing body가 확인되면 매수합니다.

## 4. 매도/숏 조건
1. 아시아 세션이 range를 형성합니다.
2. 런던 세션에서 아시아 고점 유동성을 sweep하고 상방 push가 발생합니다.
3. 뉴욕 세션에서 reversal short bias를 설정합니다.
4. 09:30~09:45 opening range 하단을 5분봉 종가로 강하게 이탈합니다.
5. 이탈 과정에서 supply zone 또는 bearish FVG가 생성됩니다.
6. 가격이 supply/FVG로 되돌아와 저항 반응 또는 bearish engulfing을 보이면 숏 진입합니다.

## 5. 손절 조건
- demand/supply zone 반대편 또는 FVG 중단/하단·상단 아래/위.
- 원 영상 예시에서는 FVG 진입 시 midline 근처 stop도 언급하지만, 백테스트에서는 “FVG 전체 이탈”과 “midline 이탈”을 분리해 비교해야 합니다.

## 6. 익절 조건
- 1.5R~2.2R 범위의 고정 R 목표.
- 아시아 range 반대편 liquidity level 또는 직전 구조 고점/저점.
- 런던이 이미 양쪽 유동성을 모두 sweep한 날은 아시아 반대편까지의 목표를 보수적으로 낮춥니다.

## 7. 필터 조건
- 시간대: 뉴욕 09:30~09:45 ORB, 진입은 가급적 09:45 이후 초기 구간. 원 영상은 뉴욕 세션 중심.
- 거래량: 원 영상은 명시적 거래량 조건은 없으나 “displacement”를 큰 candle body로 대체 가능.
- 변동성: opening range가 지나치게 좁으면 속임수, 지나치게 넓으면 손익비 악화 가능.
- 시장 방향: Asia range → London push → NY reversal 패턴이 핵심 방향 필터.
- 종목 선정: 세션성이 있는 Forex/Index에 적합. 국내주식은 장전 세션이 제한적이므로 변형 필요.

## 8. 백테스트 가능성
- 등급: 정량화 가능에 가까운 부분 재량
- 구현 난이도: 중간
- 정량화 쉬운 요소: ORB range, 종가 돌파, candle body 크기, FVG, Asia high/low sweep, London push 방향.
- 추가 정의 필요 요소: tight Asian range 임계값, London push 강도, “displacement” 최소 body/ATR, demand/supply zone.

## 9. 기계화 규칙 초안
1. 세션 정의: Asia, London, New York을 거래소/자산별로 고정합니다.
2. Asia range 폭이 최근 20일 동일 세션 range의 p번째 분위수 이하이면 valid accumulation으로 판정합니다.
3. London push 방향은 London close와 Asia range 이탈 방향, 또는 London 세션 누적수익률로 판정합니다.
4. London이 Asia low만 sweep하고 하락 마감하면 NY long bias, Asia high만 sweep하고 상승 마감하면 NY short bias. 양쪽 sweep은 별도 continuation/skip 케이스로 분류합니다.
5. NY 09:30~09:45 range를 만들고, 5m 종가가 bias 방향으로 range를 돌파해야 합니다.
6. Displacement candle은 body >= 최근 20개 5m body 평균의 k배 및 종가가 range 밖에 위치하는 조건으로 정의합니다.
7. FVG는 3-candle gap 규칙으로 정의하고, demand/supply는 임펄스 직전 반대색 캔들 range로 정의합니다.
8. 되돌림이 FVG/demand/supply에 닿은 뒤 engulfing 또는 zone hold 후 재돌파 시 진입합니다.
9. SL은 zone 반대편, TP는 1.5R/2R/Asia opposite liquidity를 각각 테스트합니다.

## 10. 국내주식/코인 적용 아이디어
- 국내주식: Asia/London 구조를 그대로 쓰기 어렵습니다. 대체안은 전일 종가 이후 야간 해외지수/선물 방향, 시초가 갭, 09:00~09:15 ORB를 결합하는 방식입니다. 예: 전일 미장/야간선물이 과도하게 한쪽으로 움직인 뒤 국내 장초반 반대 ORB 돌파가 나오는지 검증.
- 코인: 24시간 거래라 세션 정의가 가능해 원형에 더 가깝습니다. Asia=KST 09:00 이전 박스, London/NY는 UTC 기준으로 구분하고 BTC/ETH 및 거래대금 상위 알트에서 long/short 양방향 테스트가 가능합니다.

## 11. 리스크/반대 시나리오
- 뉴욕 reversal 패턴은 모든 날에 발생하지 않습니다. 런던이 상·하단을 모두 sweep한 날은 continuation이 우세할 수 있다고 원 영상에서도 언급합니다.
- ORB 종가 돌파 후 되돌림이 없으면 신호가 누락됩니다.
- FVG/demand 재테스트는 주관성이 있어 정의 변경에 따라 성과가 크게 바뀔 수 있습니다.
- 세션 시간이 DST와 자산별 거래시간에 민감합니다.

## 12. 후속 검증 질문
- Asia range 폭 필터를 넣으면 ORB 단독 대비 손익비가 개선되는가?
- London one-side sweep과 both-side sweep의 NY 성과 차이는 유의미한가?
- FVG entry와 demand/supply entry 중 어느 쪽이 drawdown이 낮은가?
- 코인에서 KST 09:00/런던/뉴욕 세션 중 어느 조합이 가장 안정적인가?
