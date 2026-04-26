# 013. Intraday VWAP Pullback, Retest Breakout, and RSI Divergence Reversal

## 1. 출처
- 채널/작성자: 슈퍼트레이더
- 제목: 거래량 보는법 모르는 초보 투자자도 가능한 세력의 5분봉 단타 매매법
- URL: https://www.youtube.com/watch?v=FHSjShoAaUw
- 수집일: 2026-04-27
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/FHSjShoAaUw.txt`
- 주요 근거 구간: 11:50~16:21 VWAP 눌림·돌파·반전 규칙, 17:00~22:25 Super VWAP 밴드 운영 규칙

## 2. 전략 요약
- 한 문장: 장중 VWAP 위/아래의 주도권을 먼저 판정한 뒤, VWAP 재접근·돌파 후 재테스트·RSI 다이버전스 확인 구간에서 5분봉 단타 진입을 수행하는 양방향 가격/거래량 평균 전략입니다.
- 자산군: 국내주식, 미국주식, 코인
- 시간프레임: 5분봉 중심, 15분봉 보조 가능
- 전략 유형: 매수 전략 + 매도/숏 전략 / VWAP 눌림·돌파·반전

## 3. 매수 조건
### A. VWAP 눌림 매수
1. 장 초반 가격이 VWAP 위를 계속 유지하거나, VWAP 아래로 내려갔다가 첫 5~6개 5분봉 안에 VWAP 위로 회복합니다.
2. 이후 가격이 VWAP 근처까지 눌립니다.
3. VWAP와 이전 지지 가격대가 겹치는 구간이면 우선합니다.
4. 진입 확인은 다음 중 하나 이상입니다.
   - 하락 추세선 상향 돌파
   - 이전 단기 고점 돌파
   - 해머형, 상승 장악형 등 상승 반전 캔들
   - VWAP 하향 이탈 시도 실패 후 긴 아래꼬리로 회복

### B. VWAP 돌파 후 재테스트 매수
1. 가격이 큰 거래량으로 VWAP를 상향 돌파합니다.
2. 돌파 후 VWAP 근처로 되돌림이 발생합니다.
3. 되돌림 저점이 이전 저점보다 높게 형성됩니다.
4. 가격이 다시 직전 고점을 돌파할 때 진입합니다.

### C. VWAP + RSI 다이버전스 반전 매수
1. 가격은 VWAP보다 상당히 아래에 있고 저점은 낮아지지만 RSI 저점은 높아지는 상승 다이버전스가 발생합니다.
2. 이후 가격이 VWAP 위로 회복합니다.
3. 중요 저항선 또는 단기 구조선을 상향 돌파하는 캔들에서 진입합니다.

## 4. 매도/숏 조건
### A. VWAP 하향 돌파 후 재테스트 숏
1. 가격이 VWAP 아래로 큰 거래량과 함께 이탈합니다.
2. VWAP 근처까지 반등하지만 회복하지 못합니다.
3. 반등 이후 다시 하락 신호가 나오면 숏 진입합니다.

### B. VWAP 과열 반전 숏
1. 가격이 VWAP보다 상당히 높게 이격되어 있고 RSI 약세 다이버전스가 발생합니다.
2. 가격이 VWAP 또는 단기 지지선을 하향 이탈합니다.
3. 중요 구조선 하향 돌파 캔들에서 숏 진입합니다.

### C. Super VWAP 밴드 역추세 단타
1. 가격이 최상단/과열 구간에서 강세 구간으로 내려오는 캔들에서 숏 진입 후보입니다.
2. 가격이 하단/침체 구간에서 지지를 확인하면 롱 진입 후보입니다.

## 5. 손절 조건
- VWAP 눌림 롱: VWAP 아래 또는 확인 캔들의 저점 아래.
- VWAP 재테스트 롱: 되돌림 저점 아래.
- VWAP 숏: VWAP 위 또는 반등 고점 위.
- RSI 다이버전스 반전: 다이버전스 기준 스윙 저점/고점 이탈 시 손절.
- Super VWAP: 롱은 전저점 이탈, 숏은 전고점 돌파 시 손절.

## 6. 익절 조건
- VWAP 눌림 롱: 종가가 VWAP를 하향 이탈할 때 청산하거나 2R에서 일부 익절.
- VWAP 재테스트: 손절폭 대비 2R을 기본 목표로 설정합니다.
- Super VWAP 밴드형:
  - 롱: 중심선 도달 시 50% 익절, 상단/과열 구간 도달 시 잔여 익절.
  - 숏: 중심선 도달 시 50% 익절, 하단/침체 구간 도달 시 잔여 익절.
- 장 마감 또는 Super VWAP 일중 세션 종료 시 남은 포지션 전량 청산합니다.

## 7. 필터 조건
- 시간대: 국내주식 5분봉 기준 첫 5~6개 캔들 안 VWAP 회복 여부를 당일 롱 우위 판정에 사용합니다.
- 거래량: VWAP 돌파는 최근 20캔들 평균 거래량 이상 또는 당일 평균보다 큰 거래량을 요구합니다.
- 변동성: 장대 양봉/음봉이 연속 출현하고 밴드 기울기가 급격히 벌어지는 구간은 진입 회피합니다.
- 시장 방향: 지수 상승일은 VWAP 위 눌림 매수, 지수 하락일은 VWAP 아래 반등 숏 우선.
- 종목 선정: 당일 거래대금 상위, 시초 강세/약세가 뚜렷한 종목, 뉴스/테마 종목.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간~높음
- 가능한 이유: VWAP, RSI, 거래량, 2R, VWAP 이탈은 수치화 가능합니다.
- 어려운 부분: 상승 장악형/해머형은 정의 가능하지만 “중요 지지선”, “추세선 돌파”, Super VWAP의 정확한 공식은 추가 정의가 필요합니다.

## 9. 기계화 규칙 초안
```text
vwap = intraday cumulative(price * volume) / cumulative(volume)
rsi = RSI(close, 14)
opening_bias_long = all(close[0:5] > vwap[0:5]) or (min(close[0:6] < vwap[0:6]) and close[5] > vwap[5])

pullback_to_vwap = abs(close - vwap) / ATR(14) < 0.3
bull_reversal = close > prior_swing_high or candle_pattern in [hammer, bullish_engulfing]
long_entry = opening_bias_long and pullback_to_vwap and bull_reversal
long_stop = min(vwap, signal_low)
long_exit = close < vwap or price >= entry + 2R

breakout_long = close crosses above vwap and volume > SMA(volume,20)
retest_long = breakout_recent and low <= vwap * 1.002 and close > vwap and close > prior_swing_high

rsi_bull_div = price_lower_low and rsi_higher_low
reversal_long = rsi_bull_div and close > vwap and close > structure_high
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 5분봉 VWAP는 기관/외국인 평균단가 추정치로 해석하기 쉬워 당일 주도주 눌림 매수 필터로 적합합니다.
- 코인: 24시간 시장이라 세션 VWAP 기준을 UTC 00:00, 한국시간 09:00, 미국장 시작 등 여러 기준으로 테스트해야 합니다.
- 국내주식은 공매도 제약 때문에 숏 규칙은 인버스 ETF, 선물 또는 롱 청산/회피 신호로 별도 분리합니다.

## 11. 리스크/반대 시나리오
- VWAP 터치만으로 진입하면 추세 붕괴 초입을 눌림으로 오인할 수 있습니다.
- 강한 추세일수록 VWAP까지 되돌림이 오지 않아 기회비용이 발생합니다.
- 장 초반 VWAP는 거래량 누적이 적어 작은 체결에도 급변할 수 있습니다.
- Super VWAP는 공개 공식이 불명확해, 동일 재현 전에는 보조 아이디어로 취급해야 합니다.

## 12. 후속 검증 질문
1. 국내주식 5분봉에서 첫 5~6개 캔들 VWAP 회복 조건이 당일 방향 예측력을 갖는가?
2. VWAP 눌림 후 “이전 고점 돌파” 확인을 넣으면 승률과 손익비가 어떻게 변하는가?
3. RSI 다이버전스 + VWAP 회복은 단독 VWAP 반전보다 기대값이 높은가?
4. 코인은 세션 VWAP 시작 시각별 성과 차이가 큰가?
