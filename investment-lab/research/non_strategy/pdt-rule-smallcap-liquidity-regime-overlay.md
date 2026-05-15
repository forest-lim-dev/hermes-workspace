# PDT 규칙 완화와 소형주 단타 Regime Overlay

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: `Big PDT Rule Change and What it Means for You`
- URL: https://www.youtube.com/watch?v=cnoJ9DkWPVM
- 수집일: 2026-05-15
- 문서화: 2026-05-16
- 원문 위치: `data/raw_transcripts/youtube/cnoJ9DkWPVM.txt`

## 2. 분류
- 비단타/보조 아이디어: 시장 regime·유동성 필터
- 관련 전략: 눌림목매매, 신고점돌파매매 모두의 position sizing 및 거래 빈도 조절

## 3. 핵심 요약
- PDT 최소 계좌 요건이 $25,000에서 $2,000으로 낮아질 경우, 미국 소형주·저가주에 retail volume이 집중되어 intraday volatility와 scanner leader 기회가 증가할 수 있다는 regime 가설입니다.
- 이는 직접 매수 규칙은 아니지만, `market_hotness_score`, `retail_liquidity_regime`, `small_cap_volume_expansion` 같은 상위 필터로 쓸 수 있습니다.

## 4. 자동매매 변수 후보
- `regulatory_event_window`: 규칙 시행 전후 N일.
- `small_cap_total_volume_ratio`: 소형주 top 20 거래량 / 최근 20일 평균.
- `top_gainer_count_50pct`: 당일 +50% 이상 종목 수.
- `top_gainer_count_100pct`: 당일 +100% 이상 종목 수.
- `penny_volume_dominance`: $2 미만 종목 거래량이 top 10 거래량에서 차지하는 비율.
- `hot_market_daily_goal_multiplier`: hot regime에서는 허용 거래 수/size를 늘리고 cold regime에서는 축소.

## 5. 전략적 함의
- 눌림목매매: hot regime에서는 첫 micro pullback이 유일한 진입일 수 있어 대기 시간을 줄일 수 있습니다. 단, 첫 급등 후 완전 round trip이 반복되면 다시 dust-settle 필터를 강화해야 합니다.
- 신고점돌파매매: scanner obvious leader가 더 자주 생길 수 있어 HOD breakout, daily level breakout, round number breakout 후보가 증가합니다.
- 위험관리: 거래 빈도 증가가 과매매를 유발할 수 있으므로 계좌 손실 한도와 첫 손실 후 size 축소 규칙을 동시에 강화해야 합니다.

## 6. 백테스트 가능성
- 등급: B+
- 이유: 실제 PDT 시행 전후 이벤트 연구는 가능하지만, 제도 시행 효과와 동시 거시·계절·뉴스 요인을 분리해야 합니다.
- 우선 검증: 시행 전후 30/60/90일의 소형주 top gainer count, 거래대금, HOD breakout follow-through, VWAP pullback 성공률 비교.

## 7. 리스크/반대 시나리오
- 규칙 시행이 지연되거나 broker별 적용이 달라 효과가 분산될 수 있습니다.
- 유동성 증가는 기회뿐 아니라 fake breakout, halt, pump-and-dump도 증가시킬 수 있습니다.
- 미국 제도 변화는 국내주식/코인에 직접 적용되지는 않으며, 국내에서는 별도 수급 이벤트로 대체해야 합니다.
