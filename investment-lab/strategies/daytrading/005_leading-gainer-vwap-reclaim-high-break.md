# 전략 후보: Leading % Gainer VWAP Reclaim + High Break / Dip Bounce

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: “Day Trading the Top 2 Leading % Gainers in the Market”
- URL: https://www.youtube.com/watch?v=atHr4cLbtI0
- 수집일: 2026-04-25
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/atHr4cLbtI0.txt`

## 2. 전략 요약
- 한 문장: 당일 leading percentage gainer 중 뉴스·저유통주·강한 장전 상승 종목을 관찰하다가, 과열 직후가 아니라 VWAP reclaim, 고점 재돌파, 또는 급락 후 반등에서 짧게 진입하는 초단타 전략입니다.
- 자산군: 원 영상은 미국 소형주. 국내주식 테마주/상한가 후보, 코인 급등 알트에 변형 가능.
- 시간프레임: 스캐너/프리마켓 관찰, 1m 및 10초 차트 실행.
- 전략 유형: 매수 전략 중심. 숏은 언급되지 않음.

## 3. 매수 조건
1. 스캐너에서 당일 상승률 상위 종목을 찾습니다.
2. 선호 후보는 뉴스 catalyst, 낮은 float(예: 영상 사례 CPIX 9.1M float), 높은 상대거래량, 장전 또는 장초반 강한 상승이 있는 종목입니다.
3. 과열 구간에서 topping tail/rejection이 연속되면 즉시 추격하지 않습니다.
4. 진입 모델 A — VWAP reclaim:
   - 장전 또는 장초반 급등 후 selloff.
   - 이후 가격이 다시 VWAP 위로 회복합니다.
   - 10초/1분 차트에서 VWAP break 직후 momentum candle 또는 소폭 pullback 후 재상승에 진입합니다.
5. 진입 모델 B — high break:
   - 급등 후 일정 시간 pullback/reset이 발생합니다.
   - 직전 고점 또는 반등 고점 돌파 직전에서 squeeze/high break를 노립니다.
6. 진입 모델 C — dip bounce:
   - 큰 selloff/flush 후 과매도 반등이 빠르게 발생할 때 짧게 매수합니다.
   - 단, 이는 가장 재량적이며 slippage 위험이 큽니다.

## 4. 매도/숏 조건
- 원 영상에서는 숏 전략을 다루지 않습니다.
- 단타 전략 분류상 매수 전용으로 기록합니다.
- 반대 신호: high break 실패, VWAP 재이탈, topping tail 재출현, volume 감소는 청산 또는 no-entry 조건으로 취급합니다.

## 5. 손절 조건
- VWAP reclaim: VWAP 재이탈 또는 진입 candle 저가 이탈.
- High break: 돌파 실패 후 직전 pullback low 이탈 또는 breakout level 하회.
- Dip bounce: flush low 재이탈 또는 반등 실패 즉시 손절.
- “trader rehab/guardrails” 언급상 손실 후 size 축소, 일일 손실 제한을 별도 risk overlay로 두는 것이 적절합니다.

## 6. 익절 조건
- 매우 짧은 구간에서 부분익절: 영상 사례 AUD는 7.20 진입 후 7.50~7.60 부근 이익실현.
- 다음 half/whole dollar, premarket high, halt level, 직전 고점이 목표 후보.
- high break 후 즉시 follow-through가 약하면 빠르게 축소/청산합니다.

## 7. 필터 조건
- 시간대: 원 작성자는 7 a.m.부터 관찰, 정규장 전후도 포함. 국내주식은 09:00~10:00 집중 후보.
- 거래량: 상대거래량 급증, 스캐너 포착, 10초/1분봉 체결 강도 필요.
- 변동성: 당일 +50%~100% 이상 급등 종목은 기회와 리스크가 동시에 큼. halt 가능성 고려.
- 시장 방향: 개별 뉴스/수급 중심이라 지수 방향보다 종목 momentum 우선.
- 종목 선정: leading % gainer, news catalyst, 낮은 float/유통물량, easy-to-borrow 여부는 매수 관점에서는 short pressure/수급 해석용 보조정보.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 높음
- 정량화 쉬운 요소: 당일 상승률 순위, VWAP, high break, topping tail, 거래량, float/news 여부 일부.
- 어려운 요소: 10초 차트 체결감, 호가창/Level 2, 뉴스 품질 해석, halt 전후 slippage, “무거워 보임” 같은 주관 판단.

## 9. 기계화 규칙 초안
1. 매일 장전/장초반 universe를 당일 등락률 상위 N개, 거래대금/상대거래량 상위, 가격 구간, 유통주식수 필터로 구성합니다.
2. News catalyst 여부를 수동 태그 또는 뉴스 API로 별도 저장합니다.
3. VWAP reclaim setup:
   - 가격이 VWAP 아래로 1회 이상 하락한 뒤, 1m 종가가 VWAP 위로 회복.
   - reclaim candle volume >= 직전 20개 1m 평균 volume의 k배.
   - 진입은 reclaim 종가 또는 첫 pullback 후 VWAP 위 지지 확인.
   - SL은 VWAP - buffer, TP는 1R/2R 또는 직전 고점.
4. High break setup:
   - 당일 고점 대비 pullback이 x% 이상 발생한 뒤 y분 이상 consolidation.
   - 직전 고점 돌파 시 진입, 실패 시 즉시 청산.
5. Dip bounce setup:
   - 1m 기준 z% 이상 급락 또는 큰 음봉 후 다음 candle이 저점 회복하면 소액 진입.
   - SL은 flush low, TP는 VWAP/직전 breakdown level.
6. 연속 topping tail이 N개 이상이면 추격 진입 금지 필터를 둡니다.

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 전일 대비 상승률/거래대금 상위, 뉴스/공시/테마, 시초가 급등 후 VWAP 회복, VI 전후 high break를 후보로 삼을 수 있습니다. 호가 단위와 VI 정지 규칙 때문에 슬리피지 모델이 중요합니다.
- 코인: 거래대금 상위 급등 알트에서 VWAP reclaim과 high break는 구현 가능하나, 24시간장이라 “장전” 개념 대신 최근 1~4시간 상승률 ranking으로 universe를 구성해야 합니다.

## 11. 리스크/반대 시나리오
- 급등주는 topping tail과 false breakout이 빈번합니다.
- 낮은 float/저유동성 종목은 체결 슬리피지와 halt risk가 큽니다.
- 영상은 수익 사례 중심이나 작성자도 drawdown과 trader rehab을 언급하므로 size/risk guardrail이 핵심입니다.
- 국내주식 VI 및 코인 급락 청산 cascade에서는 백테스트 체결가와 실제 체결가 괴리가 커질 수 있습니다.

## 12. 후속 검증 질문
- 국내주식 상승률 상위 종목에서 VWAP reclaim 후 5/10/20분 기대수익률은 양수인가?
- 연속 topping tail 필터가 손실 회피에 도움이 되는가?
- high break setup은 pullback 깊이와 consolidation 시간이 어느 정도일 때 가장 안정적인가?
- 뉴스 catalyst 태그를 넣으면 단순 상승률 상위 대비 성과가 개선되는가?
