# 067. Catalyst Quality + Heavy Seller 신고점돌파 필터

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: `+$2,306.80 Trading Leading Percentage Gainers`
- URL: https://www.youtube.com/watch?v=hrZJKJ9NGbk
- 수집일/문서화: 2026-05-15
- 원문 위치: `data/raw_transcripts/youtube/hrZJKJ9NGbk.txt`
- 주요 근거 타임스탬프:
  - 01:13~01:54: leading gainer가 +145%까지 상승 후 전부 반납, 금요일/뉴스 품질/매도 압력 언급
  - 02:17~03:14: ELPW는 중국 기업·당일 뉴스 부재, volume profile상 pop 뒤 강한 매도
  - 03:24~04:06: MACD 양전환·거래량 증가에도 $4 double top 실패
  - 04:15~05:22: false breakout 이후 ask seller가 두꺼워지고 choppy해져 추가 예측 돌파 중단
  - 05:47~08:38: headline 품질/SEC filing/placement agent 충돌, NTIP 뉴스주 재돌파는 짧은 수익 후 rollover

## 2. 전략 분류
- 신고점돌파매매 / 매수 전략 + 진입 금지 필터
- 성격: `breakout candidate`를 매수하기 전에 뉴스 품질과 매도 압력으로 제외하는 보조 규칙

## 3. 전략 요약
- 당일 급등 leading gainer라도 신규·신뢰도 높은 catalyst가 없거나, 돌파 시 ask seller와 윗꼬리가 반복되면 신고점돌파 매수 후보에서 제외하고, 뉴스가 있는 2차 후보의 짧은 재돌파만 제한적으로 거래하는 규칙입니다.
- 자산군: 미국 소형주 원형, 국내 테마주/코인 급등주에 적용 가능
- 시간프레임: 장전 1분·10초, 정규장 초반 1분
- 전략 유형: 매수 전략, 동시에 no-trade filter

## 4. 시장/종목 선행 조건
1. `leading_gainer_rank <= 5`: 당일 scanner 상위권이어야 합니다.
2. `day_gain_pct >= 30~50%`: 충분히 시장 관심을 받아야 합니다.
3. `fresh_catalyst_score >= 2`: 신규 계약·실적·임상·규제·대형 파트너십은 높게, 단순 예측/분석가 의견/재탕 뉴스/뉴스 부재는 낮게 평가합니다.
4. `offering_or_shelf_risk = false`: SEC filing, 국내 전환사채/유상증자/대주주 매도 공시, 코인 unlock·재단 지갑 이동이 있으면 감점합니다.
5. 시장 환경은 강한 소형주 risk-on이 아니면 작은 base hit만 허용합니다.

## 5. 진입 준비 조건
- 첫 pop 이후 `initial_high`가 만들어지고, pullback 뒤 `reclaim_attempt`가 발생해야 합니다.
- `MACD_positive`나 단순 거래량 증가만으로는 부족하며, 호가가 얇아지는 것이 아니라 ask 물량을 흡수해야 합니다.
- 후보 A가 너무 heavy하면 scanner의 2차 후보 중 당일 뉴스가 있고 고점 재돌파 구조가 명확한 종목으로 이동합니다.
- `resistance_line`: 반복 고점 또는 ascending resistance를 연결해, 그 위에서 10초/1분 종가가 유지되는지 확인합니다.

## 6. 매수 조건 / 진입 트리거
1. `fresh_catalyst_score >= 2` and `no_offering_conflict`.
2. 직전 고점 또는 round number 근처에서 pullback 후 다시 거래량 증가.
3. `breakout_bar.close > prior_high` 또는 10초봉 기준 고점 돌파 후 즉시 bid가 따라붙음.
4. 예시: NTIP는 뉴스 후 pop→selloff→come back up→increasing volume에서 직전 고점 돌파 진입, $2.75 부근까지 squeeze.
5. 목표는 전체 추세 보유가 아니라 `first squeeze leg` 수익 확보입니다.

## 7. 진입 금지 조건
- `no_news_flag = true`: 당일 catalyst가 없는 급등. 영상의 ELPW는 가장 obvious였지만 뉴스 부재가 핵심 감점 요인입니다.
- `country_or_sector_trust_penalty`: 반복적으로 pump/offer 패턴이 강한 소형 해외 기업군은 보수적으로 처리합니다.
- `false_breakout_count >= 2`: $4 돌파 실패, $4.19 rejection처럼 같은 가격대에서 반복 실패.
- `ask_stack_thick = true`: 매도 호가가 두껍고 체결이 위로 이동하지 않음.
- `heavy_selling_volume_profile = true`: 상승 거래량보다 하락 거래량이 크고 pop 직후 전부 반납.
- 금요일 후반, 주말 전 bad-news/offer 우려가 큰 시간대.

## 8. 손절 조건
- 진입 pivot 재하회 즉시 축소/청산.
- breakout 후 1~2개 10초봉 또는 1개 1분봉 안에 follow-through가 없으면 시간 손절.
- `double_top_fail`: 고점 돌파 시도 후 윗꼬리와 함께 종가가 이전 고점 아래로 닫히면 손절.
- 뉴스 품질이 낮은 종목은 stop을 넓히지 않고 starter size만 사용합니다.

## 9. 익절 조건 / 트레일링 조건
- 1차: 다음 round number 또는 직전 intraday high에서 50~100% 청산.
- 2차: squeeze가 이어져도 topping tail 또는 bid pull 발생 시 잔여 청산.
- 장중 전체 추세 보유보다 `base hit` 우선. 영상 사례도 $2,306 수익 후 주간 마감 리스크를 낮췄습니다.

## 10. 필터 조건
- 시간대: 미국 장전 7:00~9:30. 금요일·월말에는 뉴스 품질 기준 상향.
- 거래량: `breakout_volume_ratio >= 1.5`이되, sell-volume dominance면 제외.
- 변동성: spread가 1분 ATR의 20% 이상이면 제외.
- 시장 방향: 소형주 risk-on, 전일 유사 뉴스주 follow-through 확인.
- 종목 선정: leading gainer, fresh news, clean level, thin but not illiquid book.
- 뉴스/테마: 단순 전망/분석가 buy rating은 SEC·공시 충돌 여부를 반드시 확인.

## 11. 실패 패턴과 회피 규칙
- 뉴스 없는 scanner 급등: 유동성만 붙은 pop은 double top과 round trip 확률이 높습니다.
- buy rating + placement agent 충돌: 분석가/주관사 이해상충은 매도 물량 유입 가능성으로 처리합니다.
- obvious but heavy: 가장 많이 보는 종목이라도 pull-away가 없으면 더 이상 anticipation 금지.
- 반복 저가주 scanner 후보: 너무 싼 종목은 체결/수수료/호가 단위 문제로 제외.

## 12. 백테스트 가능성
- 등급: B+
- 정량화 가능 항목: news flag, news quality NLP score, filing risk, false breakout count, wick ratio, ask/bid imbalance, sell-volume dominance.
- 구현 난이도: 중간~높음. 뉴스 품질·공시 이해상충은 텍스트/공시 데이터가 필요합니다.
- 추가 정의 필요사항: `fresh_catalyst_score`, `offering_conflict_score`, `heavy_selling_volume_profile`, `ask_stack_thick`.

## 13. 기계화 규칙 초안
```pseudo
for symbol in top_gainers:
    if day_gain_pct(symbol) < 30: continue
    if not fresh_news(symbol): continue
    if news_quality_score(symbol) < 2: continue
    if offering_or_shelf_conflict(symbol): continue
    if false_breakout_count(symbol, lookback=20min) >= 2: continue
    if sell_volume_dominance(symbol) > 0.6: continue

    pivot = recent_intraday_high(symbol)
    if price_reclaims_after_pullback(symbol) and break_with_volume(symbol, pivot, ratio=1.5):
        entry = stop_limit_above(pivot)
        stop = pivot - buffer_or_pullback_low
        target = next_round_number_or_hod(symbol)
        if rr(entry, stop, target) >= 1.5:
            buy_starter(symbol, entry, stop)
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: 거래대금 상위 급등주라도 공시가 단순 조회공시/풍문/CB·유증 리스크면 돌파 금지. 전고점 돌파 시 매도잔량이 재충전되는지 호가로 필터링합니다.
- 코인: 거래소 공지/상장/파트너십 뉴스가 재탕인지 확인하고, 재단 unlock·입금 지갑 이동이 있으면 제외합니다.

## 15. 리스크/반대 시나리오
- 뉴스 품질이 낮아도 유동성 장세에서는 계속 squeeze될 수 있습니다. 필터는 일부 대박을 놓치는 대가로 손실 회피를 목표로 합니다.
- 호가 데이터가 없으면 `ask_stack_thick` 구현이 어렵고, 1분봉만으로는 heavy seller를 늦게 인식할 수 있습니다.

## 16. 후속 검증 질문
1. 뉴스 없는 leading gainer의 돌파 성공률은 뉴스 있는 후보 대비 얼마나 낮은가?
2. `false_breakout_count >= 2` 이후 다음 돌파의 기대값은 음수인가?
3. 공시상 shelf/CB/유증 리스크가 있는 급등주의 intraday high breakout 성과는 어떤가?
