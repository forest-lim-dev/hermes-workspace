# 063. Day-1 뉴스 급등주 눌림 후 curl/retest 스캘프

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: 3 Stocks Up Over 100% With More Breaking News!
- URL: https://www.youtube.com/watch?v=9Q48uYDUPjg
- 수집일: 2026-05-13
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/9Q48uYDUPjg.txt`
- 핵심 근거 구간:
  - 00:02:30~00:03:08: after-hours 뉴스 → $1.50에서 $5 급등 → 눌림 → $5 돌파/재상승, 4천만주 거래량, 익절.
  - 00:03:18~00:03:27: $5.50 half-dollar 및 $5.78 돌파를 기대했으나 신고가 재돌파 실패 후 철수.
  - 00:05:58~00:06:16: dip 매수 후 curl 반등은 성공했지만 add 이후 장대음봉 rejection으로 큰 손실.
  - 00:06:19~00:06:26: 높은 승률이라도 평균 손실이 크면 전략 손익이 훼손됨.

## 2. 전략 분류
- 눌림목매매 / 매수 전략
- 보조 성격: 뉴스·갭·당일 leading gainer 모멘텀 스캘프

## 3. 전략 요약
뉴스로 100% 이상 급등한 저가·소형주가 첫 급등 후 짧게 눌린 뒤 round number/half-dollar 또는 직전 고점 방향으로 다시 curl할 때만 짧게 진입하고, 실패 시 즉시 철수하는 Day-1 눌림목 스캘프입니다.

- 자산군: 미국 저가·소형주 중심. 국내주식/코인은 변형 적용 가능.
- 시간프레임: 프리마켓~정규장 초반, 1분봉/5분봉, Level 2/체결 흐름 보조.
- 전략 유형: 매수-only 모멘텀 continuation, 빠른 base-hit 익절.

## 4. 시장/종목 선행 조건
1. **Day-1 catalyst**
   - 당일 또는 전일 장후 신규 뉴스가 있어야 합니다.
   - 기존 급등의 2일차 continuation보다 Day-1이 가장 깨끗하다는 관찰을 전제로 둡니다.
2. **선행 급등**
   - 뉴스 후 기준가 대비 최소 +50%, 우선 +100% 이상 급등.
   - 예시 원문: $1.50 → $5, 또는 전일 800% 급등 후 후속 급등주 출현.
3. **거래량/관심도**
   - 절대 거래량이 매우 커야 합니다. 원문 예시는 4천만주.
   - 스캐너 상위 등락률/거래량 종목이어야 하며, 시장 내 leading gainer 후보가 유리합니다.
4. **가격대/호가 안정성**
   - 너무 고가가 되어 1분봉 한 개의 변동폭이 계좌 허용 손실을 초과하면 제외합니다.
   - $18~$42처럼 한 캔들 저가가 10포인트씩 흔들리는 구조는 회피 대상으로 해석합니다.

## 5. 진입 준비 조건
- 첫 급등 이후 곧바로 추격하지 않고, 최소 1~3개의 1분봉 눌림 또는 flag/curl 구조를 기다립니다.
- 눌림 구간에서 전저점이 높아지거나, 매도 압력이 둔화되어야 합니다.
- round number($5, $6 등), half-dollar($5.50), 직전 high-of-day, intraday resistance를 미리 표시합니다.
- 눌림 후 재상승이 위 기준선까지 충분한 공간을 남겨야 합니다.

## 6. 매수 조건 / 진입 트리거
### 기본 트리거
1. `news_catalyst == true`
2. `gap_or_intraday_move_pct >= +50~100%`
3. 첫 급등 후 `pullback_bars >= 2` 또는 직전 고점 대비 `pullback_pct >= 8~20%`
4. 눌림 저점 이탈 없이 1분봉 고점이 높아짐
5. 아래 중 하나 발생 시 starter 진입:
   - 눌림 후 첫 1분봉 고점 돌파
   - round number/half-dollar 돌파 직전 선취매(예: $5.50 돌파 기대)
   - 직전 resistance를 거래량 증가와 함께 reclaim
6. 확장 진입/add는 최초 진입가 대비 이익이 난 상태에서만 허용합니다.

### 원문 기반 구체 예
- MYSE: after-hours 뉴스로 $1.50 → $5 급등, 눌림 후 $5 돌파가 깨끗하게 나오며 진입/익절.
- BTOG: dip 매수 후 curl은 맞았지만 추가 매수 뒤 장대음봉 rejection. 따라서 add는 candle close 확인 또는 직전 고점 돌파 확인 후로 제한해야 합니다.

## 7. 진입 금지 조건
- 2일차 continuation만 남은 종목: Day-1보다 패턴이 지저분할 수 있어 우선순위 하향.
- 이미 4천만주 이상 거래되어 호가가 과밀하고 topping/rejection이 반복되는 경우.
- 가격이 너무 높아 1분봉 평균 range가 허용 손절폭보다 큰 경우.
- spread가 넓고 주문당 체결량이 작아 슬리피지가 커지는 종목.
- 눌림 시간이 너무 짧아 단순 1~2분 shakeout인지 확인이 어려운 경우. 원문에서도 “pullback for more than just two minutes” 필요성을 언급.
- 당일 손실/드로다운 상태에서 계좌 cushion이 없을 때 고변동 종목 진입 금지.

## 8. 손절 조건
- 기본: 눌림 저점 또는 진입 직전 1분봉 저가 이탈.
- 빠른 실패: 돌파 기대선($5.50, $5.78 등) 위로 붙지 못하고 즉시 장대음봉/rejection이 나오면 시장가 철수.
- 시간 손절: 진입 후 1~3개 1분봉 안에 high-of-day 방향으로 확장하지 못하면 축소/청산.
- 계좌 손절: 1회 손실이 평균 base-hit 이익의 1.0~1.5배를 넘지 않도록 강제. 원문상 작은 승리 다수 + 큰 손실 1회가 문제였기 때문입니다.

## 9. 익절 조건 / 트레일링 조건
- 1차 익절: 직전 고점, round number, half-dollar, high-of-day 근처.
- 2차 익절: high-of-day 돌파 시 일부 잔량만 추적.
- topping tail 또는 돌파 후 즉시 종가가 기준선 아래로 복귀하면 잔량 청산.
- 본 전략은 “getting in, getting green, getting out”에 가깝게 base-hit 중심으로 설계합니다.

## 10. 필터 조건
- 시간대: 미국 프리마켓 07:00~09:30, 정규장 초반 09:30~10:30을 우선. 국내는 09:00~10:00, 코인은 뉴스 발생 직후 30~90분.
- 거래량: 당일 상대거래량 5배 이상, 분봉 거래량이 직전 20개 평균 대비 1.5배 이상 재증가.
- 변동성: 1분 ATR 또는 최근 3개 봉 평균 range가 허용 손절폭 이하.
- 시장 방향: 소형주 모멘텀 장세가 유리. 원문은 전일/당일 다수 100% 이상 급등주가 연쇄적으로 등장한 환경.
- 종목 선정: news catalyst, top % gainer, 저가·고거래량, 호가 체결이 빠른 종목.
- 뉴스/테마 여부: 단순 기술적 급등보다 명확한 headline 선호.

## 11. 실패 패턴과 회피 규칙
1. **큰 range 고가화**
   - $42 고점 후 다음 캔들 저가 $32처럼 손절 불가능한 폭이 나오면 거래 금지.
2. **double top 후 짧은 눌림만 발생**
   - $5 double top에서 2분 이하 눌림은 confirmation 부족.
3. **add 후 장대음봉 rejection**
   - 이익 구간 add라도 돌파봉 종가 확인 전 과도한 size-up 금지.
4. **red-on-day 전환**
   - BTOG처럼 종국에 당일 음전하는 종목은 초반 작은 반등 이후 빠르게 momentum이 소멸할 수 있습니다.
5. **승률 착시**
   - 75~80% 승률이어도 평균 손실이 평균 이익보다 3~5배 크면 자동매매에서는 제외 또는 size 축소.

## 12. 백테스트 가능성
- 등급: **A-**
- 정량화 가능 항목:
  - news 발생 시각, 당일 상승률, 상대거래량, top gainer rank
  - pullback bars, pullback depth, low hold 여부
  - round/half-dollar proximity, high-of-day distance
  - 1분봉 rejection candle, upper wick ratio, red candle range
  - 평균 승리/평균 손실 비율, add 여부별 성과
- 구현 난이도: 중간. 뉴스 태그와 프리마켓 분봉 데이터가 필요합니다.
- 추가 정의 필요사항:
  - “뉴스 품질” 점수화
  - “too crowded”를 호가 데이터 없이 거래량/체결빈도로 대체할 기준
  - 코인·국내주식의 round number 정의

## 13. 기계화 규칙 초안
```pseudo
for symbol in universe:
    if not has_fresh_news(symbol, within_hours=18): continue
    if day_gain_pct(symbol) < 50: continue
    if rel_volume(symbol) < 5: continue
    if top_gainer_rank(symbol) > 20: continue
    if one_min_atr_pct(symbol) > max_allowed_atr_pct(account_risk): continue

    impulse_high = high_since_news(symbol)
    pullback_low = lowest_low_after(impulse_high)
    pullback_pct = (impulse_high - pullback_low) / impulse_high

    if pullback_bars < 2 or pullback_pct < 0.08: wait
    if current_low < pullback_low: invalidate

    trigger = break_above(last_1m_pivot_high) or reclaim(round_or_half_level)
    if trigger and volume_1m > avg_volume_20_1m * 1.5:
        enter_starter(size = risk_based_size(stop=pullback_low))
        stop = min(pullback_low, entry_candle_low)

    if unrealized_profit > initial_risk and break_above(next_level):
        add_small_only_if(close_1m_above_level)

    take_profit_at([prior_high, round_number, high_of_day])
    exit_if(close_1m_below_trigger_level or upper_wick_ratio > 0.5 or red_candle_range > 1.5*avg_range)
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식:
  - 장전/장중 뉴스 + 거래대금 상위 + 전일 대비 급등 종목에 적용.
  - VI 진입 전후는 변동성 폭이 크므로, VI 해제 직후 첫 1~3분봉 range가 계좌 손절폭을 초과하면 금지.
  - round number 대신 호가단위 변곡 가격, 전일고가, 장중 고점, VI 기준가를 사용.
- 코인:
  - 상장/거래소 공지/테마 뉴스 후 5분봉 급등 → 1~3분봉 눌림 → 직전 고점 retest.
  - BTC/ETH 5분봉이 VWAP 아래로 급락하면 알트 눌림 반등 신뢰도 하향.

## 15. 리스크/반대 시나리오
- 뉴스 급등주는 유동성은 많지만 반대 방향 유동성도 많아 장대음봉 손실이 큽니다.
- 프리마켓/정규장 초반 호가 공백, 거래정지, VI/서킷, 시장가 슬리피지가 실제 성과를 크게 훼손할 수 있습니다.
- “놓친 급등”을 보상하려는 심리로 늦은 고가 추격이 발생하기 쉽습니다.
- 본 문서는 교육·리서치 목적이며 매수/매도 지시가 아닙니다.

## 16. 후속 검증 질문
1. Day-1 뉴스 종목에서 2분 눌림 vs 5분 이상 눌림 중 기대값이 높은 조건은 무엇인가?
2. round number 선취매와 실제 돌파 후 진입의 손익비 차이는?
3. add는 즉시 돌파 중 추가와 1분봉 종가 확인 후 추가 중 어느 쪽이 큰 손실을 줄이는가?
4. 국내 VI 종목에서 VI 직후 첫 눌림은 본 전략과 같은 방식으로 테스트 가능한가?
