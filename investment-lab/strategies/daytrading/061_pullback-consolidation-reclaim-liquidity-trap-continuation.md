# 061. 주도 테마 강세장 눌림·재탈환 + 유동성 트랩 지속 매수

## 1. 출처
- 채널/작성자: Investors Underground / ChrisL, Sunday Scan
- 제목: Free Video Scan – Stocks to Watch for the Week of May 4, 2026
- URL: https://www.investorsunderground.com/free-scan-may-04-2026/
- 수집일: 2026-05-12
- 원문 위치: `data/raw_transcripts/articles/2026-05-12_iu_free_scan_may_04_2026.txt`

## 2. 전략 분류
- 눌림목매매 / 매수 전략
- 보조적으로 신고점 재접근·유동성 트랩 돌파 요소 포함

## 3. 전략 요약
- 한 문장: 강한 시장·강한 테마 안에서 이미 큰 상승을 보인 종목이 추격 구간을 지나 1~2일 이상 눌림·기반 형성을 보인 뒤 VWAP/직전 고점/전일 고가를 재탈환하면 재상승을 노리는 단타·스윙 겸용 매수 전략입니다.
- 자산군: 미국 소형주·테마주 원형, 국내 테마주/코인에도 변환 가능
- 시간프레임: 일봉 후보 선정 + 1분/5분 장중 트리거
- 전략 유형: 매수 전략, 눌림목 재상승, liquidity trap continuation

## 4. 시장/종목 선행 조건
1. 시장은 상승 모멘텀 우위여야 합니다. 원문은 Nasdaq·AI 주도 강세, “path of least resistance is still higher”를 강조합니다.
2. 테마가 명확해야 합니다. 예: AI, 메모리, 정부 지원, 규제, 실적·가이던스, 섹터 sympathy.
3. 종목은 다음 중 하나 이상을 충족합니다.
   - 당일/최근 3일 거래량이 20일 평균 대비 3배 이상.
   - 최근 1~5거래일 20~100% 이상 상승 후 과열 추격이 아니라 consolidation 대기.
   - 동종 테마 대장 또는 대장 추종 sympathy로 시장 관심이 확인됨.
4. “BE missed move but reentry on consolidation”, “ATER strong ramp and pullback, reclaim and move back toward highs”, “XTLB/HCAI/TLIH need consolidation before next leg”가 핵심 근거입니다.

## 5. 진입 준비 조건
- 눌림 인정 조건 초안:
  1. 직전 상승파동의 20~50% 되돌림 또는 VWAP/전일 고가/전고점/5분 20EMA 부근까지 조정.
  2. 눌림 중 거래량이 직전 상승봉 거래량 대비 40~70% 이하로 감소.
  3. 저점이 무질서하게 무너지지 않고 2개 이상 higher low 또는 평평한 박스 저점 형성.
  4. 과열 갭 직후 바로 추격하지 않고 최소 3~10개 5분봉의 기반 형성 확인.
- 유동성 트랩 준비 조건:
  - 직전 고점 부근에서 매수 추격자를 한 번 털거나 전일 고가/장중 박스 상단 아래에서 거래량이 줄어든 뒤 재돌파 대기.

## 6. 매수 조건 / 진입 트리거
1. Reclaim 트리거:
   - 가격이 VWAP 또는 5분 20EMA 아래에서 위로 회복하고, 회복봉 종가가 VWAP 위에 유지.
   - 동시에 1분/5분 거래량이 직전 20봉 평균의 1.5배 이상.
2. 고점 재접근 트리거:
   - 눌림 후 직전 minor high 또는 당일 박스 상단을 종가 기준 돌파.
   - 이상적으로 돌파봉 몸통이 전체 캔들 길이의 50% 이상이고 윗꼬리가 40% 미만.
3. Liquidity trap 트리거:
   - 전고점/전일 고가 위로 짧게 돌파 후 되밀림이 나오더라도, VWAP 또는 박스 중단을 이탈하지 않고 재돌파하면 2차 진입.
4. 분할 진입:
   - 1차: VWAP reclaim 종가.
   - 2차: 직전 눌림 고점/당일 고점 재돌파.

## 7. 진입 금지 조건
- 소스가 명시한 회피: negative catalyst가 momentum의 공기를 빼는 종목(POET 예시), fund selling·float 증가로 bounce가 어려운 종목(CAR 예시).
- 자동화 금지 조건 초안:
  1. 당일 고점 대비 60% 이상 왕복 하락한 full round trip.
  2. 5분봉 기준 VWAP reclaim이 2회 이상 실패.
  3. 눌림 중 음봉 거래량이 양봉 거래량보다 크고 OBV/누적 거래량 방향이 하락.
  4. 시장 ETF/지수 5분봉이 VWAP 아래에서 lower low를 갱신.
  5. 뉴스가 부정적이거나 유상증자·대주주 매도·오퍼링·float 증가가 확인된 경우.

## 8. 손절 조건
- 기본 손절: 진입 트리거가 발생한 reclaim 봉의 저가 또는 직전 눌림 저점 이탈.
- VWAP형 손절: 진입 후 2개 연속 1분봉 또는 1개 5분봉이 VWAP 아래 종가 마감.
- 위험 제한: 손절폭은 당일 ATR(5분 14) 0.8~1.2배 또는 종목 가격의 1.5~3.0% 중 작은 값으로 제한.

## 9. 익절 조건 / 트레일링 조건
- 1차 익절: 진입 리스크 1.5R~2R 또는 직전 고점/전일 고가 재도달.
- 2차 익절: 신고점/당일 고점 돌파 후 거래량이 유지되면 5분 20EMA 또는 VWAP 이탈까지 트레일링.
- 빠른 실패 청산: 고점 돌파 후 3개 1분봉 안에 돌파 가격 아래로 복귀하고 거래량이 감소하면 절반 이상 축소.

## 10. 필터 조건
- 시간대: 미국장은 09:35~11:30 ET 우선. 국내장은 09:05~10:30, 코인은 미국 정규장 개장 전후 또는 거래량 피크 구간.
- 거래량: 후보일 거래대금/거래량은 20일 평균 대비 3배 이상, 트리거봉은 최근 20개 1분/5분봉 평균의 1.5배 이상.
- 변동성: 직전 3개 5분봉 고저폭 평균이 초기 상승봉 고저폭의 30~70%로 축소될수록 선호.
- 시장 방향: Nasdaq/QQQ 또는 국내 KOSDAQ/테마 지수 5분 VWAP 위.
- 종목 선정: 테마 대장, 2등 sympathy, low float squeezer, earnings/upgrade/regulatory catalyst.

## 11. 실패 패턴과 회피 규칙
1. Failed reclaim: VWAP 회복 후 즉시 2개 봉 안에 재이탈.
2. No-volume bounce: 반등봉 거래량이 눌림 음봉 거래량보다 작음.
3. Late-stage prior base break: 이미 큰 상승 후 이전 기반들이 무너지기 시작하는 후기 국면.
4. Negative catalyst rug pull: 부정 뉴스가 나오며 테마 전체보다 훨씬 약하게 움직임.
5. Full reversal scenario: 뉴스 기반 종목은 upside continuation과 full reversal을 모두 계획해야 합니다.

## 12. 백테스트 가능성
- 등급: A-
- 정량화 가능 항목: 테마 강도, 갭/상승률, 거래량 배수, VWAP reclaim, consolidation 시간, 되돌림률, 고점 재돌파, 손절·익절 R.
- 구현 난이도: 중간. 뉴스·테마 분류는 별도 라벨이 필요하지만 가격·거래량만으로 1차 구현 가능.
- 추가 정의 필요사항:
  - liquidity trap의 수치 정의: 전고점 돌파 후 X분 내 -Y% 되밀림 후 재돌파.
  - 테마 대장/2등주 판별: 동일 테마 내 거래대금·등락률 순위.
  - negative catalyst 자동 제외: 공시/뉴스 키워드 사전.

## 13. 기계화 규칙 초안
```python
universe = stocks_with(
    rel_volume_20d >= 3,
    intraday_value_rank <= 50,
    theme_strength_rank <= 3,
    price_change_5d >= 0.20
)

for symbol in universe:
    impulse = prior_move_pct >= 0.20 and impulse_volume >= 3 * avg_volume_20d
    pullback = retrace_pct_of_impulse.between(0.20, 0.50) or touch(vwap, tolerance=0.003)
    consolidation = bars_since_high >= 3 and range_contract_ratio <= 0.70 and volume_contract_ratio <= 0.70
    reclaim = close > vwap and prev_close < vwap and volume > 1.5 * sma(volume, 20)
    high_rebreak = close > prior_minor_high and upper_wick_ratio < 0.40
    market_ok = index_close > index_vwap and theme_index_strength > 0
    avoid = negative_news or failed_vwap_reclaim_count >= 2 or full_round_trip

    if impulse and pullback and consolidation and market_ok and not avoid:
        if reclaim or high_rebreak:
            enter_long()
            stop = min(last_pullback_low, vwap - 0.2 * atr_5m)
            take_profit_1 = entry + 1.5 * (entry - stop)
            trail = max(vwap, ema20_5m)
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: 장초반 테마 대장주가 첫 급등 후 VWAP/시가/전고점 부근 눌림을 만들 때 적용합니다. VI 직후 바로 추격하지 않고 5분봉 3~6개 consolidation 후 reclaim을 요구합니다.
- 코인: 24시간 거래 특성상 “세션” 대신 거래량 피크 구간과 BTC/ETH 방향 필터를 사용합니다. 펀딩비 급등·미결제약정 과열 시 눌림이 liquidation cascade로 변할 수 있어 포지션 크기를 낮춥니다.

## 15. 리스크/반대 시나리오
- 강한 테마에서도 2등주·3등주는 대장주 약화 시 급격히 무너질 수 있습니다.
- 원문이 지적한 것처럼 과열 종목은 long continuation과 full reversal을 모두 계획해야 합니다.
- 소형주는 유동성·슬리피지·호가 공백으로 백테스트 체결가와 실거래 차이가 커질 수 있습니다.

## 16. 후속 검증 질문
1. 눌림 깊이를 직전 상승폭 대비 20~50%로 제한하면 VWAP 터치 단독보다 성과가 좋아지는가?
2. VWAP reclaim 후 직전 minor high 재돌파까지 기다리면 승률은 올라가지만 기대수익이 감소하는가?
3. 테마 대장주와 sympathy 종목을 분리하면 손절 빈도와 평균 R이 어떻게 달라지는가?
4. 국내 VI 종목에서 consolidation 최소 시간을 10분/20분/30분으로 달리할 때 최적값은 무엇인가?
