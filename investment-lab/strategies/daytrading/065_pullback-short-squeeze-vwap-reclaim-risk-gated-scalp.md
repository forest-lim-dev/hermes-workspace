# 065. Short Squeeze VWAP Reclaim 눌림목 스캘프

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: `400% Short Squeeze?!?! No, 800% is Better!`
- URL: https://www.youtube.com/watch?v=B_6yuh7YY2g
- 수집일: 2026-05-13, 문서화: 2026-05-14
- 원문 위치: `data/raw_transcripts/youtube/B_6yuh7YY2g.txt`
- 주요 근거 타임스탬프:
  - 00:00~00:22: breaking news, easy-to-borrow, 200MA 저항 우려에도 $2.70→$12+ 급등
  - 01:47~02:24: 6.7M float, 100M+ volume, 유통주식수 대비 초과 거래량
  - 06:00~07:08: 8am scanner, $3.18 cup-and-handle breakout, $4 돌파, VWAP 재돌파 후 추가 패턴
  - 07:14~08:19: false breakout 다수, VWAP 돌파 눌림이 가장 clean한 setup
  - 08:31~10:02: easy-to-borrow와 200MA 저항, short collateral requirement 상승은 squeeze 연료

## 2. 전략 분류
- 눌림목매매 / 매수 전략
- 보조 성격: short squeeze regime filter, risk-gated size-up rule

## 3. 전략 요약
- breaking news로 scanner에 포착된 저유통주가 첫 급등 후 VWAP를 회복하고 짧은 눌림을 만들 때, 눌림 저점 이탈을 무효화선으로 삼아 다음 round number/HOD 방향 확장을 노리는 초단타 매수 전략입니다.
- 자산군: 미국 저유통 소형주 원형, 국내주식 VI/테마 급등주 및 코인 저유동 알트에 응용 가능
- 시간프레임: 10초~1분 진입, 1~5분 관리
- 전략 유형: 매수 전략

## 4. 시장/종목 선행 조건
1. `breaking_news_flag = true`: 장전 또는 장중 새 뉴스가 scanner에 포착되어야 합니다.
2. `relative_volume >= 10`: 영상 사례는 float 6.7M 대비 100M+ 거래량으로 float turnover가 15배 이상입니다. 자동화 초기값은 `cum_volume / float >= 1.0`을 최소, `>= 3.0`을 강한 조건으로 둡니다.
3. `day_gain_pct >= 50%`: 첫 alert 이후 50~100% 이상 상승해야 squeeze 후보로 인정합니다.
4. `low_float_flag = true`: 미국주는 float 20M 이하, 국내는 유통시총/호가잔량이 얇은 테마주, 코인은 24h 거래대금 대비 order book depth가 얕은 종목.
5. `short_pressure_proxy = true`: easy-to-borrow임에도 숏 담보율/대차 부담/급등 지속이 나타나거나, 국내·코인에서는 공매도/숏 포지션 청산 가능성을 직접 데이터로 대체합니다.
6. `macro_risk_on = true`: 영상은 PDT rule 완화 기대, 시장 all-time high, AI catalyst처럼 참여자 증가·위험선호가 배경입니다.

## 5. 진입 준비 조건
- 1차 급등 후 바로 추격하지 않고 다음 중 하나를 기다립니다.
  1. VWAP 하회 후 재상향 reclaim
  2. cup-and-handle 형태: 초기 고점 → red/near-red pullback → $3 부근 회복 → handle 압축 → pivot $3.18 돌파
  3. round number 전 눌림: $4, $5.50 등 호가 단위가 몰리는 가격 직전의 1~3개 소형 캔들
- `pullback_depth_pct`: 직전 impulse 저점→고점 상승폭의 20~60% 이내. 60% 초과 또는 전일 종가 하회 재진입은 위험 신호로 별도 분리합니다.
- `volume_contract_ratio <= 0.7`: 눌림 거래량이 상승봉 평균보다 줄어야 합니다. 단, squeeze주에서는 false breakout 손절 물량 때문에 거래량이 높을 수 있어 `red_volume_spike_after_new_high`는 실패 신호로 취급합니다.

## 6. 매수 조건 / 진입 트리거
1. Scanner 조건 충족: `breaking_news_flag`, `day_gain_pct`, `rel_volume`, `float_turnover` 통과.
2. 가격이 VWAP 아래에서 위로 회복하거나, VWAP 위에서 higher low를 형성합니다.
3. 다음 중 하나가 발생하면 starter 진입:
   - `close_10s_or_1m > VWAP` and `high_break(minor_pivot)`
   - cup-and-handle pivot 돌파: 예시 $3.18
   - round number 직전 압축 후 ask 체결 증가: 예시 $3.95→$4.00, $5.45→$5.50
4. add 조건:
   - 최초 진입 후 즉시 unrealized profit이 생기고, 다음 pivot 또는 round number를 거래량 증가로 돌파
   - 당일 손익 cushion이 있을 때만 size cap 상향. 영상 사례는 초기 10k shares 제한 후 $5k+ cushion 확보 시 약 20~22k shares까지 확대.

## 7. 진입 금지 조건
- 첫 alert 직후 고점까지 수직 상승한 1봉을 market order로 추격.
- 200MA 같은 명확한 상위 저항 바로 아래에서 risk/reward가 1:1 미만.
- `first_new_high_reject = true`: 신고가를 만들자마자 윗꼬리 50% 이상 + 종가가 pivot 아래.
- `range_per_bar_pct > max_stop_pct`: 10초/1분봉 한 개 range가 허용 손절폭을 초과.
- 이미 여러 차례 false breakout 후 spread가 확대되고 호가가 얇아진 구간.
- trader rehab 상태 또는 전일/당일 drawdown 상태에서 cushion 없이 full size 진입.

## 8. 손절 조건
- 기본: 눌림 저점 또는 VWAP reclaim 실패선 이탈.
- cup-and-handle: handle low 또는 pivot $3.18 재하회.
- round number play: 돌파 실패 후 round number 아래에서 10초/1분봉 종가 확정.
- 시간 손절: 진입 후 1~3개 10초봉 또는 1개 1분봉 안에 확장하지 못하고 체결강도가 약해지면 축소/청산.
- 계정 리스크: 당일 red 전환 또는 max loss 근접 시 즉시 중단.

## 9. 익절 조건 / 트레일링 조건
- 1차: 다음 round number 또는 직전 HOD 근처에서 1/2 청산.
- 2차: halt level 또는 급등 연장 구간에서 분할 청산.
- trailing: 10초/1분 higher low 이탈, VWAP 재이탈, 또는 윗꼬리 cluster 2회 발생 시 잔여 정리.
- squeeze outlier는 끝까지 보유보다 scalp 반복이 원 출처와 더 일치합니다. 영상에서도 $2.70→$12 전체를 잡는 것은 불가능하다고 명시합니다.

## 10. 필터 조건
- 시간대: 미국 장전 8:00~9:30 scanner 포착 후 정규장 초반까지. 정규장 이후 halt/stop/market order로 range가 과도해지면 금지 또는 size 축소.
- 거래량: `cum_volume / float >= 1`, `breakout_volume_ratio >= 1.5`.
- 변동성: 1분 ATR이 계좌 허용 손절폭의 1배 이하일 때만 full size.
- 시장 방향: 지수/소형주 risk-on, 같은 테마(AI 등) 동조.
- 종목 선정: leading percentage gainer, low float, breaking news, 높은 float turnover.
- 뉴스/테마: AI, 규제 변화, 계약/임상/실적 등 당일 신규 catalyst 우선.

## 11. 실패 패턴과 회피 규칙
- false breakout: 새 고점 직후 장대 윗꼬리 + 거래량 급증 + pivot 아래 종가. 다음 돌파는 확인봉 전까지 금지.
- red-to-green 실패: 뉴스 후 전일 종가 아래로 재하락하면 초기 squeeze 논리 약화.
- 200MA 저항 실패: daily 200MA 바로 아래에서 반복 rejection.
- margin/liquidity shock: 증거금 요건 상향으로 long forced selling 가능. 레버리지 의존 전략 금지.
- halt 이후 dip-and-rip은 수익 잠재력이 크지만 손절 불가능 구간이 생기므로 별도 전략으로 분리.

## 12. 백테스트 가능성
- 등급: A-
- 정량화 가능 항목:
  - scanner time, news flag, float, cumulative volume, float turnover
  - VWAP reclaim, cup-and-handle pivot, round number proximity
  - pullback depth, pullback duration, volume contraction/expansion
  - false breakout wick ratio, 1m ATR risk
- 구현 난이도: 중간. 미국주는 float/news/장전 10초 데이터가 필요하며, 국내·코인은 데이터 대체 정의가 필요합니다.
- 추가 정의 필요사항:
  - `breaking_news_quality_score`
  - `short_pressure_proxy`
  - `halt_level_distance`
  - `account_cushion_size_rule`

## 13. 기계화 규칙 초안
```pseudo
for symbol in scanner:
    if not news_today(symbol): continue
    if day_gain_pct(symbol) < 50: continue
    if rel_volume(symbol) < 10: continue
    if float_turnover(symbol) < 1.0: continue
    if one_min_atr_pct(symbol) > max_stop_pct: continue

    setup = detect_pullback_after_impulse(symbol)
    if setup.retrace_pct not in [20, 60]: continue
    if close_above_vwap(symbol) and break_minor_pivot(symbol):
        entry = ask_or_stop_limit(symbol)
        stop = min(setup.pullback_low, vwap(symbol) - buffer)
        if expected_rr(entry, stop, next_round_or_hod(symbol)) < 1.5: continue
        size = base_size
        if daily_profit_cushion > cushion_threshold:
            size = min(size * 2, max_size_cap)
        buy(symbol, size, entry, stop)
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: 장전 뉴스+거래대금 상위+유통주식수 회전율 급증 종목에서 VWAP 재돌파 눌림만 허용. VI 직전/직후는 `halt_level_distance`로 size 축소.
- 코인: 거래소 공지/상장/테마 뉴스 후 5분 VWAP reclaim과 funding/short liquidation spike를 결합. low-float 대신 order book depth/24h turnover를 사용.

## 15. 리스크/반대 시나리오
- easy-to-borrow 종목은 숏 압력이 지속될 수 있어 squeeze가 실패하면 round trip이 빠릅니다.
- float turnover가 높아도 회사 ATM/워런트/기관 매도 물량이 나오면 매수세를 흡수합니다.
- 영상 사례는 극단적 변동성 구간이라 슬리피지와 체결 실패를 보수적으로 잡아야 합니다.

## 16. 후속 검증 질문
1. VWAP reclaim 직후 진입과 reclaim 후 minor high 돌파 진입 중 어느 쪽의 기대값이 높은가?
2. float turnover 1배, 3배, 5배 기준별 성과 차이는?
3. 200MA 저항 근처에서 breakout 성공률은 얼마나 낮아지는가?
4. 국내 VI 종목에서 halt 직전 진입 금지 거리를 몇 %로 둘 것인가?
