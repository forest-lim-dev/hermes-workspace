# 전략 후보: Low Float News Momentum Micro Pullback

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: “The Micro Pullback Trading Strategy (Small Account Challenge)”
- URL: https://www.youtube.com/watch?v=6P25hNn_H00
- 수집일: 2026-04-25
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/6P25hNn_H00.txt`

## 2. 전략 요약
- 한 문장: 뉴스로 급등하며 스캐너에 포착된 저유통주가 10초~1분 차트에서 50% 이상 되돌리지 않는 짧은 pause를 만든 뒤 재상승할 때, 고점 재돌파와 half/whole dollar continuation을 노리는 초단타 매수 전략입니다.
- 자산군: 원 영상은 미국 소형주. 국내주식 급등 테마주와 코인 급등 알트에 변형 가능.
- 시간프레임: 10초 차트 중심, 보조 1분 차트.
- 전략 유형: 매수 전략, momentum continuation / micro pullback.

## 3. 매수 조건
1. 종목 선정 5대 조건을 충족해야 합니다.
   - 당일 최소 +10% 이상 상승.
   - 50일 평균 대비 상대거래량 5배 이상.
   - 뉴스 catalyst 존재.
   - 가격대는 대체로 2~20달러 선호.
   - 유통주식수는 2천만 주 미만, 이상적으로 1천만 주 미만.
2. 뉴스 직후 또는 스캐너 포착 직후 가격이 빠르게 상승합니다.
3. 고점에서 무작정 추격하지 않고, 몇 초~수십 초짜리 micro pullback을 기다립니다.
4. Pullback은 직전 상승 leg의 50% 이상을 되돌리면 안 됩니다. 50% 이상 하락하면 약세로 간주합니다.
5. 10초 차트에서 2~3개 red candle 또는 일시적 pause가 나온 뒤, 더 이상 내려가지 않고 다시 위로 전환할 때 진입합니다.
6. 이상적 진입은 pullback low를 명확히 둘 수 있고, 재상승이 직전 고점 retest로 이어질 수 있는 위치입니다.

## 4. 매도/숏 조건
- 원 영상은 숏 전략을 다루지 않습니다.
- 본 문서는 매수 전용 전략으로 분류합니다.
- 숏/회피 신호: 50% 이상 retracement, full round trip, topping tail 연속, news pop 이후 즉시 insider/공급 매물로 눌림, low of pullback 이탈.

## 5. 손절 조건
- 기본 손절: micro pullback low 이탈.
- 상승 leg의 50% retracement 이탈 시 손절 또는 no-entry.
- 첫 거래 risk는 일일 최대손실의 1/4 수준으로 제한하는 risk overlay가 제안됩니다.
- “3 strikes, you’re out”: 작은 손실 3회 누적 시 당일 중단 규칙을 검토합니다.

## 6. 익절 조건
- 1차 목표: 직전 고점 retest.
- 2차 목표: 다음 half dollar 또는 whole dollar.
- 강한 squeeze에서는 scale-out 방식으로 일부 청산 후 잔여를 continuation에 맡깁니다.
- 체결 속도가 매우 빠르므로 고정 limit/marketable limit, bracket order 등 실행 규칙이 필요합니다.

## 7. 필터 조건
- 시간대: 뉴스 발생 직후, 프리마켓/장초반 포함. 국내주식은 09:00~10:00와 VI 전후 구간 후보.
- 거래량: 상대거래량 5배 이상, 스캐너 포착, 거래대금 급증.
- 변동성: 당일 +10% 이상은 최소 조건이고, 실제 사례는 +100% 이상 급등도 포함.
- 시장 방향: 개별 catalyst가 핵심이므로 지수보다 종목 수급 우선.
- 종목 선정: 저유통주, 뉴스, 가격 접근성, 높은 rate of change가 핵심.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 높음
- 정량화 쉬운 요소: 등락률, 상대거래량, 가격대, float, 10초/1분 pullback 깊이, 직전 고점 retest, half/whole dollar target.
- 어려운 요소: 뉴스 품질, 초단위 체결/슬리피지, 호가 공백, halt, 스캐너 실시간 포착 시점.

## 9. 기계화 규칙 초안
1. Universe: 당일 상승률 >= 10%, relative volume >= 5, 가격 2~20달러, float < 20M, 뉴스 태그 보유 종목.
2. Momentum leg: 최근 1~3분 수익률 또는 10초봉 연속 상승폭이 threshold 이상이면 leg start/end를 기록합니다.
3. Pullback: leg 고점 이후 10초봉 2~4개 이내의 하락/횡보이며 retracement <= 50%.
4. 진입: 가격이 pullback high 또는 직전 10초봉 고가를 돌파할 때. 대안으로 pullback low 형성 후 첫 green candle high break.
5. SL: pullback low - tick buffer.
6. TP: 직전 high, 다음 0.5달러/1.0달러 라운드 넘버, 또는 1R/2R 분할익절.
7. No-entry: pullback이 50% 초과, volume 급감, spread가 ATR 대비 과도, halt 직전 과열 신호.
8. Risk overlay: 첫 거래 risk <= daily max loss의 25%, 3연속 손실 시 중단.

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 가격대 조건은 2~20달러 대신 개인 참여가 많은 중소형주 가격대와 거래대금 조건으로 대체합니다. 유통주식수/시가총액, 뉴스/공시/테마, 장초반 VI 가능성을 함께 필터링해야 합니다. 10초 데이터가 없다면 1분봉 내부 고저가로 보수적으로 근사합니다.
- 코인: float 개념은 유통시총/거래대금 대비 free float로 대체하고, 뉴스 대신 상장/파트너십/거래소 공지/소셜 급증을 catalyst로 태깅합니다. 초단위 데이터와 펀딩/오더북 불균형이 있으면 더 적합합니다.

## 11. 리스크/반대 시나리오
- micro pullback은 매우 빠른 실행이 필요해 백테스트와 실제 체결 괴리가 큽니다.
- 저유통주 급등은 halt, 호가 공백, 급락 round trip 위험이 큽니다.
- 뉴스가 좋더라도 insider/공급 매물이 나오면 급등이 즉시 실패할 수 있습니다.
- FOMO를 이용하는 전략이라 규칙 미준수 시 고점 추격 손실로 변질될 위험이 큽니다.

## 12. 후속 검증 질문
- 10초 데이터 없이 1분봉으로 micro pullback을 근사해도 기대값이 남는가?
- 50% retracement 필터는 38.2%, 50%, 61.8% 중 어느 기준이 가장 안정적인가?
- float < 10M과 < 20M의 성과 차이는 얼마나 큰가?
- 국내주식 VI 직전/직후 micro pullback은 별도 전략으로 분리할 가치가 있는가?
