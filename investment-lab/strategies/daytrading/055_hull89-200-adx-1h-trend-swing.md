# 055. 1시간봉 Hull 89/200 + ADX 추세 전환 양방향 전략

## 1. 출처
- 채널/작성자: 코인독학
- 제목: 두달간, 무일푼 → 2억 만든 스윙 매매법
- URL: https://www.youtube.com/watch?v=zFwPFO5ETWU
- 수집일: 2026-05-10
- 원문 위치: `data/raw_transcripts/youtube/zFwPFO5ETWU.txt`

## 2. 전략 요약
- 한 문장: 1시간봉에서 Hull MA 89가 Hull MA 200을 교차한 뒤 ADX 25 이상일 때 다음 봉에 진입하고, 최근 고저점 손절 대비 2.5R로 청산하는 양방향 추세 전략입니다.
- 자산군: 코인 선물 중심, 국내주식은 스윙/ETF에 제한 적용
- 시간프레임: 1시간봉
- 전략 유형: 양방향 전략 / 추세 전환·스윙형 단타

## 3. 매수 조건
1. Hull 이동평균 89와 200을 1시간봉에 설정합니다.
2. Hull 89가 Hull 200을 상향 돌파합니다.
3. 교차 봉이 완성된 후 다음 봉에서 진입합니다.
4. ADX가 25 이상이어야 하며, 25 미만이면 가짜 돌파로 보고 제외합니다.

## 4. 매도/숏 조건
1. Hull 89가 Hull 200을 하향 돌파합니다.
2. 교차 봉이 완성된 후 다음 봉에서 숏 진입합니다.
3. ADX 25 이상 조건을 동일하게 적용합니다.

## 5. 손절 조건
- 롱: 교차 지점 기준 최근 저점 이탈.
- 숏: 교차 지점 기준 최근 고점 돌파.
- 손절폭이 과도하게 넓으면 최근 고저점 대신 Hull 교차 가격 부근으로 축소하는 보정 규칙을 둡니다.

## 6. 익절 조건
- 기본 익절: 손절폭의 2.5배(2.5R).
- 예: 손절폭 2.8%이면 목표수익률은 약 7.0%.
- 중간에 반대 교차가 먼저 발생하면 조기 청산 규칙을 별도 검증합니다.

## 7. 필터 조건
- 시간대: 24시간 코인 시장에는 상시 적용, 국내주식은 장중 데이터보다 종가/시간봉 스윙에 적합.
- 거래량: 원문 핵심 조건은 아니지만 거래대금 상위 코인/ETF로 제한 권장.
- 변동성: 손절폭이 7% 이상처럼 과도하면 현실적 목표가 비정상적으로 커지므로 진입 제외 또는 손절 보정.
- 시장 방향: 양방향 가능하나 횡보장에서는 ADX 필터가 중요합니다.
- 종목 선정: BTC, ETH, 고유동성 알트, 지수 ETF/레버리지 ETF 후보.

## 8. 백테스트 가능성
- 등급: 정량화 가능
- 구현 난이도: 낮음~중간
- 이유: Hull MA, ADX, 교차 후 다음 봉 진입, 최근 고저점 손절, 2.5R 익절이 모두 규칙화 가능합니다. 다만 Hull 계산식과 손절 보정 규칙을 명확히 고정해야 합니다.

## 9. 기계화 규칙 초안
```text
TF = 1h
HMA_fast = HMA(close, 89)
HMA_slow = HMA(close, 200)
ADX14 >= 25
LongEntry = crossover(HMA_fast, HMA_slow) confirmed at candle close; enter next candle open
ShortEntry = crossunder(HMA_fast, HMA_slow) confirmed at candle close; enter next candle open
LongStop = min(recent_swing_low, cross_price) rule variant test
ShortStop = max(recent_swing_high, cross_price) rule variant test
TakeProfit = Entry +/- 2.5 * initial_risk
Skip = initial_risk_pct > threshold, e.g. 4~5% for spot or 2~3% for leveraged futures
```

## 10. 국내주식/코인 적용 아이디어
- 코인: BTC/ETH/상위 알트 1시간봉 양방향 추세 전략으로 직접 테스트 가능합니다.
- 국내주식: 개별주 단타보다는 KOSPI200/KOSDAQ150 레버리지·인버스 ETF 또는 유동성 높은 대형주 스윙 필터로 적합합니다.

## 11. 리스크/반대 시나리오
- 1시간봉 교차 전략은 횡보장에서 연속 손절이 발생할 수 있습니다.
- ADX 25가 과최적화된 값일 가능성이 있으므로 20/25/30 민감도 검증이 필요합니다.
- 손절폭 보정은 재량 요소가 있어 규칙을 고정하지 않으면 백테스트와 실거래가 달라집니다.

## 12. 후속 검증 질문
1. HMA 89/200 대신 55/144, 100/200 조합의 성과는 어떤가?
2. ADX 25 필터가 실제로 횡보장 손실을 줄이는가?
3. 최근 고저점 손절과 교차가격 손절 중 어느 방식이 기대값이 높은가?
