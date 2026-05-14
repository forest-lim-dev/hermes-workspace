# 069. Daily Level Catalyst Curl 신고점돌파·눌림목 스캘프

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: `Prediction Markets Catalyst Sends Stock Up Over 100%`
- URL: https://www.youtube.com/watch?v=CVBv8tPpyxA
- 수집일/문서화: 2026-05-15
- 원문 위치: `data/raw_transcripts/youtube/CVBv8tPpyxA.txt`
- 주요 근거 타임스탬프:
  - 00:04~00:38: 과거 prediction market catalyst로 $2→$36 급등 후 offering으로 float 증가
  - 00:43~01:12: 계약 실행 뉴스는 강하지 않아 보였고, 시장 관심은 penny stocks에 집중
  - 02:51~03:21: 뉴스 전 선행 상승, easy-to-borrow로 crowded 우려
  - 03:33~04:04: daily levels $5.85/$6.17/$6.73/$7.49/$9.48/$10/$11.75가 순차 저항·목표로 작동
  - 05:01~05:55: $8 돌파 실패·재돌파 후 $9.31~$9.58 pullback curl에서 23c/share 수익
  - 06:08~06:48: ascending volume, doji/topping tail/jack knife candle 이후 cushion 부족으로 중단

## 2. 전략 분류
- 혼합: 신고점돌파매매 + 눌림목매매
- 전략 유형: 매수 전략

## 3. 전략 요약
- 과거 대형 catalyst 이력이 있는 종목이 신규 실행 뉴스로 재급등할 때, daily resistance ladder를 미리 표시하고, 장중 round number/직전 고점 돌파 뒤 짧은 pullback-curl이 발생하면 다음 daily level까지의 짧은 확장을 노리는 스캘프 전략입니다.
- 자산군: 미국 소형주 원형, 국내 이슈 재점화 테마주, 코인 재상장/파트너십 재부각 종목
- 시간프레임: 10초~1분 진입, 1~5분 관리
- 전략 유형: 매수 전략

## 4. 시장/종목 선행 조건
1. `historical_catalyst_memory = true`: 과거 같은 테마/뉴스로 큰 상승 이력이 있어 참여자 기억이 남아 있어야 합니다.
2. `fresh_or_followup_news = true`: 신규 뉴스가 있되, 단순 실행/확인 뉴스는 `quality_score`를 중간 이하로 둡니다.
3. `daily_level_ladder`: 과거 고점·저항을 $5.85, $6.17, $6.73, $7.49, $9.48, $10, $11.75처럼 미리 배열합니다.
4. `easy_to_borrow_penalty`: easy-to-borrow는 숏 crowded와 매도 압력 가능성으로 size를 줄입니다.
5. 같은 시간대 penny stock 과열로 시장 관심이 분산되어 있으면 추격 진입을 피합니다.

## 5. 진입 준비 조건
- 뉴스 전 선행 상승이 있으면 정보 선반영/누군가 먼저 산 정황으로 추격 금지.
- 각 daily level 돌파 후 바로 사지 않고, 다음 중 하나를 기다립니다.
  1. whole dollar($8/$10) 돌파 후 pullback이 얕게 끝남
  2. topping tail 이후 즉시 무너지지 않고 다시 high를 회복
  3. 10초/1분 pullback에서 저점이 상승하고 curl back up 발생
- `pullback_depth_pct`: 직전 impulse의 15~45% 되돌림 선호. 50% 초과는 momentum 약화.
- `ascending_volume`: 신고점 돌파 이전 3~5개 1분봉 거래량이 증가해야 하지만, 윗꼬리 동반 급증은 실패 신호입니다.

## 6. 매수 조건 / 진입 트리거
1. 가격이 직전 daily level을 돌파하고 다음 level까지 최소 1.5R 이상의 공간이 있습니다.
2. round number 또는 intraday high 돌파 후 pullback이 발생합니다.
3. pullback 저점이 VWAP 또는 직전 pivot 위에서 형성됩니다.
4. 10초봉 또는 1분봉이 pullback high를 재돌파하며 `curl_trigger = true`.
5. 예시 진입: $9.31~$9.38 pullback curl 매수, $9.58 부근 base hit 청산.

## 7. 진입 금지 조건
- 뉴스가 강하지 않은데 1차 급등을 chase.
- easy-to-borrow + float 증가 이후인데 squeeze 압력 확인 없이 full size.
- daily level 바로 아래에서 R/R이 1:1 미만.
- jack knife candle: 급등·급락 또는 급락·급등의 긴 wick이 반복되는 구간.
- topping tail/gravestone doji가 연속 발생하고 trader cushion이 없는 상태.
- penny stock 광풍으로 시장 관심이 다른 곳에 집중되어 해당 종목 volume follow-through가 약한 경우.

## 8. 손절 조건
- pullback low 이탈 또는 재돌파한 pivot 재하회.
- whole dollar breakout 실패 후 가격이 round number 아래에서 10초/1분 종가 확정.
- `jack_knife_count >= 2` 이후 신규 진입은 중단, 보유분은 축소.
- 진입 후 1~2개 10초봉 안에 수익권으로 가지 못하면 scalp 실패로 처리합니다.

## 9. 익절 조건 / 트레일링 조건
- 1차: 다음 daily level 또는 round number 직전에서 절반 이상 청산.
- 2차: $10, $11.75처럼 상위 level까지 열려 있으면 10초 higher low를 따라 잔여 추적.
- cushion이 없거나 drawdown 회복 중이면 20~30센트 base hit를 우선합니다.
- gravestone doji, topping tail, jack knife candle 출현 시 잔여 청산.

## 10. 필터 조건
- 시간대: 뉴스 발표 후 장전 8:00~9:30, 정규장 초반. 뉴스 전 선행 상승은 감점.
- 거래량: `ascending_volume = true`, breakout volume이 직전 5봉 평균 대비 1.5배 이상.
- 변동성: 10초봉 range가 손절 허용폭 이하.
- 시장 방향: risk-on 또는 해당 테마 관심 유지. 관심이 초저가주로 과도하게 쏠리면 size 축소.
- 종목 선정: 과거 대형 move 기억, 현재 catalyst, 명확한 daily level ladder.
- 뉴스/테마: prediction market, crypto partnership, AI 등 retail attention을 끄는 테마 선호.

## 11. 실패 패턴과 회피 규칙
- 재탕 follow-up news: 원뉴스보다 약할 수 있어 첫 돌파 chase 금지.
- offering 이후 float 증가: 과거처럼 가볍게 움직이지 않을 수 있습니다.
- easy-to-borrow crowded: 숏 squeeze 압력이 약하고 매도자가 많을 가능성.
- daily level hit-and-reject: 레벨이 존중되는 만큼 바로 아래/직후 rejection도 강할 수 있습니다.

## 12. 백테스트 가능성
- 등급: A-
- 정량화 가능 항목: historical move memory, news timestamp, daily resistance ladder, level distance R/R, pullback depth, curl trigger, jack-knife wick ratio.
- 구현 난이도: 중간. daily level 자동 추출과 10초 데이터가 있으면 구현 가능성이 높습니다.
- 추가 정의 필요사항: `historical_catalyst_memory`, `daily_level_ladder`, `curl_trigger`, `jack_knife_candle`.

## 13. 기계화 규칙 초안
```pseudo
for symbol in news_scanner:
    levels = extract_daily_resistance_levels(symbol, lookback=180d)
    if not has_historical_big_move(symbol, threshold=200pct): continue
    if news_quality_score(symbol) < 1.5: size_cap = starter_only
    if easy_to_borrow(symbol) or float_increased_since_last_run(symbol): size_cap *= 0.5

    current_level = nearest_broken_level(price, levels)
    next_level = next_resistance_above(price, levels)
    if rr_to_level(price, stop_candidate, next_level) < 1.5: continue

    if breakout_then_pullback(symbol) and pullback_depth in 15..45 and curl_rebreak(symbol):
        entry = stop_limit_above(curl_high)
        stop = pullback_low - buffer
        target = min(next_level, next_round_number)
        buy(symbol, size_cap, entry, stop, target)
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: 과거 2차전지/AI/로봇 등으로 상한가 이력이 있는 종목이 후속 공시로 재급등할 때, 전고점·상한가 종가·갭상단을 daily ladder로 설정합니다.
- 코인: 과거 상장/파트너십 급등 이력이 있는 코인이 후속 공지로 재부각되면, 이전 펌핑 고점과 round number를 ladder로 사용합니다.

## 15. 리스크/반대 시나리오
- follow-up news가 약해 보여도 retail memory가 강하면 예상보다 크게 squeeze될 수 있습니다.
- 반대로 과거 급등 후 offering/float 증가가 있으면 동일 테마라도 움직임이 둔화될 수 있습니다.
- 10초봉 기반 전략은 체결 지연과 슬리피지에 민감합니다.

## 16. 후속 검증 질문
1. 과거 200%+ 급등 이력이 있는 종목의 후속 뉴스 intraday breakout 성과는 일반 뉴스주보다 우수한가?
2. daily level까지의 R/R 1.5 이상 필터가 손익비를 개선하는가?
3. jack-knife candle 1회와 2회 이후의 신규 진입 기대값은 어떻게 다른가?
