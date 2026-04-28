# 019. Opening Range Reversal: 약한 돌파/꼬리 거절 스캘핑

## 1. 출처
- 채널/작성자: Trade with Pat
- 제목: Simple A+ Scalping Strategy You’ve NEVER Seen
- URL: https://www.youtube.com/watch?v=IDqjEOJ_ps4
- 수집일: 2026-04-29
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/IDqjEOJ_ps4.txt`

## 2. 전략 요약
- 한 문장: 뉴욕장 초반 75분 범위를 기준으로 강한 변위 돌파가 아닌 약한 돌파/꼬리 거절이 나오면 범위 안쪽으로 되돌리는 평균회귀 스캘핑을 시도하는 전략입니다.
- 자산군: 원 영상은 EUR/USD 중심, 코인·지수선물·국내주식 장초 변동성 구간에 응용 가능
- 시간프레임: 5분봉, 기준 range는 08:00~09:15 UTC-4
- 전략 유형: 양방향 전략 / 매수·매도 모두 가능 / ORB 역추세 평균회귀

## 3. 매수 조건
1. 지정 세션의 opening range를 산출합니다. 원 규칙은 08:00~09:15 UTC-4의 고가·저가입니다.
2. 5분봉 기준 가격이 range 하단을 살짝 이탈하되, 강한 장대 음봉 종가 돌파가 아니라 다음 중 하나를 보입니다.
   - 하단 이탈 후 곧바로 range 안으로 종가 복귀
   - 하단 아래 긴 아래꼬리 형성 후 종가가 range 하단 근처/상단에 위치
3. 이탈 캔들이 큰 displacement를 만들지 않아야 합니다.
4. 하단을 지지선으로 해석하고 range 내부 방향으로 롱 진입합니다.

## 4. 매도/숏 조건
1. 가격이 opening range 상단을 살짝 이탈합니다.
2. 강한 장대 양봉 종가 돌파가 아니라 약한 돌파, range 내부 복귀, 또는 위꼬리 거절을 보입니다.
3. 상단을 저항선으로 해석하고 range 내부 방향으로 숏 진입합니다.

## 5. 손절 조건
- 기본형: 매수는 rejection wick 저점 또는 range 하단 이탈폭의 저점 아래, 매도는 rejection wick 고점 또는 range 상단 이탈폭의 고점 위.
- 기계화 초안: 손절폭은 `max(최근 rejection candle range, ATR(14)*0.5)` 이상으로 설정해 미세 노이즈를 피합니다.
- 원 영상에는 불리하게 움직일 때 grid/scale-in으로 두 번째 포지션을 더 크게 추가하는 방식이 언급되지만, 이는 손실 확대 위험이 커서 별도 고위험 변형으로 분리해야 합니다.

## 6. 익절 조건
- 원 영상 사례는 평균 8.57 pips, 예시 5.1~16.7 pips의 빠른 수익을 목표로 제시합니다.
- 기계화 초안:
  - 1차 목표: range 중앙값 또는 고정 R 1.0~1.5R
  - 2차 목표: range 반대편 50~80% 지점
  - 진입 후 2~3개 5분봉 내 유리하게 진행되지 않으면 시간 청산을 검토합니다.

## 7. 필터 조건
- 시간대: 원본은 09:15 UTC-4 이후 EUR/USD. 국내주식은 09:00~09:15 range, 코인은 거래량이 커지는 UTC/미국장 개장 전후 range로 재정의 필요.
- 거래량: range 이탈 시 거래량 급증이 동반되면 trend run 가능성이 커져 제외하거나 별도 돌파 전략으로 분류합니다.
- 변동성: range 폭이 과도하게 넓으면 목표 pips 대비 손절이 커져 제외합니다.
- 시장 방향: 강한 상위 추세/뉴스가 있는 날은 평균회귀 실패 가능성이 큽니다.
- 종목 선정: 평균회귀 가능한 유동성 높은 종목, 스프레드가 좁은 코인/FX/대형주가 우선입니다.

## 8. 백테스트 가능성
- 등급: 정량화 가능에 가까운 부분 정량화 가능
- 구현 난이도: 중간
- 이유: range, weak break, wick rejection, 고정 시간 청산은 정량화 가능하지만, “약한 돌파”와 “displacement 부재”의 임계값 정의가 필요합니다.

## 9. 기계화 규칙 초안
```text
range_start=08:00, range_end=09:15 UTC-4
ORH=max(high), ORL=min(low)
for each 5m candle after range_end:
  upside_probe = high > ORH and close <= ORH + 0.25*(ORH-ORL)
  downside_probe = low < ORL and close >= ORL - 0.25*(ORH-ORL)
  weak_body = abs(close-open) < 0.6*ATR(14)
  wick_reject_short = high > ORH and (high-max(open,close)) > 0.4*(high-low)
  wick_reject_long = low < ORL and (min(open,close)-low) > 0.4*(high-low)
  if downside_probe and weak_body and wick_reject_long: long
  if upside_probe and weak_body and wick_reject_short: short
stop = rejection_extreme +/- buffer
partial/exit = range_mid or 1.2R; time_stop=3 bars
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 09:00~09:10 또는 09:00~09:15 range 설정 후, 장초 VI/뉴스 급등주는 제외하고 유동성 상위 종목의 range 하단/상단 fake break 평균회귀를 검증합니다.
- 코인: BTC/ETH 및 거래대금 상위 알트에서 미국장 전후 75분 range를 사용하되, funding/뉴스 이벤트 구간은 제외합니다.
- 24시간 코인은 세션 정의가 핵심이므로 Asia/London/NY 세션별로 별도 파라미터를 검증합니다.

## 11. 리스크/반대 시나리오
- 약한 돌파로 보였으나 이후 강한 trend run으로 전환될 수 있습니다.
- grid/scale-in 변형은 마틴게일 성격이 있어 단일 손절형과 분리해 검증해야 합니다.
- range 폭이 좁은 날은 수수료·슬리피지가 기대값을 잠식할 수 있습니다.
- 국내주식 장초 호가 공백, VI, 시초가 갭은 실제 체결가를 악화시킬 수 있습니다.

## 12. 후속 검증 질문
1. weak breakout의 최적 정의는 종가 복귀, wick 비율, ATR 대비 body 중 무엇이 가장 안정적인가?
2. trend run을 피하기 위한 거래량/상위 추세 필터가 필요한가?
3. range 중앙 청산과 반대편 청산 중 어떤 방식이 기대값과 승률 균형이 좋은가?
4. grid/scale-in 없이 단일 손절만 적용해도 전략성이 유지되는가?
