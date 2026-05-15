# 070. VWAP Reclaim 눌림목 — 약한 촉매·두꺼운 매물 No-Trade 필터

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: `Today Was An Exercise in Discipline...`
- URL: https://www.youtube.com/watch?v=1g4FOzXvlpw
- 수집일: 2026-05-15
- 문서화: 2026-05-16
- 원문 위치: `data/raw_transcripts/youtube/1g4FOzXvlpw.txt`
- 주요 근거 타임스탬프:
  - 00:49~03:18: `regained compliance`/reverse split은 실질 개선 없는 약한 catalyst로 평가
  - 03:20~04:05: 7시 첫 pop 후 즉시 sell-off, 이후 HOD 재접근 curl이 있었으나 진입 보류
  - 04:35~05:14: VWAP 위 reclaim은 있었지만 sub-par catalyst와 많은 seller가 동시에 존재
  - 05:31~06:57: 50c spike, VWAP 위 micro pullback에도 double top/stacked level2 우려로 회피
  - 07:38~09:00: 좁은 range에서 큰 size로 10~15c만 노리는 충동은 hidden seller에 20c 손실 위험
  - 10:33~10:58: D+1 첫 daily candle new high는 2차 catalyst 없으면 실패 가능성 높음

## 2. 전략 분류
- 눌림목매매 / 보조 no-trade 필터
- 전략 유형: 매수 전략의 진입 금지 규칙

## 3. 전략 요약
- VWAP reclaim과 micro pullback-curl이 보여도, 뉴스 품질이 낮고 호가가 두꺼우며 상단에 double top/hidden seller가 예상되면 눌림목 진입을 포기하는 방어형 필터입니다.
- 자산군: 미국 소형주 원형, 국내 reverse split/관리종목 해제성 공시주, 코인 단순 기술 반등/상폐 리스크 해소성 뉴스
- 시간프레임: 장전 7:00~10:00 ET, 10초~1분 진입 판단
- 전략 유형: 매수 금지 필터, 반자동 알림 차단 규칙

## 4. 시장/종목 선행 조건
1. 종목이 scanner에 포착되고 intraday로 30~70% 이상 상승합니다.
2. 첫 pop 이후 sell-off가 발생해 VWAP 아래 또는 직전 base까지 밀립니다.
3. 이후 VWAP reclaim, HOD 접근, micro pullback 같은 표면상 눌림목 트리거가 나옵니다.
4. 그러나 catalyst가 실질 매출/계약/승인/강한 테마가 아니라 `regained compliance`, reverse split, 단순 요건 충족 등 방어적 뉴스입니다.
5. 같은 시간대 거래대금이 penny stock 또는 다른 leader로 분산되어 있습니다.

## 5. 진입 준비 조건
- 정상적인 눌림목으로 인정하려면 아래 최소 조건을 충족해야 합니다.
  1. `news_quality_score >= 2`: 신규 계약, FDA/임상, AI/방산/원전 등 강한 테마 또는 숫자가 있는 공시.
  2. 첫 pop 후 sell-off가 있더라도 VWAP 위에서 두 번째 base를 형성.
  3. pullback 저점이 상승하고, 각 반등봉의 거래량이 증가.
  4. 호가/체결에서 반복적인 large ask refill이 없어야 함.
- 위 조건 중 2개 이상이 결여되면 눌림목 후보가 아니라 `trap curl`로 분류합니다.

## 6. 매수 조건 / 진입 트리거
- 이 문서의 핵심은 매수 신호가 아니라 “매수하지 않기”입니다. 단, 허용 가능한 예외 트리거는 다음과 같습니다.
  1. VWAP reclaim 이후 2개 이상의 1분봉 종가가 VWAP 위에서 유지.
  2. HOD까지 최소 1.8R 이상의 공간이 있고, HOD 돌파 후 다음 daily level까지 1.5R 이상.
  3. ask stack이 얇아지고, 체결강도/시장가 매수가 ask refill을 흡수.
  4. 2차 catalyst 또는 sector-wide sympathy가 확인.
- 예외가 없으면 HOD 재접근, VWAP 위 micro pullback, 30~50c 순간 spike만으로는 진입하지 않습니다.

## 7. 진입 금지 조건
- `news_quality_score <= 1`: reverse split, regained compliance, 단순 상장유지, 단순 PR성 공지.
- 첫 pop에서 30% 이상 상승 후 즉시 40~70% 되돌림.
- VWAP reclaim은 했지만 상단 HOD/double top 근처에서 거래량이 감소하거나 호가가 두꺼움.
- 좁은 range라서 수익 목표가 10~15c인데 예상 손절이 20c 이상.
- 9:15~10:00 ET에 아직 첫 거래가 없어 “break the ice” 충동으로 size를 키우는 상황.
- D+1 첫 daily candle new high 시도인데 2차 catalyst가 없고 전일 breakout day 대비 거래량이 낮음.

## 8. 손절 조건
- 예외적으로 진입했다면 stop은 VWAP 재이탈 또는 micro pullback low 이탈입니다.
- hidden seller 의심 구간에서는 시장가 진입 후 즉시 10초봉이 역방향으로 닫히면 손절.
- 손실 한도: range scalp에서 목표 10~15c라면 손절은 5~10c 이내여야 하며, 실제 호가상 20c 손실 가능성이 보이면 진입 금지.

## 9. 익절 조건 / 트레일링 조건
- 1차: HOD 또는 double top 직전에서 대부분 청산.
- 2차: HOD 돌파 후 volume expansion이 이어질 때만 10초 higher low 트레일.
- sub-par catalyst에서는 home-run 기대 금지. base hit가 원칙이며, 돌파 후 ask refill이 재등장하면 즉시 종료.

## 10. 필터 조건
- 시간대: 7:00~10:00 ET. 특히 9:15 이후 첫 진입은 회복 시간 부족으로 quality threshold 상향.
- 거래량: VWAP reclaim 봉이 직전 5개 1분봉 평균의 1.5배 이상이어야 하나, 매도 체결 동반 대량거래는 감점.
- 변동성: 1분봉 range가 목표 수익폭의 2배 이상이면 scalp R/R 불리.
- 시장 방향: hot market이면 일부 trap curl도 작동할 수 있으나, cold/cautious market에서는 뉴스 품질 우선.
- 종목 선정: 낮은 가격대라도 reverse split 직후 종목은 float/매도자 구조를 별도 감점.
- 뉴스/테마: 실질 catalyst 부재 시 VWAP reclaim 신호를 무효화.

## 11. 실패 패턴과 회피 규칙
- `trap curl`: 첫 sell-off 후 VWAP reclaim이 나오지만 HOD 직전마다 seller가 채워지는 패턴.
- `hidden seller top fill`: breakout 직전 큰 size를 사면 보이지 않던 매도자에게 체결되고 즉시 10~20c 밀림.
- `late ice-break trade`: 거래 없는 시간이 길어져 quality보다 P&L 시작 욕구가 우선되는 매매.
- `D+1 no second catalyst`: 전일 강세주의 첫 daily new high 시도이나 추가 뉴스가 없어 전일 거래량을 넘지 못하고 반락.

## 12. 백테스트 가능성
- 등급: A-
- 정량화 가능 항목: catalyst type, first_pop_retrace_pct, VWAP reclaim, HOD distance, bid/ask spread, 1분 거래량 상대비, D+1 volume ratio, time_of_first_trade.
- 구현 난이도: 중간. VWAP/캔들/거래량은 쉽지만 catalyst 품질과 hidden seller는 뉴스 분류·호가 데이터가 필요합니다.
- 추가 정의 필요사항: `news_quality_score`, `trap_curl`, `ask_refill_ratio`, `late_ice_break_window`, `second_catalyst_flag`.

## 13. 기계화 규칙 초안
```pseudo
for symbol in momentum_scanner:
    if has_vwap_reclaim(symbol) and has_micro_pullback(symbol):
        quality = news_quality_score(symbol)
        retrace = first_pop_retrace_pct(symbol)
        rr = reward_to_risk(entry=curl_high, stop=pullback_low, target=hod)
        ask_refill = ask_refill_ratio(symbol, near=hod)

        if quality <= 1: reject("subpar catalyst")
        if retrace > 0.55: reject("first pop failed too deeply")
        if rr < 1.8: reject("HOD too close / stop too wide")
        if ask_refill > threshold: reject("hidden seller / thick tape")
        if time_now >= '09:15' and no_trade_yet and account_in_rehab:
            require_quality_score(>=3)

        if not rejected and volume_expansion_confirmed:
            buy_starter(stop=pullback_low, target=hod_or_next_level)
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: 관리종목 해제, 거래재개, 액면병합/감자 후 재상장 같은 방어적 이벤트는 눌림목·VWAP 회복이 보여도 quality 점수를 낮게 둡니다.
- 코인: 상폐 리스크 해소, 지갑 점검 종료, 단순 거래소 공지성 재료는 강한 신규 수요보다 단기 숏커버/기술 반등일 수 있어 HOD 추격을 제한합니다.

## 15. 리스크/반대 시나리오
- 매우 뜨거운 시장에서는 약한 catalyst도 retail flow만으로 2~3차 squeeze가 날 수 있습니다.
- 호가 데이터가 없으면 hidden seller 판단이 늦어져 필터 실효성이 낮아집니다.
- no-trade 필터는 기회비용을 만들지만, 계좌 drawdown 회복 구간에서는 손실 방어 가치가 더 큽니다.

## 16. 후속 검증 질문
1. reverse split/regained compliance 뉴스주의 VWAP reclaim 후 HOD 돌파 성공률은 실질 계약/승인 뉴스 대비 얼마나 낮은가?
2. D+1 첫 daily candle new high가 2차 catalyst 없이 실패하는 비율은 얼마인가?
3. 9:15 이후 첫 진입의 기대값은 7:00~8:30 첫 진입 대비 낮은가?
