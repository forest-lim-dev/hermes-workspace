# 064. 선행 급등주 high-of-day 재돌파/라인인더샌드 브레이크아웃 스캘프

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: +$21,690.15 on 3 Stocks Up Over 100% TODAY
- URL: https://www.youtube.com/watch?v=TV3rb-Tl_kM
- 수집일: 2026-05-13
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/TV3rb-Tl_kM.txt`
- 핵심 근거 구간:
  - 00:02:24~00:02:40: S&P500/IWM이 고점 부근, FCHL이 leading gapper 및 halt, 1.45억주 거래량, pop→pullback→rally.
  - 00:04:13~00:04:27: 한 종목이 계속 올라가면 새 setup이 형성될 때마다 반복 거래 가능.
  - 00:08:51~00:10:05: micro pullback 추격을 피하고, pullback 후 curl에서 high-of-day retest를 노린 진입. $3.80~3.85 “line in the sand” 돌파로 $4 및 고점 재시험 기대.
  - 00:09:24~00:10:19: topping tail이 반복되면 가짜 돌파/익절 지연 리스크.
  - 00:10:53~00:11:17: 재돌파 실패 및 tape 판독 어려움으로 재진입 회피.

## 2. 전략 분류
- 신고점돌파매매 / 매수 전략
- 혼합 요소: 돌파 전 눌림·curl 대기 후 high-of-day retest를 노리는 breakout-pullback hybrid

## 3. 전략 요약
당일 100% 이상 급등한 leading gainer가 첫 급등 후 pullback/curl을 만들고, 직전 저항보다 약간 아래의 “line in the sand”를 돌파할 때 선진입하여 $4·high-of-day·halt level 재돌파를 짧게 노리는 스캘프입니다.

- 자산군: 미국 소형 모멘텀주. 국내 급등주/코인 단타로 변형 가능.
- 시간프레임: 1분봉 중심, 5분봉 구조 확인.
- 전략 유형: 매수-only 신고점·당일고점 재돌파, 빠른 분할익절.

## 4. 시장/종목 선행 조건
1. **시장 환경**
   - 소형주 모멘텀 장세가 선행되어야 합니다.
   - 원문은 S&P500과 IWM이 고점 근처로 회복하고, 여러 종목이 +100% 이상 움직이는 환경을 언급합니다.
2. **종목 강도**
   - top % gainer 또는 leading gapper.
   - 당일 +100% 이상 상승, 또는 $1.80 → $3.60, $4.50 → $8처럼 단시간 50~100% impulse.
3. **거래량/유동성**
   - 충분한 거래량 필요. 원문 예시는 1.45억주, 6천만주 등 매우 높은 관심 종목.
   - 단, 과도하게 crowded되어 bid/offer가 두껍고 topping tail이 반복되면 품질 하락.
4. **돌파 후보 레벨**
   - high-of-day, round number($4), half-dollar, halt level, 직전 topping tail 고점.

## 5. 진입 준비 조건
- “상단 추격”이 아니라, 선행 급등 후 pullback이 발생하고 다시 curl하는 구간을 대기합니다.
- 직전 high-of-day 바로 아래에 실제 매수세가 붙는 조기 트리거를 찾습니다.
- 원문 예시에서는 명확한 $4 돌파보다 조금 이른 $3.80~3.85를 line in the sand로 잡았습니다.
- 진입 전 topping tail 빈도와 윗꼬리 비율을 확인합니다.

## 6. 매수 조건 / 진입 트리거
### 고점 재돌파 선행 진입형
1. `day_gain_pct >= 100%` 또는 top gainer rank 상위권.
2. 첫 고점 이후 `pullback_pct >= 10%` 또는 1분봉 3개 이상 조정.
3. 눌림 후 1분봉 저점이 높아지고, 직전 소고점을 돌파.
4. `line_in_sand` 정의:
   - `prior_HOD - 0.2~0.5 * recent_1m_ATR`, 또는
   - round number 직전 2~5호가 아래, 또는
   - 직전 topping tail cluster 상단.
5. 가격이 `line_in_sand`를 거래량 증가와 함께 돌파하면 starter 진입.
6. 목표는 `prior_HOD`, round number, halt level/re-halt 가능 구간.

### 확인형
- `line_in_sand` 돌파 후 1분봉 종가가 기준선 위에서 유지되고, 다음 봉이 고점을 갱신하면 진입.
- 선행 진입형보다 체결은 늦지만 false breakout 감소 가능.

## 7. 진입 금지 조건
- high-of-day 부근마다 topping tail이 2~3회 이상 반복되고, 종가가 저항 위에 남지 못함.
- 9:30 정규장 개장 직후 stop/market order/halt level로 swings가 급격히 커져 1R 손절이 불가능함.
- 이미 “thickly traded” 상태가 되어 tape 판독이 어렵고, bid/offer가 과밀하게 쌓임.
- 재돌파 실패 후 다시 curl하더라도 직전보다 거래량이 줄어듦.
- 당일 수익을 크게 확보한 뒤 심리적으로 더 큰 수익을 추구하는 구간. 원문은 큰 unrealized profit을 일부 반납한 사례를 제시합니다.

## 8. 손절 조건
- 기본 손절: `line_in_sand` 재이탈 또는 진입봉 저가 이탈.
- 구조 손절: pullback low 이탈.
- 즉시 손절: 돌파 직후 장대 윗꼬리/장대음봉이 발생하고 종가가 기준선 아래.
- 변동성 손절: 1분봉 range가 사전 허용 손실의 1.5배 이상이면 진입 취소 또는 강제 축소.
- 시간 손절: 1~2개 1분봉 안에 HOD 방향으로 확장하지 못하면 청산.

## 9. 익절 조건 / 트레일링 조건
- 1차 익절: prior high-of-day 직전 또는 round number 직전.
- 2차 익절: high-of-day 돌파 후 re-halt/다음 심리 가격대.
- trailing:
  - 가격이 목표에 도달하면 잔량 stop을 breakeven 또는 직전 1분봉 저가로 올립니다.
  - topping tail이 나오면 잔량의 50~100% 즉시 정리.
- 본 전략은 큰 추세 보유보다 “setup이 다시 형성되면 재거래”를 선호합니다.

## 10. 필터 조건
- 시간대:
  - 프리마켓 07:00~09:25: tape가 가볍고 line-in-sand가 더 잘 작동할 수 있음.
  - 정규장 09:30 이후: stop/market order와 halt level로 변동성이 증폭되므로 size 축소.
- 거래량:
  - 돌파봉 1분 거래량이 직전 20개 1분봉 평균의 1.5~3배 이상.
  - 단, 누적 거래량이 과도하게 커져 가격 진행이 둔화되면 crowded penalty 적용.
- 변동성:
  - `recent_1m_ATR / price`가 계좌 risk budget 이하.
- 시장 방향:
  - IWM/소형주 지수 또는 동종 급등주 breadth가 양호할 때 우선.
- 종목 선정:
  - leading gapper, high relative volume, 뉴스/테마, high-of-day 근접 종목.

## 11. 실패 패턴과 회피 규칙
1. **topping tail cluster**
   - 1분봉 윗꼬리가 전체 range의 40~50% 이상인 봉이 연속 출현하면 돌파 신뢰도 하락.
2. **line-in-sand 돌파 후 즉시 재이탈**
   - 기준선 위 종가 유지 실패 시 가짜 돌파로 처리.
3. **고점 재돌파 실패 후 거래량 감소**
   - 두 번째 curl에서 거래량이 줄면 재진입 금지.
4. **개장 직후 volatility expansion**
   - 정규장 개장 후 $6→$5, $8.40→$7.80 같은 큰 swing은 손절/체결 품질을 악화.
5. **unrealized profit 반납**
   - HOD 도달 시 일부 익절 없이 전량 보유하면 topping tail 반락에서 수익 반납 가능.

## 12. 백테스트 가능성
- 등급: **A**
- 정량화 가능 항목:
  - top gainer rank, day_gain_pct, rel_volume
  - prior_HOD, line_in_sand, round number proximity
  - pullback_pct, pullback_bars, higher_low 여부
  - breakout_volume_ratio, close_hold, upper_wick_ratio
  - time-of-day, halt 발생 여부, 1분 ATR/price
  - 선행 진입형 vs 1분봉 종가 확인형 성과 비교
- 구현 난이도: 중간. 분봉 데이터만으로 상당 부분 구현 가능하나 halt/뉴스/프리마켓 데이터가 있으면 성능 평가가 좋아집니다.
- 추가 정의 필요사항:
  - line-in-sand 자동 산출 방식
  - topping tail cluster 기준
  - crowded 상태를 거래량·호가 없이 대체하는 proxy

## 13. 기계화 규칙 초안
```pseudo
for symbol in intraday_scanner:
    if top_gainer_rank(symbol) > 20: continue
    if day_gain_pct(symbol) < 80: continue
    if rel_volume(symbol) < 5: continue
    if price_distance_to_HOD(symbol) > 0.15: continue
    if recent_1m_ATR_pct(symbol) > account_max_stop_pct: continue

    HOD = high_of_day(symbol)
    pullback_low = recent_swing_low_after(HOD)
    if pullback_bars < 3: continue
    if current_low <= pullback_low: continue

    line = max(recent_pivot_high, HOD - 0.5 * ATR_1m, nearest_round_level_below(HOD))
    if upper_wick_cluster(last_5_bars) >= 3: continue

    if cross_above(price, line) and volume_1m > avg_volume_20_1m * 1.5:
        enter_long(size=risk_based(stop=min(line - 0.1*ATR_1m, last_1m_low)))

    if close_1m < line: exit_all()
    take_partial(HOD - tick_buffer)
    if break_above(HOD) and close_1m_above(HOD): trail_stop(last_1m_low)
    if upper_wick_ratio(current_bar) > 0.5: exit_remaining()
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식:
  - 거래대금 상위·등락률 상위·뉴스 급등주에서 당일고점 재돌파를 테스트.
  - line-in-sand는 당일고점 바로 아래 호가단위 3~10틱, VI 기준가, 정수 가격, 전고점으로 정의.
  - VI 근접 시 신규 진입보다 VI 후 첫 1~3분봉 종가 유지 확인형을 별도 테스트.
- 코인:
  - 거래소 상장/공지·테마 급등 코인에서 5분봉 high 재돌파 전 1분봉 line-in-sand를 사용.
  - 펀딩비·BTC 방향·거래소별 김치프리미엄/스프레드를 필터로 추가.

## 15. 리스크/반대 시나리오
- 신고점돌파는 가장 많은 참여자가 보는 구간이라 fakeout이 빈번합니다.
- 소형 급등주는 halt, 공매도 가능 여부, 유통주식 수, 호가 공백이 손절 실행을 어렵게 할 수 있습니다.
- 시장이 약하거나 소형주 breadth가 나쁘면 선행 급등주도 high-of-day 재돌파가 실패하기 쉽습니다.
- 본 문서는 교육·리서치 목적이며 특정 종목 매수/매도 지시가 아닙니다.

## 16. 후속 검증 질문
1. `line_in_sand = HOD - 0.5ATR` 방식과 round number 직전 진입 방식 중 어느 쪽이 성과가 좋은가?
2. 1분봉 종가 확인형이 선행 진입형 대비 손익비를 얼마나 개선하는가?
3. topping tail cluster를 몇 개 봉/몇 % 윗꼬리로 정의해야 false breakout을 잘 걸러내는가?
4. 국내주식 VI 전 돌파와 VI 후 종가 유지 확인형을 별도 전략으로 분리해야 하는가?
