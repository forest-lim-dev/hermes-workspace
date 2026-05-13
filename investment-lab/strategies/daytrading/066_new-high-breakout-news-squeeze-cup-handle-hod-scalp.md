# 066. News Squeeze Cup-and-Handle 신고점돌파 스캘프

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: `Here we go! Another Short Squeeze!`
- URL: https://www.youtube.com/watch?v=TZkQiVOR5vc
- 수집일: 2026-05-13, 문서화: 2026-05-14
- 원문 위치: `data/raw_transcripts/youtube/TZkQiVOR5vc.txt`
- 주요 근거 타임스탬프:
  - 02:35~02:49: EFOI가 9:00am breaking news 후 $2.50→$5.50 급등 후 하락
  - 03:34~03:43: 9:00am에 +100% 이상 상승하며 entire market leading gainer가 됨
  - 03:49~04:08: 첫 pop 후 pullback, $4 돌파 기대, $4.50 add, stall 시 소익절
  - 04:22~04:34: 약한 price action으로 이탈 후 $5.50→$9.50 대형 돌파는 미참여
  - 04:39~05:08: 정규장 이후 stop order/market order/halt level이 swing을 증폭, $1/share swing으로 risk management 난화
  - 08:03~09:00: AI catalyst, market all-time highs, risk-on 배경
  - 09:38~10:08: 가장 큰 move와 관리 가능한 move의 시간대 구분 필요

## 2. 전략 분류
- 신고점돌파매매 / 매수 전략
- 보조 성격: 돌파 진입 금지 필터, 시간대·halt risk overlay

## 3. 전략 요약
- 장전/개장 직전 breaking news로 당일 leading gainer가 된 종목이 첫 고점 돌파 전 cup-and-handle 또는 pullback-curl을 만든 뒤 $4, $5.50 같은 round/half-dollar pivot을 재돌파할 때만 진입하는 신고점돌파 전략입니다.
- 자산군: 미국 소형주 원형, 국내 뉴스·테마 급등주/코인 급등 알트 응용
- 시간프레임: 1분 진입, 10초 보조, 1~5분 청산
- 전략 유형: 매수 전략

## 4. 시장/종목 선행 조건
1. `time_of_catalyst`: 장전 또는 9:00 전후 breaking news. 영상 사례는 9:00am 뉴스.
2. `leading_gainer_rank <= 3`: 순간적으로 market-wide leading gainer가 된 종목만 추적.
3. `day_gain_pct >= 100`: 첫 impulse만으로 +100% 이상 또는 이에 준하는 급등.
4. `theme_strength = true`: AI catalyst, 전체 시장 신고가, oil/macro risk 완화 등 위험선호 배경.
5. `manageable_range = true`: 1분봉 range가 허용 손절폭 이내인 시간대. 영상은 개장 후 $1/share swing 때문에 관리 난이도가 상승했습니다.

## 5. 진입 준비 조건
- 첫 급등봉에서 바로 따라가지 않고 다음 구조를 대기합니다.
  1. 첫 고점 형성: 예시 $5.50
  2. pullback: 너무 깊지 않게 전일 종가/주요 VWAP 위 또는 빠른 회복 가능 구간
  3. curl: 저점을 높이고 $4, $4.50 같은 중간 pivot에 접근
  4. 신고점/중간고점 재돌파 전 거래량 재증가
- `cup_handle_ready = true`:
  - cup: 급등 후 하락·회복으로 U/V형 복원
  - handle: pivot 바로 아래 2~5개 1분봉 좁은 range
  - breakout pivot: 직전 minor high, round number, half-dollar, HOD 직전 line

## 6. 매수 조건 / 진입 트리거
1. 필수 트리거:
   - `price > VWAP`
   - `breakout_level` 돌파: $4, $4.50, $5.50, HOD 등
   - `breakout_volume_ratio >= 1.5`
2. 조기 트리거:
   - HOD 돌파를 기다리지 않고 HOD 아래 `line_in_sand = HOD - 0.2~0.5 * 1m_ATR`에서 ask가 붙고 pullback low가 유지될 때 starter 진입.
3. 확인 트리거:
   - 1분봉 종가가 pivot 위에서 닫히거나, 돌파 직후 눌림이 pivot 위에서 지지될 때 add.
4. add 금지 예외:
   - $4.50 add 후 바로 stall한 사례처럼 돌파 이후 1~2개 10초봉 안에 확장하지 않으면 add를 취소하고 starter만 남깁니다.

## 7. 진입 금지 조건
- `post_open_halt_whip = true`: 정규장 개장 후 halt level/stop order/market order가 겹쳐 1분봉 range가 $1 이상 또는 가격 대비 10~15% 이상.
- `stall_after_add = true`: add 가격 위에서 호가가 붙지 못하고 즉시 매도 체결이 우세.
- `round_trip_risk = true`: 뉴스 후 +100% 상승했다가 전일 종가 근처/음전 가능성이 보이는 경우.
- `no_cushion_full_size = true`: 이미 큰 일간 손실·월간 drawdown 상태에서 cushion 없이 size-up.
- 큰 수익을 놓친 FOMO로 $5.50→$9.50 같은 후행 수직봉을 추격.

## 8. 손절 조건
- 기본: 돌파 pivot 재하회. 예: $4 돌파 진입이면 $3.90~$3.95 또는 직전 눌림 저점.
- HOD 직전 line 진입: line 이탈 또는 pullback low 이탈.
- false breakout: 신고점 돌파 후 10초/1분봉 종가가 기준선 아래 + 윗꼬리 50% 이상이면 즉시 청산.
- volatility stop: `1m_ATR > planned_stop * 1.5`가 되면 신규 진입 중지, 보유분 축소.
- daily stop: 당일 이익을 크게 확보한 뒤에는 최대 손실보다 `profit giveback limit`을 우선 적용합니다.

## 9. 익절 조건 / 트레일링 조건
- 1차 익절: 다음 half-dollar/round number 또는 HOD retest.
- 2차 익절: halt level 접근, 급등봉 연속, 또는 +1R~2R 도달.
- trailing: 직전 10초/1분 higher low 이탈, pivot 재하회, VWAP 재이탈.
- profit protection: 당일 큰 cushion이 생긴 뒤에는 후반부 수익 기회보다 giveback 회피를 우선합니다.

## 10. 필터 조건
- 시간대:
  - 장전 8:00~9:25: 비교적 관리 가능한 돌파·눌림만 선호.
  - 9:30 이후: 유동성은 증가하지만 stop/market/halt swing이 커져 size 30~50% 축소 또는 확인형 진입만 허용.
- 거래량: 돌파봉 거래량이 최근 20개 1분봉 평균의 1.5배 이상.
- 변동성: 1분 ATR/가격이 10%를 초과하면 자동매매 신규 진입 금지 후보.
- 시장 방향: 지수 all-time high 또는 risk-on, 테마 동조.
- 종목 선정: 당일 등락률 상위, 뉴스, 낮은 유동/강한 회전율, HOD 근처.
- 뉴스/테마: AI처럼 당일 참여자가 몰릴 수 있는 narrative 우선.

## 11. 실패 패턴과 회피 규칙
1. early pop and full retrace: $2.50→$5.50 후 바로 전일 종가 방향으로 하락하면 round trip 위험.
2. stalled add: $4.50 add 후 HOD로 연결되지 않으면 작은 이익/본전 청산.
3. post-open oversized swing: $6→$5, $8.40→$7.80처럼 1분 내 손절 허용폭을 초과하는 whip.
4. psychological FOMO: 놓친 $5.50→$9.50 구간을 뒤늦게 따라가면 손절선이 사라짐.
5. news exhaustion: 뉴스 최초 반응 이후 거래량은 유지되지만 고점이 낮아지면 돌파 전략 중지.

## 12. 백테스트 가능성
- 등급: A
- 정량화 가능 항목:
  - news timestamp, scanner rank, day_gain_pct
  - HOD, minor pivot, round/half-dollar breakout
  - breakout volume ratio, 1m close hold, upper wick ratio
  - post-open range expansion, halt proximity, giveback limit
- 구현 난이도: 중간. 가격·거래량·VWAP 데이터로 대부분 구현 가능하며, news quality와 halt level은 별도 데이터가 필요합니다.
- 추가 정의 필요사항:
  - `leading_gainer_rank` 실시간 계산 범위
  - `manageable_move_window`
  - `halt_level_distance_pct`
  - `profit_giveback_limit`

## 13. 기계화 규칙 초안
```pseudo
for symbol in intraday_gainers:
    if not news_today(symbol): continue
    if rank_by_day_gain(symbol) > 3: continue
    if day_gain_pct(symbol) < 100: continue
    if not price_above_vwap(symbol): continue
    if one_min_atr_pct(symbol) > 10: continue

    pivot = detect_minor_pivot_or_round_level(symbol)
    if not pivot: continue
    if breakout_volume_ratio(symbol, pivot) < 1.5: continue
    if upper_wick_ratio(last_bar(symbol)) > 0.5: continue

    if break_above(pivot) and close_hold(pivot, bars=1):
        stop = max(pivot - buffer, recent_pullback_low(symbol))
        target1 = next_round_or_hod(symbol)
        if expected_rr(entry_price, stop, target1) >= 1.5:
            buy(symbol, size_by_range_and_cushion(symbol), entry_price, stop)

    if market_open_phase and halt_distance_pct(symbol) < min_halt_distance:
        reduce_size(0.5)
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: 장전/장중 뉴스로 거래대금 1~3위에 진입한 종목의 전고점·VI 직전 가격·호가 단위 돌파를 사용. VI 근접 시 신규 진입 금지 또는 소량만 허용.
- 코인: 거래소 상장/파트너십 뉴스 후 5분 HOD와 round number 돌파. BTC/ETH가 5분 VWAP 위일 때만 alt breakout 허용.

## 15. 리스크/반대 시나리오
- 가장 큰 상승 구간은 관리 불가능한 변동성과 함께 올 수 있어 자동매매가 의도치 않은 고점 체결을 할 수 있습니다.
- 당일 +100% 이상 종목은 false breakout 빈도가 높고, 한 번의 장대 음봉이 평균 이익을 지울 수 있습니다.
- 뉴스 품질이 약하거나 이미 시장에 알려진 catalyst라면 돌파는 liquidity exit가 될 수 있습니다.

## 16. 후속 검증 질문
1. 장전 돌파와 정규장 후 돌파 중 수익/손실 분포는 어떻게 다른가?
2. `1m_ATR_pct > 10%` 금지 기준이 너무 엄격한가, 혹은 손실 outlier를 충분히 줄이는가?
3. HOD 직접 돌파 진입보다 HOD 아래 line-in-sand 조기 진입의 슬리피지·승률 차이는?
4. 국내 VI/halt 구간에서 돌파 전·후 어느 쪽이 더 기계화 가능한가?
