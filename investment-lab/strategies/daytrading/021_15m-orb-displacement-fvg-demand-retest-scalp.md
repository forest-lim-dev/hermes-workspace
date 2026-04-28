# 021. 첫 15분 캔들 ORB Displacement + FVG/Demand Retest Scalping

## 1. 출처
- 채널/작성자: Trade with Pat
- 제목: The EASIEST Scalping Strategy I Trade DAILY
- URL: https://www.youtube.com/watch?v=j5v9OlQ_gsY
- 수집일: 2026-04-29
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/j5v9OlQ_gsY.txt`

## 2. 전략 요약
- 한 문장: 각 세션의 첫 15분봉 고저 범위를 만든 뒤, 5분봉에서 강한 변위 돌파가 발생하면 FVG 또는 demand/supply zone 되돌림과 engulfing 확인으로 추세 지속 스캘핑을 수행하는 전략입니다.
- 자산군: Forex, futures, gold, indices 예시; 코인·국내주식에 응용 가능
- 시간프레임: 15분봉 range 설정, 5분봉 실행, 1시간봉 지지/저항 confluence
- 전략 유형: 양방향 전략 / ORB trend continuation / pullback entry

## 3. 매수 조건
1. 거래 세션의 첫 15분 캔들 고가와 저가를 range high/low로 지정합니다.
2. 5분봉으로 전환한 뒤, range high 위로 큰 양봉이 종가 돌파하며 displacement를 생성합니다.
3. 돌파 과정에서 FVG 또는 demand zone을 식별합니다.
   - FVG: 강한 상승 중 비효율/imbalance 구간
   - Demand: 장대 상승 직전 마지막 음봉 또는 상승이 시작된 박스
4. 즉시 추격하지 않고 가격이 FVG/demand로 되돌아오길 기다립니다.
5. 되돌림 구간에서 bullish engulfing 등 momentum confirmation이 종가로 완성되면 롱 진입합니다.
6. 1시간봉에서 저항 돌파 후 지지 전환, 또는 상위 구조 고점 돌파가 있으면 가점합니다.

## 4. 매도/숏 조건
1. 첫 15분 range low 아래로 5분봉 장대 음봉이 종가 이탈하며 displacement를 생성합니다.
2. 돌파 과정에서 FVG 또는 supply zone을 식별합니다.
3. 가격이 supply/FVG로 되돌아온 뒤 bearish engulfing이 나오면 숏 진입합니다.
4. 1시간봉 저항 반응, 지지 이탈 후 저항 전환이 있으면 가점합니다.

## 5. 손절 조건
- 매수: demand/FVG 하단, ORB range 하단, 또는 최근 swing low 아래. 영상 예시에서는 range 바로 아래 stop이 언급됩니다.
- 매도: supply/FVG 상단, ORB range 상단, 또는 최근 swing high 위.
- 손절이 너무 타이트하면 obvious support sweep에 털릴 수 있다는 예시가 있으므로, `zone extreme + ATR buffer`를 검증해야 합니다.

## 6. 익절 조건
- 영상 예시: 중간 저항에서 20~30% 부분익절, 손절 본전 이동, 최종 목표는 trend continuation 및 다음 구조 레벨.
- 예시 R/R: 약 1.5R, 2.5R 사례가 언급됩니다.
- 기계화 초안:
  - 1차: 최근 5분봉 구조 고점/저점 또는 1R
  - 2차: 2R 또는 다음 1시간봉 supply/demand
  - 부분익절 후 잔여는 trailing swing stop 또는 break-even stop 적용

## 7. 필터 조건
- 시간대: “어떤 세션의 첫 15분”이 핵심입니다. 영상은 09:30, 02:00 Europe/London premarket, 08:00 US session 예시를 사용합니다.
- 거래량: displacement 캔들은 직전 평균 대비 거래량 증가를 요구하는 것이 좋습니다.
- 변동성: 첫 15분 range가 너무 좁으면 fake break가 많고, 너무 넓으면 손절 대비 목표가 불리합니다.
- 시장 방향: 1시간봉 지지/저항 돌파·리테스트와 일치하면 우선순위를 높입니다.
- 종목 선정: 유동성 높은 종목, 명확한 세션 개념이 있는 상품, 스프레드/수수료가 낮은 상품.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간
- 이유: 첫 15분 range, displacement, engulfing, R/R은 정량화 가능하나 FVG/demand/supply zone 정의와 상위 시간봉 confluence 표준화가 필요합니다.

## 9. 기계화 규칙 초안
```text
session_open = configurable
OR_15m_high = high(first 15m candle)
OR_15m_low  = low(first 15m candle)
LTF = 5m

long_break = close > OR_15m_high and body > 0.8*ATR(14) and close_position_in_range > 0.7
bullish_displacement = count_consecutive_green >= 2 or body > 1.2*avg_body(20)
FVG = low[current] > high[current-2]  # bullish 3-candle imbalance variant
Demand = last bearish candle before bullish_displacement
POI = nearest(FVG or Demand)
entry_long = price_retests(POI) and bullish_engulfing(close)
stop_long = min(POI_low, OR_15m_low, recent_swing_low) - 0.1*ATR
TP1 = 1R or nearest_resistance; TP2 = 2R or HTF_supply

short rules are symmetric.
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 09:00~09:15 첫 15분봉 range를 기준으로, 09:15 이후 거래대금 상위 종목의 강한 돌파-되돌림-재상승 구조를 탐색합니다. VI 발동 종목과 호가 공백이 큰 저유동 종목은 제외합니다.
- 코인: BTC/ETH는 Asia/London/NY 세션별 첫 15분 range를 분리해 테스트합니다. 알트코인은 거래대금·스프레드·상장뉴스 필터가 필요합니다.
- 국내주식에서는 상위 시간봉 confluence를 전일 고가/저가, 당일 VWAP, 전일 종가로 대체할 수 있습니다.

## 11. 리스크/반대 시나리오
- 첫 15분 range 돌파가 많아도 실제 trend continuation이 약하면 손익비가 급격히 악화됩니다.
- FVG/demand zone을 너무 넓게 잡으면 손절이 커지고, 너무 좁게 잡으면 정상적인 liquidity sweep에 손절될 수 있습니다.
- 강한 갭/뉴스 종목은 되돌림 없이 진행해 미체결 기회비용이 발생합니다.
- 국내주식은 장초 체결 지연·VI·호가 공백이 백테스트와 실거래 괴리를 만들 수 있습니다.

## 12. 후속 검증 질문
1. 첫 15분 range와 첫 5/10/30분 range 중 어느 정의가 국내주식/코인에 더 적합한가?
2. displacement를 body/ATR, 연속 캔들 수, 거래량 중 어떤 기준으로 정의할 때 안정적인가?
3. FVG와 demand/supply 중 어느 POI가 더 좋은 기대값을 보이는가?
4. 부분익절+본전 이동이 순 기대값을 개선하는가, 아니면 수익의 오른쪽 꼬리를 줄이는가?
