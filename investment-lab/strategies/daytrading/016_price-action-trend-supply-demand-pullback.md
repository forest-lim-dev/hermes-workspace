# 016. Price Action Trend + Supply/Demand Pullback

## 1. 출처
- 채널/작성자: 슈퍼트레이더
- 제목: 단타 매매법 딱 1가지만 알면 인생이 바뀝니다 (코인, 주식 차트 보는법 모르는 초보도 가능)
- URL: https://www.youtube.com/watch?v=mQ73oYfJdzQ
- 수집일: 2026-04-28
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/mQ73oYfJdzQ.txt`
- 주요 근거 구간: 01:12~04:25 추세·유효 저점/고점 판정, 04:42~06:50 수요·공급존 정의, 09:29~10:08 진입/손절/목표, 14:29~17:53 2:1 이상 손익비 필터

## 2. 전략 요약
- 한 문장: 고점·저점 구조로 추세 방향을 먼저 결정하고, 강한 가격 이동 직전의 횡보 구간인 수요/공급존 재방문에서 반전 캔들과 거래량을 확인한 뒤 최소 2:1 손익비일 때만 진입합니다.
- 자산군: 코인, 국내주식, 해외주식
- 시간프레임: 5분~30분 단타, 상위 추세는 30분~1시간 후보
- 전략 유형: 양방향 전략 / 추세추종 눌림·되돌림

## 3. 매수 조건
1. 고점과 저점이 순차적으로 높아지는 상승 구조를 확인합니다.
2. “유효 저점”은 이전 고점을 명확히 돌파한 이후 형성된 저점으로만 인정합니다.
3. 가격이 유효 저점 아래로 하락하지 않는 동안 매수 방향만 고려합니다.
4. 강한 상승이 시작되기 직전 잠깐 횡보하거나 멈춘 구간의 고가~저가를 demand zone으로 표시합니다.
5. 가격이 조정으로 demand zone까지 되돌아옵니다.
6. demand zone 안 또는 바로 위에서 양봉 반전 캔들이 발생합니다.
7. 반전 캔들의 거래량이 직전 평균보다 증가합니다.
8. 진입 전 목표가까지의 기대수익이 손절폭의 최소 2배 이상이어야 합니다.

## 4. 매도/숏 조건
1. 저점과 고점이 순차적으로 낮아지는 하락 구조를 확인합니다.
2. “유효 고점”은 이전 저점을 명확히 하향 돌파한 이후 형성된 고점으로만 인정합니다.
3. 가격이 유효 고점 위로 상승하지 않는 동안 매도/숏 방향만 고려합니다.
4. 강한 하락이 시작되기 직전 횡보 구간의 고가~저가를 supply zone으로 표시합니다.
5. 가격이 반등으로 supply zone까지 되돌아옵니다.
6. supply zone에서 음봉 반전 캔들과 거래량 증가가 확인됩니다.
7. 목표가까지 손익비가 최소 2:1 이상일 때만 진입합니다.

## 5. 손절 조건
- 롱: demand zone 하단 바로 아래. 보수적으로는 유효 저점 아래.
- 숏: supply zone 상단 바로 위. 보수적으로는 유효 고점 위.
- 추세 무효화: 롱은 유효 저점 종가 이탈, 숏은 유효 고점 종가 돌파 시 구조가 깨진 것으로 간주합니다.
- 손익비 필터를 통과하지 못하면 진입 자체를 취소합니다.

## 6. 익절 조건
- 1차 목표: 최근 고점(롱) 또는 최근 저점(숏).
- 목표가가 너무 가까워 2R 미만이면 거래하지 않습니다.
- 목표 돌파 후 추세가 지속되면 새 demand/supply zone 생성 후 재진입 또는 일부 물량 추적 청산을 별도 검증합니다.

## 7. 필터 조건
- 시간대: 국내주식은 09:10~10:30과 13:30~14:50 우선. 코인은 거래량 집중 세션 우선.
- 거래량: 반전 캔들 거래량이 직전 20캔 평균 대비 1.2~1.5배 이상인 경우 우선 검증합니다.
- 변동성: zone 폭이 ATR 대비 과도하게 넓으면 손절폭이 커져 손익비가 나빠질 수 있습니다.
- 시장 방향: 지수/섹터가 같은 방향이면 가중치 부여. 국내주식 개별 테마주는 테마 대장주 우선.
- 종목 선정: 당일 거래대금 상위, 추세가 명확하고 스프레드가 좁은 종목.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간
- 가능한 부분: HH/HL, LH/LL, 이전 고점 돌파 이후의 유효 저점, zone 재방문, 거래량 증가, 2R 필터는 정량화 가능합니다.
- 어려운 부분: 수요/공급존을 “강한 이동 직전 횡보”로 잡는 방식은 알고리즘 정의가 필요합니다.

## 9. 기계화 규칙 초안
```text
swing_high, swing_low = pivot(high, low, left=3, right=3)
uptrend = latest_swing_high > prior_swing_high and latest_swing_low > prior_swing_low
valid_low = swing_low formed after close > prior_swing_high
valid_high = swing_high formed after close < prior_swing_low

demand_zone = consolidation_range_before(bull_impulse)
supply_zone = consolidation_range_before(bear_impulse)
bull_impulse = body > 1.5 * avg_body(20) and close > prior_range_high
bear_impulse = body > 1.5 * avg_body(20) and close < prior_range_low

long_confirm = close > open and close > prior_close and volume > 1.3 * avg_volume(20)
short_confirm = close < open and close < prior_close and volume > 1.3 * avg_volume(20)

long_entry = uptrend and close > valid_low and price_touches(demand_zone) and long_confirm
short_entry = downtrend and close < valid_high and price_touches(supply_zone) and short_confirm
long_stop = demand_zone.low - buffer
short_stop = supply_zone.high + buffer
long_target = recent_swing_high
short_target = recent_swing_low
trade_allowed = reward_risk >= 2.0
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 상승 추세 테마주에서 장중 첫 눌림을 demand zone으로 매매하고, 하락 조건은 공매도 대신 매수 회피/청산 필터로 활용합니다.
- 코인: 양방향 선물에서 같은 규칙을 롱/숏 모두 적용하되, 펀딩비·청산맵 과열 구간은 별도 리스크 필터로 둡니다.
- 거래량 확인이 핵심이므로 코스닥 저유동 종목보다 거래대금 상위 종목에 우선 적용합니다.

## 11. 리스크/반대 시나리오
- 추세 전환 초입에서는 HH/HL 판정이 늦어 좋은 타점을 놓칠 수 있습니다.
- 급락/급등 뉴스에서는 demand/supply zone이 한 번에 관통되어 손절이 커질 수 있습니다.
- 거래량 증가 양봉이 단기 반등 후 실패하는 bull trap일 수 있습니다.
- 2R 목표를 최근 고점으로만 두면 횡보장에서는 진입 빈도가 크게 줄어듭니다.

## 12. 후속 검증 질문
1. swing pivot left/right 값을 2, 3, 5 중 무엇으로 둘 때 단타에 가장 적합한가?
2. demand/supply zone을 횡보 박스 기준으로 할지 첫 임펄스 캔들 기준으로 할지 성과 차이는?
3. 거래량 증가 필터 1.2배, 1.5배, 2.0배 중 어느 수준이 국내주식에서 과최적화를 줄이는가?
4. 최근 고점 목표와 고정 2R 목표 중 어느 청산 방식이 더 안정적인가?
