# 2026-04-25 단타매매 전략 리서치 배치 로그

## 처리 요약
- 처리 완료 컨텐츠: 5건
- 실패/보류: 1건
- 원문 transcript 저장: 5건
- 전략 후보 문서 생성: 5건
- 비단타/보조 아이디어 문서: 없음

## 처리 완료 컨텐츠

### 1) Trade with Pat — The Only Day Trading Strategy I’d Use If I Had to Start Over
- URL: https://www.youtube.com/watch?v=s9t8oXX7iVw
- 원문: `investment-lab/data/raw_transcripts/youtube/s9t8oXX7iVw.txt`
- 산출물: `investment-lab/strategies/daytrading/002_100ema-break-retest-supply-demand-scalp.md`
- 핵심 전략: 100 EMA 추세 필터 + 돌파된 지지/저항 retest + 5m/15m demand/supply 진입.
- 유형: 양방향 전략
- 백테스트 가능성: 부분 정량화 가능 / 구현 난이도 중간~높음

### 2) Trade with Pat — The ONLY Day Trading Strategy I'll use ALL 2026 (Backtested 1000 Times)
- URL: https://www.youtube.com/watch?v=E3McKlAp3qk
- 원문: `investment-lab/data/raw_transcripts/youtube/E3McKlAp3qk.txt`
- 산출물: `investment-lab/strategies/daytrading/003_displacement-orb-session-reversal.md`
- 핵심 전략: 15분 ORB 종가 돌파 + displacement + FVG/demand 되돌림을 Asia/London/NY reversal 필터로 선별.
- 유형: 양방향 전략
- 백테스트 가능성: 정량화 가능에 가까운 부분 재량 / 구현 난이도 중간

### 3) Trade with Pat — My BEST 5 Minute Scalping Strategy (330 Backtests)
- URL: https://www.youtube.com/watch?v=Bdgev1or-7M
- 원문: `investment-lab/data/raw_transcripts/youtube/Bdgev1or-7M.txt`
- 산출물: `investment-lab/strategies/daytrading/004_amd-session-reversal-5m-three-entry-scalp.md`
- 핵심 전략: AMD(Asia accumulation, London manipulation, NY distribution/reversal) 방향 필터 + S/R, supply/demand, ORB 3가지 5분봉 entry model.
- 유형: 양방향 전략
- 백테스트 가능성: 부분 정량화 가능 / 구현 난이도 중간~높음

### 4) Ross Cameron - Warrior Trading — Day Trading the Top 2 Leading % Gainers in the Market
- URL: https://www.youtube.com/watch?v=atHr4cLbtI0
- 원문: `investment-lab/data/raw_transcripts/youtube/atHr4cLbtI0.txt`
- 산출물: `investment-lab/strategies/daytrading/005_leading-gainer-vwap-reclaim-high-break.md`
- 핵심 전략: 상승률 상위·뉴스·저유통주 후보에서 VWAP reclaim, high break, dip bounce만 선별해 짧게 진입.
- 유형: 매수 전략
- 백테스트 가능성: 부분 정량화 가능 / 구현 난이도 높음

### 5) Ross Cameron - Warrior Trading — The Micro Pullback Trading Strategy (Small Account Challenge)
- URL: https://www.youtube.com/watch?v=6P25hNn_H00
- 원문: `investment-lab/data/raw_transcripts/youtube/6P25hNn_H00.txt`
- 산출물: `investment-lab/strategies/daytrading/006_micro-pullback-low-float-news-momentum.md`
- 핵심 전략: 뉴스·저유통주·상대거래량 급증 종목에서 10초~1분 micro pullback이 50% 이상 되돌리지 않고 재상승할 때 진입.
- 유형: 매수 전략
- 백테스트 가능성: 부분 정량화 가능 / 구현 난이도 높음

## 실패/보류
- Trade with Pat — The Only 1 Minute ORB Scalping Strategy That I TRUST
- 인벤토리 URL의 video id `yM-qSKJEylI`가 10자로 기록되어 YouTube 표준 11자 ID 파싱 실패.
- 조치: 실패 원인을 inventory 처리 이력에 기록. 다음 배치에서 원 URL 재확인 필요.

## 다음 배치 후보
1. Ross Cameron — +$2,306.80 Trading Leading Percentage Gainers: https://www.youtube.com/watch?v=hrZJKJ9NGbk
2. 슈퍼트레이더 — Opening Price Day Trading Method: https://www.youtube.com/watch?v=t8nmwXo5UlA
3. 코인독학 — 30-Minute Chart Day Trading Method (MACD + Price Action): https://www.youtube.com/watch?v=SKRg3D82Fjc
4. 코인독학 — Bollinger Band + MFI 단타: https://www.youtube.com/watch?v=WIuneu0pT8Q
5. AlphaTrends — Anchored VWAP Multiple Timeframes: https://alphatrends.net/archives/2023/03/how-to-chart-anchoredvwap-multiple-timeframes-03012023/

## 메모
- 오늘 처리한 Trade with Pat 3건은 서로 중복되는 ORB/AMD/FVG/demand 개념이 많으므로, 후속 작업에서 공통 컴포넌트와 독립 edge를 분리해야 합니다.
- Ross Cameron 전략은 데이터 요구사항이 다릅니다. 10초/1분봉, VWAP, 장전 스캐너, 뉴스/float/상대거래량 데이터가 필요합니다.
- 모든 문서는 리서치/교육 목적의 전략 후보이며 수익 보장 또는 매수·매도 지시가 아닙니다.
