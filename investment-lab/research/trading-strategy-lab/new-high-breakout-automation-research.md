# 신고점돌파매매 자동화 리서치 통합 노트

업데이트: 2026-05-15

## 핵심 결론
- 신고점돌파는 “고점 초과” 자체보다 `선행 리더십 + 압축/균형 + 거래량 확장 + 종가 유지 + 섹터 동조`의 조합으로 정의할 때 자동화 가능성이 높습니다.
- 단타에서는 당일고점/전일고점 돌파, 데이·스윙 연계에서는 20일/60일/52주 신고가 돌파를 분리해 테스트해야 합니다.

## 출처별 공통 규칙
1. Qullamaggie 기존 문서(`032`, `039`, `046`)
   - 1/3/6개월 수익률 상위 리더가 30~100% 선행 상승 후 2주~2개월 질서 있는 눌림·압축을 만들고 range expansion.
   - 진입은 ORH/피벗/박스 상단 돌파, 손절은 당일 저가 또는 피벗 아래.
2. 국내 대장주 돌파/상한가 계열 기존 문서(`030`, `045`, `053`, `060`)
   - 거래대금 상위 대장주, 기준봉/상한가/세력 거래량 이후 전고점 재돌파.
   - VI·상한가 근접 리스크와 장대 윗꼬리 false breakout 관리 필요.
3. Investors Underground 2026-04-27 신규 문서(`062`)
   - 반도체/AI 섹터 리더십과 위험선호가 선행 조건.
   - 장기 consolidation 이후 equilibrium break가 강한 continuation으로 이어질 수 있음.
   - 대형 리더(ARM/AMD/NVDA)와 2선 sympathy(POET/MXL/AMSC)를 구분해야 함.
4. Ross Cameron 2026-05-13 신규 문서(`064`)
   - 당일 +100% 이상 leading gainer가 pullback/curl 후 HOD 직전의 `line_in_sand`를 돌파할 때 선진입.
   - 명확한 HOD 돌파보다 0.2~0.5ATR 아래 또는 round number 직전에서 tape가 붙는 지점을 트리거 후보로 사용.
   - topping tail cluster, 9:30 이후 과도한 swing, thickly traded/crowded 상태는 false breakout 필터로 분리.
5. Ross Cameron 2026-05-14 신규 문서(`066`)
   - 9:00am breaking news로 market-wide leading gainer가 된 종목의 cup-and-handle/round-number pivot 돌파를 신고점돌파로 정의.
   - `day_gain_pct >= 100`, `price > VWAP`, `breakout_volume_ratio >= 1.5`, `1m close hold` 조합이 기본 자동화 후보.
   - 정규장 이후 halt/stop/market order가 만든 1분 과대 swing은 수익 기회와 별개로 자동매매 금지 또는 size 축소 필터로 둠.
6. Ross Cameron 2026-05-15 신규 문서(`067`, `068`, `069`)
   - 신고점돌파 후보는 fresh catalyst와 공시/매도물량 리스크를 먼저 걸러야 하며, 뉴스 없는 leading gainer 또는 buy rating/placement agent 충돌은 제외.
   - D1 대비 volume decay가 큰 D3+ continuation은 고점을 높여도 spread/slippage가 커져 breakout edge가 약해지는 no-trade regime.
   - 과거 대형 catalyst memory가 있는 종목은 daily resistance ladder를 기준으로 돌파 후 pullback-curl을 기다려 다음 level까지의 짧은 확장을 노림.

## 신고점 범위 정의 후보
- `intraday_high_break`: 당일 고점 돌파.
- `prev_day_high_break`: 전일 고점 돌파.
- `n_day_high_break`: 20일/60일 고점 돌파.
- `box_break`: 최근 N일 박스 상단 돌파.
- `all_time_or_52w_high`: 52주/역사적 신고가 돌파.

## 자동매매 변수 후보
- `box_days`: 압축 기간. 10/20/40/60거래일 비교.
- `box_width_pct`: 박스 고저폭 / 박스 저점.
- `atr_compression`: 현재 ATR20 / 선행 impulse ATR20.
- `line_in_sand`: HOD 직전 조기 트리거. 후보: `HOD - 0.2~0.5 * 1m_ATR`, 직전 pivot high, round number 직전 가격.
- `cup_handle_pivot`: 첫 고점 후 pullback/curl/handle 상단. 장전 squeeze에서는 round/half-dollar와 겹칠수록 우선순위 상향.
- `manageable_move_window`: 시간대별 1분 ATR/가격이 손절 허용폭 이내인 구간. 정규장 이후 halt/stop/market order 구간은 별도 regime.
- `breakout_buffer`: 기준선 대비 돌파 폭. 0.2~0.5% 후보.
- `breakout_volume_ratio`: 돌파봉 거래량 / 20개 분봉 평균. 1.5/2.0/3.0배 비교.
- `close_hold`: 돌파 후 1~2개 5분봉이 기준선 위 종가 유지.
- `upper_wick_ratio`: 윗꼬리 / 전체 range. 40% 이하 후보.
- `topping_tail_cluster`: 최근 5개 1분봉 중 윗꼬리 40~50% 이상 봉 개수.
- `crowded_proxy`: 누적 거래량/유통주식수, bid-ask spread 변화, 1분 ATR 증가율.
- `fresh_catalyst_score`: 신규성·실질성·재탕 여부·공시 충돌을 합산한 뉴스 품질 점수.
- `offering_conflict_score`: shelf/offering/CB/유증/재단 unlock 등 매도물량 리스크 점수.
- `catalyst_day_index`: D1/D2/D3+ 돌파 성능 분리용 이벤트 일자.
- `volume_decay_ratio`: D1 동시간 대비 현재 거래량 유지율.
- `daily_level_ladder`: 과거 daily resistance와 round number를 정렬한 목표·저항 배열.
- `jack_knife_candle`: 고점 돌파 후 긴 양방향 wick이 생기는 변동성 과열 신호.
- `sector_rs`: 섹터 ETF 또는 테마 바스켓의 당일/20일 상대강도.
- `leader_rank`: 테마 내 거래대금·수익률 순위.

## 가짜 돌파 필터
- 돌파봉 종가가 기준선 아래로 복귀.
- 돌파 후 거래량이 즉시 평균 이하로 감소.
- 섹터 ETF/대장주가 VWAP 아래 lower low.
- 장대 윗꼬리 또는 gap + fade 구조.
- 대장주가 이미 급등 후 약해지는데 후발주만 뒤늦게 돌파.
- HOD 직전 돌파 시도에서 topping tail이 반복되고 종가가 기준선 위에 남지 못함.
- 정규장 개장 직후 stop/market order/halt level로 1분봉 range가 손절 허용폭을 초과.
- 돌파 후 add 가격 위에서 즉시 stall하고 tape가 붙지 못하면 starter만 남기거나 청산.
- 뉴스 부재, 재탕 follow-up, buy rating/placement agent 충돌 등 `fresh_catalyst_score`가 낮은 급등주는 제외.
- D3+ volume decay continuation에서 spread/slippage가 커지는 경우 고점 돌파라도 no-trade.
- daily level 바로 아래에서 진입해 다음 저항까지 R/R 1.0 미만이면 제외.

## 백테스트 우선순위
1. A급: 20일 박스 상단 돌파 + ATR 압축 + 거래량 2배 + 섹터 VWAP 상방.
2. A급: 전일고가/당일고가 돌파 후 5분봉 종가 유지 + VWAP 상방.
3. B+: 2선 sympathy 돌파를 대장주 강도 조건으로 필터링.
4. B: 돌파 후 눌림 재매수와 최초 돌파 진입 비교.
5. C: 옵션 flow/뉴스 narrative 점수화. 데이터 확보 난이도 높음.
6. A: 당일 +100% leading gainer의 HOD 직전 `line_in_sand` 돌파 + 거래량 1.5배 + topping tail cluster 없음. 선행 진입형과 1분봉 종가 확인형을 비교.
7. A: 9:00am news squeeze + cup-and-handle/round-number pivot 돌파 + VWAP 상방 + manageable 1m ATR. 장전 구간과 정규장 halt-risk 구간을 분리 테스트.
8. B+: fresh catalyst score와 offering/shelf conflict score를 결합해 뉴스 없는 leading gainer·이해상충 buy rating의 false breakout 감소 효과 검증.
9. A-: `catalyst_day_index`와 `volume_decay_ratio` 기반 D1 vs D3+ 신고점돌파 기대값 비교.
10. A-: historical catalyst memory + daily level ladder + pullback-curl 후 다음 level까지의 base-hit 전략.

## 후속 검증 질문
- 국내주식은 20일 고점 돌파보다 전일고점+거래대금 급증이 단타에 더 적합한가?
- 코인에서는 4시간 박스 상단 돌파와 5분봉 돌파 중 어느 기준이 슬리피지를 덜 유발하는가?
- 신고점 돌파의 최적 손절선은 기준선 하회, 돌파봉 저가, VWAP 이탈 중 무엇인가?
