# 눌림목매매 자동화 리서치 통합 노트

업데이트: 2026-05-13

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

## 후속 검증 질문
- VWAP reclaim 단독 vs reclaim 후 minor high 재돌파 확인 중 기대값이 높은 방식은 무엇인가?
- 국내 VI 종목에서는 VI 전 consolidation과 VI 후 첫 재돌파 중 어느 조건이 손익비가 좋은가?
- 코인에서는 BTC/ETH 5분 VWAP 필터가 alt pullback false bounce를 얼마나 줄이는가?
