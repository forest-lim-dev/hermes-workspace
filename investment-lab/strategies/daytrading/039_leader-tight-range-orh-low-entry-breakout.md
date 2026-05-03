# 039. 강한 주도주 MA 눌림·타이트 레인지 ORH 저위험 돌파

## 1. 출처
- 채널/작성자: Kristjan Kullamägi / Qullamaggie
- 제목: Some good Tweetstorms
- URL: https://qullamaggie.com/some-good-tweetstorms/
- 수집일: 2026-05-04
- 원문 위치: `sources/articles/raw/2026-05-04_qulla_tweetstorms.txt`
- 근거 구절: 댓글 중 “big move, pullback on a 10, 20 or 50 rising moving average, ... going sideways, build higher lows in a tight range, and breakout ... buy on the 1 minute, 5 minute or 60 minute opening range high with stop on the low of the days.”

## 2. 전략 요약
- 한 문장: 큰 상승을 만든 주도주가 상승 10/20/50MA 위로 눌림 후 타이트 레인지와 고저점 상승을 만들 때, 1분·5분·60분 opening range high 돌파를 저위험 진입점으로 사용하는 롱 돌파 전략입니다.
- 자산군: 주식 중심. 국내주식 테마주/거래대금 상위주와 코인 강세 알트에 응용 가능.
- 시간프레임: 일봉/60분 추세 필터 + 1분/5분/60분 ORH 진입.
- 전략 유형: 매수 전략, 모멘텀 continuation breakout.

## 3. 매수 조건
1. 대상 종목이 최근 큰 상승(big move)을 보임: 예) 최근 5~20일 수익률 상위 5~10%, 20일 신고가, 혹은 전일 대비 +10% 이상 급등.
2. 10MA/20MA/50MA 중 최소 1개 이상이 상승 기울기이며, 가격이 해당 이동평균 근처로 눌림.
3. 눌림 이후 가격이 MA를 타고 횡보하며 변동성이 축소: 예) 최근 N봉 range가 이전 N봉 range 대비 50~70% 이하.
4. 타이트 레인지 내부에서 higher lows 형성: 최소 2개 이상의 저점이 상승.
5. 진입 트리거: 1분/5분/60분 ORH 또는 타이트 레인지 상단을 거래량 증가와 함께 돌파.
6. 진입 위치가 당일 저점 대비 과도하게 멀지 않아야 함. 원문 취지는 “low entry point on fast moving stocks”.

## 4. 매도/숏 조건
- 본 문서는 롱 continuation 전략입니다. 숏은 기본 전략 대상이 아닙니다.
- 단, 돌파 실패 후 ORH 하향 재이탈과 VWAP/MA 이탈이 동시에 발생하면 롱 청산 또는 관망 신호로 사용합니다.

## 5. 손절 조건
- 기본 손절: 당일 저점(low of day) 또는 타이트 레인지 저점 아래.
- 공격적 손절: 돌파 기준봉 저점 또는 ORH 재이탈 후 1~2봉 내 회복 실패.
- 손절폭 제한: 진입가 대비 손절폭이 평균 5분 ATR의 1.5~2배를 초과하면 진입 제외.

## 6. 익절 조건
- 1차: 2R 또는 직전 고점/전일 고점.
- 2차: 신고가 확장 시 5분 10/20EMA 이탈, parabolic extension, 또는 추세선 이탈까지 트레일링.
- 국내주식에서는 VI/상한가 근접, 호가 공백 확대 시 분할 청산 규칙 필요.

## 7. 필터 조건
- 시간대: ORH는 장초반 1분·5분·60분 범위를 모두 실험. 국내주식은 09:00~10:00 형성 ORH 우선.
- 거래량: 돌파봉 거래량이 직전 20개 1분/5분봉 평균 대비 1.5~3배 이상.
- 변동성: prior big move 이후 변동성 수축이 확인될수록 가점.
- 시장 방향: 지수/섹터가 강하거나 최소한 급락 중이 아닐 것.
- 종목 선정: 최근 주도 테마, 거래대금 상위, 신고가 근처, float/유통주식이 가벼운 종목을 우선.

## 8. 백테스트 가능성
- 등급: 정량화 가능
- 구현 난이도: 중간
- 이유: 큰 상승, 상승 MA, volatility contraction, higher lows, ORH 돌파, low-of-day stop 모두 OHLCV로 정의 가능합니다. 다만 “주도주”와 “타이트함”의 파라미터 탐색이 필요합니다.

## 9. 기계화 규칙 초안
```text
Universe = KOSDAQ/KOSPI 거래대금 상위 300 또는 코인 거래대금 상위 50
1) leader_filter: 10일 수익률 상위 10% AND 종가 > 20MA AND 20MA slope > 0.
2) pullback_filter: 당일/최근 가격이 rising 10/20/50MA 중 하나의 ±2ATR 이내.
3) tight_range: 최근 12개 5m봉 high-low range <= 이전 24개 5m봉 range의 0.65배.
4) higher_lows: 최근 swing low 2개 이상 상승.
5) ORH_5m = 첫 5분봉 고가, ORH_60m = 첫 60분봉 고가.
6) entry = close crosses above ORH or range_high with volume >= 2*avg_volume_20.
7) stop = min(low_of_day, range_low) - tick_buffer.
8) target = 2R first, trail remainder below 5m 20EMA or prior 5m swing low.
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 상한가/VI 제도가 있어 돌파 체결 직후 슬리피지가 큼. ORH 돌파 전 타이트 레인지 폭과 예상 손절폭이 좁은 종목만 선별.
- 코인: 24시간 거래라 “opening range”를 한국장 09:00, 런던 16:00, 뉴욕 22:30/23:30 KST 등 유동성 시작 구간으로 재정의.
- 테마 순환이 빠른 국장에서는 같은 테마 내 대장주만 허용하고 후발주는 돌파 실패율 별도 검증.

## 11. 리스크/반대 시나리오
- 큰 상승 이후 분배 구간을 continuation으로 오판하면 고점 돌파 실패 손절이 잦아집니다.
- ORH가 너무 높게 형성되면 “low entry” 원칙과 충돌합니다.
- 지수 급락일에는 주도주도 레인지 상단 돌파 후 즉시 되밀릴 수 있습니다.
- 댓글 기반 아이디어라 원문 저자의 공식 세부 규칙이 아니며, 별도 검증이 필요합니다.

## 12. 후속 검증 질문
1. big move를 1일/5일/20일 수익률 중 무엇으로 정의할 때 단타 기대값이 높은가?
2. ORH는 1분, 5분, 60분 중 어떤 기간이 국내주식에 적합한가?
3. 손절을 low of day로 둘 때 손절폭이 커지는 문제를 ATR 제한으로 해결할 수 있는가?
4. higher lows를 스윙 알고리즘으로 정의할 때 최소 저점 간격은 몇 봉이 적절한가?
