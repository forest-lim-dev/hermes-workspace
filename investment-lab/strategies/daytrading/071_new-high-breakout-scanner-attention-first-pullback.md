# 071. Scanner Attention 신고점돌파·첫 눌림목 대기 전략

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: `Day Trading Watch List for MONDAY!`
- URL: https://www.youtube.com/watch?v=T_EgRZO3IkM
- 수집일: 2026-05-15
- 문서화: 2026-05-16
- 원문 위치: `data/raw_transcripts/youtube/T_EgRZO3IkM.txt`
- 주요 근거 타임스탬프:
  - 01:37~02:16: PDT 규칙 완화 기대가 retail volume/volatility를 소형주에 집중시킬 수 있음
  - 06:27~06:46: 가격대별 성과 분석상 $5~10, 넓게 $2~20 sweet spot 선호, $2 미만은 낮은 성과
  - 09:03~11:55: 시장 관심이 이미 penny stock에 있으면 신규 뉴스주 follow-through가 약해질 수 있음
  - 14:14~16:40: scanner 첫 pop을 추격하지 말고 dust settle 후 지지 유지 여부 확인
  - 17:05~18:34: hot market에서는 첫 micro pullback이 유일한 진입이 될 수 있으나, 현재는 pop-hold-obvious 조건 필요
  - 18:44~18:53: 먼저 작게 ice break/cushion을 만든 뒤 size up

## 2. 전략 분류
- 혼합: 신고점돌파매매 + 눌림목매매
- 전략 유형: 매수 전략 / 시장상황 필터

## 3. 전략 요약
- 당일 scanner 1등 관심주가 될 가능성이 있는 $2~20 소형주를 대상으로, 첫 급등봉 추격은 피하고 급등 후 지지·상위 gainers 유지·거래량 follow-through가 확인될 때 첫 눌림 또는 HOD 재돌파를 매수하는 전략입니다.
- 자산군: 미국 소형주 원형, 국내 거래대금 상위 테마주, 코인 급등률/거래대금 상위 알트코인
- 시간프레임: 장전 7:00~정규장 초반, 10초~5분
- 전략 유형: 매수 전략 + 종목 선정/시장 관심 필터

## 4. 시장/종목 선행 조건
1. 시장 regime: retail risk-on, 최근 3~5거래일 100%+ 급등주가 반복되어 참여자가 “다음 leader”를 찾는 환경.
2. 가격대: Ross 기준 $5~10 최선, 넓게 $2~20 허용. $2 미만 penny stock은 성과 낮아 감점.
3. scanner obviousness: 첫 pop 후에도 당일 상승률이 30~100% 이상으로 top gainer 상단에 남아야 합니다.
4. attention concentration: 장전부터 특정 penny stock이 5천만주 이상 거래되며 관심을 선점하면 신규 뉴스주의 follow-through를 낮게 평가합니다.
5. catalyst: breaking news, hot sector pivot(AI 등), 또는 명확한 retail story가 있어야 합니다.

## 5. 진입 준비 조건
- 신규 scanner alert 직후 1~2분은 관찰 구간으로 둡니다.
- “dust settle” 확인:
  1. 첫 급등봉 고점 대비 되돌림이 35~65% 이내에서 멈춤.
  2. 급락 후 완전 round trip하지 않고 전일 종가/뉴스 전 가격보다 충분히 위에서 base 형성.
  3. base 형성 후에도 top gainer 순위가 1~3위권 또는 최소 top 10 안에 유지.
  4. 10초/1분 higher low가 2회 이상 발생.
- hot market(연속 300~1000% move 발생)에서는 관찰 시간을 줄이고 첫 micro pullback 허용. cooler market에서는 pop-hold 확인 전 진입 금지.

## 6. 매수 조건 / 진입 트리거
### A. 첫 눌림목 진입
1. 첫 pop으로 scanner에 노출되고 거래량이 급증합니다.
2. 1차 되돌림 후 base low가 형성됩니다.
3. 가격이 base high 또는 10초 lower high를 재돌파하며 curl up.
4. stop은 base low/VWAP/직전 pivot 중 가까운 구조적 저점.
5. target은 HOD 재테스트, 이후 HOD 돌파 시 next daily level 또는 round number.

### B. 신고점 재돌파 진입
1. 첫 pop 후 가격이 HOD 아래에서 consolidation.
2. 직전 실패 고점 바로 아래에서 volume이 마르지 않고 압축.
3. HOD 돌파 순간 거래량이 직전 5개 1분봉 평균 대비 1.5~3배 이상.
4. 돌파 직후 bid가 HOD 위에서 유지되면 starter → cushion 이후 add.

## 7. 진입 금지 조건
- 첫 1분봉에서 100% 상승 후 $5.5→$3처럼 40% 이상 즉시 급락하고 base 확인 전 추격.
- pop 후 당일 상승률이 8% 수준으로 내려와 top gainer 관심권에서 이탈.
- 이미 penny stock/다른 종목이 5천만~7억주 거래량으로 시장 관심을 독점.
- 가격이 너무 높아 trader 본인 sweet spot을 벗어남(예: $15 출발→$43 이동, 변동폭·손절 부담 과대).
- 첫 거래부터 큰 size. cushion 없이 “이번 주를 만회”하려는 aggressive sizing.

## 8. 손절 조건
- 첫 눌림 진입: base low 이탈 또는 VWAP 재이탈.
- HOD 돌파 진입: 돌파 가격 아래로 10초/1분 종가 이탈, 또는 돌파봉 거래량이 이어지지 않고 즉시 윗꼬리.
- scanner obviousness 상실: top gainer 순위 급락, 거래량 급감, 신규 leader 등장.
- 계좌/심리 필터: drawdown 회복 중이면 첫 손실 이후 size를 즉시 절반 이하로 축소.

## 9. 익절 조건 / 트레일링 조건
- 1차: HOD retest 또는 round number 직전 base hit.
- 2차: HOD 돌파 후 거래량이 유지되면 10초 higher low / 1분 EMA/VWAP를 따라 trailing.
- peak-of-volume topping tail 또는 큰 윗꼬리 출현 시 잔여 청산.
- cooler market에서는 첫 목표 도달 시 대부분 청산, hot market에서만 add/trail 허용.

## 10. 필터 조건
- 시간대: 장전 7:00 ET 이후 breaking news와 정규장 초반. 9:00 정각 sudden pop은 첫 candle 완료 전 추격 금지.
- 거래량: 첫 pop 거래량은 scanner 노출에 충분해야 하나, light volume으로 100% 상승한 경우 risk 과대.
- 변동성: 1분봉 range가 계좌 허용 손절폭을 초과하면 관찰만.
- 시장 방향: S&P/Russell risk-on, 최근 소형주 leader 다수 발생 시 가점.
- 종목 선정: $5~10 우선, $2~20 허용, $2 미만/과도한 penny volume 환경은 감점.
- 뉴스/테마: AI pivot, biotech, 강한 breaking news 등 attention을 한 곳으로 모을 수 있는 story 선호.

## 11. 실패 패턴과 회피 규칙
- `first-pop-chase failure`: scanner 첫 alert에 $5~$5.5 추격 후 $3까지 급락.
- `attention dispersed`: 좋은 뉴스라도 시장 참여자가 이미 다른 leader에 집중해 후속 매수가 약함.
- `not obvious enough`: pop 후 상승률이 낮아 top 10 gainer에 들지 못해 liquidity가 따라오지 않음.
- `too expensive for edge`: 가격이 높아 share size/손절 관리가 어려워 실수 한 번의 손실이 큼.

## 12. 백테스트 가능성
- 등급: A
- 정량화 가능 항목: price bucket, top gainer rank, first_pop_pct, first_pop_retrace_pct, volume_at_alert, attention_concentration_index, HOD reclaim, VWAP hold, market_hotness_score.
- 구현 난이도: 중간~높음. 분봉/틱 데이터와 scanner 순위/뉴스 타임스탬프가 있으면 충분히 구현 가능하지만 `attention_concentration` 계산이 필요합니다.
- 추가 정의 필요사항: `scanner_obviousness`, `attention_concentration_index`, `market_hotness_score`, `dust_settle_base`, `sweet_spot_price_bucket`.

## 13. 기계화 규칙 초안
```pseudo
market_hotness = count_recent_intraday_moves(pct>=100, lookback=5d)
attention_concentration = max(premarket_volume_by_symbol) / total_top10_premarket_volume

for symbol in high_day_momentum_scanner:
    if price < 2 or price > 20: continue
    if price >= 5 and price <= 10: score += 2
    if top_gainer_rank(symbol) <= 3: score += 2
    if catalyst_quality(symbol) >= 2: score += 2
    if attention_concentration > 0.55 and symbol != attention_leader: score -= 2

    wait_until(first_pop_candle_complete or dust_settle_base_detected)
    retrace = first_pop_retrace_pct(symbol)
    if market_hotness < hot_threshold and not dust_settle_base_detected(symbol): continue
    if retrace > 0.70: continue
    if top_gainer_rank(symbol) > 10: continue

    if curl_rebreak_base_high(symbol):
        buy_starter(stop=base_low, target=hod)
    if hod_breakout_with_volume(symbol, vol_ratio>=1.5) and cushion_positive:
        add_or_buy(stop=hod_breakout_level, target=next_round_or_daily_level)
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: 장전/장초반 거래대금 상위와 등락률 상위를 결합해 “obvious leader”를 정의합니다. 첫 VI 직전/직후 추격보다 VI 해제 후 지지·재돌파를 우선 테스트합니다.
- 코인: 업비트/바이낸스 급등률·거래대금 상위 알트에서 첫 1분 급등 후 완전 되돌림을 피하고, VWAP/직전 base 위 재돌파만 허용합니다.

## 15. 리스크/반대 시나리오
- hot market 초입에서는 첫 pop을 기다리다 유일한 진입을 놓칠 수 있습니다.
- 반대로 cooler market에서는 첫 pop chase가 가장 큰 손실원이 됩니다.
- scanner 데이터가 없으면 top gainer rank와 attention concentration을 정확히 재현하기 어렵습니다.

## 16. 후속 검증 질문
1. $5~10 가격대 leader의 HOD 재돌파 기대값이 $2 미만 penny stock보다 높은가?
2. 첫 pop 후 35~65% retrace 뒤 base를 만든 종목과 즉시 HOD 추격 종목의 손익비 차이는?
3. attention concentration이 높은 날 신규 뉴스주 breakout 성공률은 낮아지는가?
