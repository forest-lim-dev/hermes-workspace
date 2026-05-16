# 눌림목매매 자동화 리서치 통합 노트

업데이트: 2026-05-17

## 핵심 결론
- 눌림목은 “싸게 보이는 하락”이 아니라, 선행 상승·테마 강도·거래량 감소·구조 유지가 동시에 충족되는 일시적 재고 조정으로 정의해야 합니다.
- 단타 자동매매에서는 `선행 impulse → 얕거나 통제된 되돌림 → 거래량 수축 → VWAP/이평/전고점 reclaim → 짧은 무효화선` 순서로 기계화하는 것이 가장 자연스럽습니다.

## 출처별 공통 규칙
1. Ross Cameron 계열 기존 문서(`006_micro-pullback-low-float-news-momentum.md`)
   - 저유통/뉴스/당일 leading gainer에서 수초~수십초 micro pullback 후 고점 재돌파.
   - 손절은 pullback low 이탈.
2. 국내 대장주 계열 기존 문서(`051`, `052`, `054`)
   - 테마 대장주만 우선, 후발주는 시가/VWAP 깊은 눌림에서 제한 진입.
   - 지수 급락 중에도 상대강도 대장주가 저점을 높일 때만 눌림 인정.
3. Investors Underground 2026-05-04 신규 문서(`061`)
   - 강한 시장·강한 테마에서 놓친 종목은 추격보다 consolidation/reclaim 대기.
   - ATER: strong ramp and pullback, reclaim and move back toward highs.
   - TLIH/XTLB/HCAI: initial volume/move 이후 base가 생기면 다음 leg 또는 liquidity trap 후보.
4. Ross Cameron 2026-05-13 신규 문서(`063`)
   - 뉴스가 있는 Day-1 100%급 leading gainer에서 첫 급등 후 최소 2~3개 1분봉 눌림 또는 8~20% pullback을 기다림.
   - 눌림 후 round number/half-dollar/HOD retest 방향으로 curl할 때 starter 진입.
   - 2일차 continuation, 너무 짧은 1~2분 눌림, 한 캔들 range가 손절 허용폭을 초과하는 고가·고변동 상태는 금지.
5. Ross Cameron 2026-05-14 신규 문서(`065`)
   - breaking news + low float + float turnover 급증 종목이 첫 급등 후 VWAP를 reclaim하고 짧은 handle/pullback을 만들 때만 눌림 인정.
   - 눌림 구조는 `impulse → 20~60% retrace → VWAP reclaim 또는 minor pivot break → round/HOD 방향 확장`으로 정량화.
   - false breakout 후 거래량 급증·윗꼬리 50% 이상, 200MA 직하단, halt 이후 1분 range가 손절폭을 넘는 구간은 진입 금지.
6. Ross Cameron 2026-05-15 신규 문서(`068`, `069`)
   - D1 뉴스/첫 급등일의 float rotation이 가장 clean한 눌림을 만들며, D3+ continuation은 가격 상승에도 volume decay·spread 확대가 있으면 눌림 후보에서 제외.
   - 과거 대형 catalyst 기억이 있는 종목은 daily level 돌파 뒤 15~45% 짧은 pullback-curl을 기다려 다음 level까지의 base hit만 노림.
   - jack-knife candle, topping tail cluster, easy-to-borrow/float 증가 이후 cushion 없는 추격은 눌림 재상승보다 실패 패턴으로 분류.
7. Ross Cameron 2026-05-16 신규 문서(`070`, `071`)
   - VWAP reclaim·micro pullback이 보여도 `regained compliance`/reverse split 같은 약한 catalyst, 두꺼운 ask refill, HOD double top 위험이 있으면 `trap curl`로 분류해 진입 금지.
   - scanner 첫 pop 직후 추격하지 않고 1~2분 dust-settle 뒤 base low, top-gainer 유지, higher low, 거래량 follow-through를 확인.
   - hot regime에서는 첫 micro pullback 허용 폭을 넓히되, cooler/cautious regime에서는 pop-hold-obvious 조건이 없으면 눌림으로 인정하지 않음.

## 자동매매 변수 후보
- `impulse_pct`: 직전 1~5일 또는 장중 상승폭. 후보 기준 20% 이상.
- `impulse_volume_ratio`: 선행 상승 거래량 / 20일 평균 거래량. 후보 기준 3배 이상.
- `retrace_pct`: 직전 상승폭 대비 되돌림률. 후보 범위 20~50%.
- `volume_contract_ratio`: 눌림 구간 거래량 / 상승 구간 거래량. 후보 기준 0.4~0.7 이하.
- `structure_hold`: higher low 개수, VWAP 유지, 전고점/전일고가 지지 여부.
- `reclaim_signal`: VWAP 또는 5분 20EMA 재상향 + 거래량 1.5배.
- `day1_news_flag`: 당일/전일 장후 신규 뉴스 여부. Day-1 뉴스 급등주 눌림 우선.
- `pullback_bars`: 선행 급등 후 눌림을 구성한 1분봉 개수. 후보 2/3/5개 비교.
- `round_half_level_proximity`: round number/half-dollar까지 남은 거리.
- `one_min_atr_risk`: 최근 1분봉 평균 range / 계좌 허용 손절폭. 1.0 초과 시 금지 후보.
- `float_turnover`: 누적 거래량 / 유통주식수. short squeeze 눌림에서는 1배 이상 최소, 3배 이상 강한 조건 후보.
- `short_pressure_proxy`: easy-to-borrow 후 담보율 상승, 대차/공매도/청산 데이터, 또는 코인 short liquidation spike.
- `false_breakout_wick_ratio`: 새 고점 직후 윗꼬리 / 전체 range. 50% 이상이면 다음 눌림은 확인형만 허용.
- `catalyst_day_index`: 뉴스/첫 급등일을 D1으로 두고 D2/D3+ continuation을 분리.
- `volume_decay_ratio`: 오늘 동시간 누적거래량 / D1 동시간 누적거래량. 0.5 미만이면 no-trade 후보.
- `daily_level_ladder`: 과거 고점·저항·round number를 정렬한 다음 목표/저항 배열.
- `curl_trigger`: pullback high 재돌파 + 10초/1분 bid follow-through.
- `jack_knife_candle`: 긴 양방향 wick 또는 급등·급락이 한 봉에 동시에 나타나는 변동성 위험 신호.
- `news_quality_score`: 뉴스 신규성·실질성·숫자/계약 여부·방어적 공시 여부를 0~3점화.
- `trap_curl`: VWAP reclaim/재상승이 있으나 약한 catalyst와 두꺼운 매도호가로 HOD 직전 실패할 확률이 높은 패턴.
- `ask_refill_ratio`: breakout 직전 ask 잔량이 체결 후 재충전되는 강도. hidden seller proxy.
- `attention_concentration_index`: top 10 scanner 종목 중 1위 또는 penny-stock group이 차지하는 거래량 비중.
- `scanner_obviousness`: 당일 상승률, top-gainer rank, 거래량, 가격대 sweet spot을 합산한 시장 관심 점수.
- `dust_settle_base`: 첫 pop 이후 1~2분 관찰 구간에서 형성된 구조적 저점/횡보 구간.
- `theme_rank`: 동일 테마 내 거래대금/등락률 순위.
- `market_filter`: 지수 또는 섹터 ETF의 5분 VWAP 상방 여부.

## 충돌하는 주장/주의점
- 강한 종목은 얕은 눌림만 주고 바로 재돌파할 수 있으나, 너무 얕은 눌림은 손절폭 대비 보상이 작아질 수 있습니다.
- 후발 sympathy는 눌림 반등 폭이 클 수 있지만 negative catalyst 또는 대장주 약화에 취약합니다.
- 유동성 트랩은 큰 수익을 줄 수 있지만, 백테스트에서는 wick/체결가/슬리피지를 보수적으로 가정해야 합니다.
- Day-1 뉴스 눌림은 승률이 높아 보여도 장대음봉 한 번이 평균 이익 여러 개를 지울 수 있어 `average_loss <= 1.5 * average_win` 제약을 별도 검증해야 합니다.

## 백테스트 우선순위
1. A급: `impulse_pct >= 20%`, `retrace_pct 20~50%`, `volume_contract_ratio <= 0.7`, `VWAP reclaim`, `market VWAP up` 조합.
2. A-/B+: 테마 대장주와 2등주를 분리한 성과 비교.
3. B: liquidity trap 재돌파 정의별 성과 비교.
4. C: 뉴스 품질/negative catalyst 필터. 텍스트 데이터 품질에 의존.
5. A-: Day-1 뉴스 + 100%급 leading gainer + 2~5개 1분봉 pullback + round/half-dollar curl 진입. 큰 손실 outlier 필터를 함께 테스트.
6. A-: breaking news + float turnover 1~3배 이상 + VWAP reclaim 눌림. 200MA 저항·false breakout wick·halt range 필터의 outlier 감소 효과를 우선 검증.
7. A-: D1 뉴스주 pullback과 D3+ volume decay continuation을 분리해, `volume_decay_ratio < 0.5` 필터가 손실/슬리피지 outlier를 줄이는지 검증.
8. A-: 과거 대형 catalyst memory + daily level ladder + 15~45% pullback-curl 진입. daily level까지 남은 R/R 1.5 이상 조건을 우선 테스트.
9. A-: VWAP reclaim 눌림 중 `news_quality_score <= 1` 또는 `ask_refill_ratio` 상위 구간을 제외했을 때 손실 outlier 감소 효과.
10. A: scanner 첫 pop 이후 `dust_settle_base` + top-gainer rank 유지 + 35~65% retrace 조건의 첫 눌림 성과를 즉시 추격과 비교.

## 후속 검증 질문
- VWAP reclaim 단독 vs reclaim 후 minor high 재돌파 확인 중 기대값이 높은 방식은 무엇인가?
- 국내 VI 종목에서는 VI 전 consolidation과 VI 후 첫 재돌파 중 어느 조건이 손익비가 좋은가?
- 코인에서는 BTC/ETH 5분 VWAP 필터가 alt pullback false bounce를 얼마나 줄이는가?

## 2026-05-17 업데이트: 국내 시간대·D+1 눌림 필터
- 신규 문서 `072`, `073`, `074` 반영.
- 국내 대장주 눌림은 D+0 신고가/상한가 이후 D+1/D+2에서 9:30 이후 VWAP·시가 회복을 확인하는 시간대 필터가 중요합니다.
- 프리마켓/NXT·장후 시간외는 개인 위주·저유동성 구간으로 신규 매수보다 보유분 매도/관찰 용도로 제한하는 것이 자동화에 유리합니다.
- 추가 변수 후보: `session_filter_kr`, `dplus_day_index`, `reclaim_after_0930`, `theme_concentration`, `leader_rotation`, `supertrend_line_stop`, `atr_percentile_expansion`.
- 백테스트 우선순위 추가: 전일 상한가/신고가 장대양봉 후보 중 9:30 이후 VWAP 회복 눌림의 성과를 9:00~9:20 조기 진입과 비교.
