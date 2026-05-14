# 068. Day-1 Volume Decay 눌림목/돌파 No-Trade 필터

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: `Holding the line...`
- URL: https://www.youtube.com/watch?v=POMf8yNOhk4
- 수집일/문서화: 2026-05-15
- 원문 위치: `data/raw_transcripts/youtube/POMf8yNOhk4.txt`
- 주요 근거 타임스탬프:
  - 00:24~01:05: breaking news day 1이 volume/relative volume/float rotation이 가장 높고 clean move 확률이 큼
  - 01:07~01:45: day 2~8 continuation은 가격이 오르더라도 volume decay, spread 확대, slippage 증가
  - 02:33~02:59: apex breakout에서 즉시 작동하지 않으면 bailout하는 방식
  - 05:01~05:22: 현재 시장은 큰 움직임 부족, edge가 낮아 no-trade 선택
  - 06:08~07:08: 200MA 아래, 고float/easy-to-borrow 종목 제외

## 2. 전략 분류
- 혼합 / 눌림목매매·신고점돌파매매 공통 진입 금지 필터
- 전략 유형: 매수 전략의 no-trade/시장상황 필터

## 3. 전략 요약
- 뉴스 발생 1일차가 아니고, 가격만 서서히 올라가며 거래량이 감소하는 continuation 종목은 눌림목·신고점돌파 모두 체결 품질이 악화되므로 자동매매 진입을 금지하거나 극소 size로만 처리하는 규칙입니다.
- 자산군: 미국 소형주 원형, 국내 급등 테마 후속일, 코인 펌핑 후 N일차 알트
- 시간프레임: 1분~5분, 장전 scanner
- 전략 유형: 매수 금지 필터 / 양방향 아님

## 4. 시장/종목 선행 조건
1. `catalyst_day_index`: 뉴스 또는 첫 급등일을 D1으로 계산합니다.
2. `volume_decay_ratio = today_premarket_volume / day1_same_time_volume` 또는 `today_cum_volume / day1_cum_volume`.
3. D2 이후라도 volume이 D1 대비 70% 이상 유지되고 fresh news가 추가되면 예외 가능.
4. `price_creep_up_with_lower_volume = true`: 가격은 고점을 높이나 거래량·체결강도는 감소하는 divergence.
5. overall market이 약세이거나 특정 섹터만 방어적 흐름이면 기준을 더 엄격히 합니다.

## 5. 진입 준비 조건
- 원칙적으로 `D1 + fresh catalyst + high float rotation`만 A급 후보로 인정합니다.
- D2~D8 continuation은 다음 조건을 모두 만족할 때만 관찰 후보입니다.
  - 전일 고점 위에서 좁은 range 유지
  - spread가 D1 대비 크게 확대되지 않음
  - 1분 ATR이 손절 허용폭 이내
  - 새로운 catalyst 또는 sector sympathy가 존재
- apex breakout: wedge/flag/pullback 끝에서 정확히 진입하며, 기다리는 매매가 아니라 즉시 작동 여부를 확인합니다.

## 6. 매수 조건 / 진입 트리거
- 이 문서는 적극 매수 전략보다 예외적 진입 조건을 정의합니다.
1. `catalyst_day_index == 1`이면 기존 breakout/pullback 전략 허용.
2. `catalyst_day_index > 1`이면 `volume_decay_ratio >= 0.7` 또는 `fresh_followup_news = true` 필요.
3. `spread_pct <= max_spread_pct` and `slippage_estimate <= stop_risk * 0.25`.
4. apex/pivot 돌파 후 10초~1분 내 즉시 수익권으로 이동해야 보유합니다.

## 7. 진입 금지 조건
- `catalyst_day_index >= 3` and `volume_decay_ratio < 0.5`.
- 가격은 상승하지만 거래량이 지속 감소하는 day 7~8 continuation.
- spread 확대, poor liquidity, 예상 slippage가 손절폭의 25% 초과.
- 200MA 아래에서 pop/selloff 반복.
- `float > 100M` 또는 easy-to-borrow로 short squeeze 압력이 약한 종목.
- trader가 drawdown 회복 중이어서 quality standard를 낮출 위험이 큰 상태.

## 8. 손절 조건
- breakout 진입 후 3~4분 내 작동하지 않으면 청산합니다.
- apex/pivot 재하회, bid 공백, spread 급확대 시 즉시 손절.
- D2+ 종목은 stop을 넓히지 않고, 최초 계획 손실을 초과하면 재진입 금지.

## 9. 익절 조건 / 트레일링 조건
- D2+ continuation 예외 진입은 첫 impulse만 목표로 합니다.
- 다음 round number/HOD 근처에서 대부분 청산하고, 잔여는 1분 higher low 이탈 시 정리합니다.
- 낮은 volume 환경에서는 큰 추세 보유보다 빠른 회전이 원칙입니다.

## 10. 필터 조건
- 시간대: 장전 7:00~9:30. D1 장전이 가장 선호됩니다.
- 거래량: D1 float rotation, relative volume, D2 이후 volume retention.
- 변동성: spread·slippage가 손절폭 대비 작아야 합니다.
- 시장 방향: 지수 약세·중동 리스크 등 risk-off면 no-trade 허용.
- 종목 선정: low float, hard-to-borrow/short squeeze 가능, fresh catalyst 우선.
- 뉴스/테마: 오래된 뉴스 재탕과 단순 continuation은 낮게 평가합니다.

## 11. 실패 패턴과 회피 규칙
- volume decay continuation: 가격만 올라가는 종목은 알고리즘이 상단 체결 후 하단 stop을 유도하기 쉽습니다.
- penny stock commission/체결 문제: 초저가주는 1~3센트 수익이 수수료·호가 비용에 잠식될 수 있습니다.
- easy-to-borrow high float: squeeze 연료가 부족해 breakout follow-through가 약합니다.
- 압박 매매: drawdown 회복 욕구로 A급이 아닌 종목을 거래하면 손실 누적 가능성이 커집니다.

## 12. 백테스트 가능성
- 등급: A-
- 정량화 가능 항목: catalyst_day_index, D1 대비 volume retention, spread_pct, slippage proxy, float, borrow status, 200MA 위치, breakout follow-through time.
- 구현 난이도: 중간. D1 기준일과 뉴스 이벤트 매칭이 필요하지만 가격/거래량 필터는 명확합니다.
- 추가 정의 필요사항: `catalyst_day_index`, `volume_decay_ratio`, `works_right_away_window`, `quality_standard_mode`.

## 13. 기계화 규칙 초안
```pseudo
for symbol in scanner:
    d = catalyst_day_index(symbol)
    vol_retention = volume_today_same_time(symbol) / volume_day1_same_time(symbol)

    if d >= 3 and vol_retention < 0.5:
        block(symbol, reason="late_day_volume_decay")
    if spread_pct(symbol) > max_spread_pct:
        block(symbol, reason="spread_slippage")
    if price_below_daily_200ma(symbol) and repeated_pop_selloff(symbol):
        block(symbol, reason="below_200ma_heavy")
    if float(symbol) > 100_000_000 and easy_to_borrow(symbol):
        block(symbol, reason="weak_squeeze_pressure")

    if not blocked and breakout_at_apex(symbol):
        enter_starter()
        if not profitable_within(minutes=3): exit()
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: D+1·D+2 테마주 중 전일 대비 거래대금이 50% 미만으로 줄었는데 고점만 올리는 종목은 눌림목·돌파 진입을 제한합니다.
- 코인: 상장/공지 D1 이후 funding·OI·거래대금이 감소하면서 가격만 상승하는 알트는 fake breakout 위험으로 간주합니다.

## 15. 리스크/반대 시나리오
- 강한 테마 장세에서는 D2~D5가 오히려 대시세가 될 수 있습니다. 따라서 fresh follow-up news, sector-wide momentum, volume retention이 있으면 예외를 허용해야 합니다.
- borrow status 데이터가 국내주식/코인에는 직접 대응되지 않으므로 대차잔고, 공매도 잔고, OI/funding 등 대체 변수가 필요합니다.

## 16. 후속 검증 질문
1. D1, D2, D3+ 별 HOD breakout 기대값은 어떻게 달라지는가?
2. D1 대비 volume retention 50%, 70%, 100% 기준 중 어느 값이 최적 필터인가?
3. spread_pct와 slippage proxy를 포함하면 백테스트 수익곡선이 얼마나 개선되는가?
