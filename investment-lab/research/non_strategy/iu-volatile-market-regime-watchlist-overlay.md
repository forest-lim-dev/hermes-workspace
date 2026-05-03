# IU 블로그 메인 페이지 기반: 변동성 장세 단타 워치리스트 보조 필터

## 1. 출처
- 작성자/사이트: Investors Underground Blog
- 제목: Learn How to Day Trade Stocks - Free Blog Articles / 최근 글 목록
- URL: https://www.investorsunderground.com/blog/
- 수집일: 2026-05-04
- 원문 위치: `sources/articles/raw/2026-05-04_iu_blog.txt`

## 2. 아이디어 요약
- 최근 글 목록은 반도체/AI 리더십, 지수 V자 반등, 중동·유가·금리·FOMC·실적 등 매크로 헤드라인이 장중 변동성을 키우는 환경을 반복적으로 언급합니다.
- 단일 진입 전략보다는 “단타 전략 실행 전 시장 레짐/테마/헤드라인 필터”로 활용할 수 있습니다.

## 3. 전략 활용 가능 포인트
1. **레짐 분류**: risk-on momentum, volatile range-bound, bearish bias, headline-driven shock 등으로 일중 매매 모드를 분리.
2. **테마 리더십 확인**: AI/반도체처럼 당일 시장을 이끄는 테마가 있으면 해당 테마의 대장주·후발주만 우선 감시.
3. **이벤트 캘린더 필터**: FOMC, 주요 실적, 지정학 뉴스, 유가 급등 등 이벤트 전후에는 ORB/돌파 전략의 손절폭과 포지션 크기 축소.
4. **스캔 우선순위**: 주간 watchlist에서 반복 등장하는 섹터와 당일 gapper/relative volume 상위 종목을 교차.

## 4. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간
- 이유: VIX, 지수 20일 변동성, 섹터 상대강도, 이벤트 더미 변수, 갭상승/갭하락 수는 정량화 가능하지만 뉴스 톤 분류는 별도 라벨링 또는 NLP가 필요합니다.

## 5. 기계화 규칙 초안
```text
1) market_regime:
   - risk_on: SPY/QQQ > VWAP and 5d return > 0, leading sector relative strength > 0
   - bearish_bias: index below 20MA or first 30m low breakdown
   - headline_shock: VIX +10% day-over-day or oil/yield large move or major event day
2) strategy_switch:
   - risk_on: leader ORH breakout, pullback continuation 우선
   - bearish_bias: failed breakout, VWAP reject, weak follower short/avoidance 우선
   - headline_shock: position_size 50% 축소, first signal pass, confirmation 강화
3) watchlist_score = gap% + relative_volume + sector_RS + news_catalyst_dummy
```

## 6. 국내주식/코인 적용 아이디어
- 국내주식: KOSDAQ 지수, 테마 대장주, 거래대금 상위 테마를 기준으로 risk-on/risk-off를 분류합니다.
- 코인: BTC/ETH 방향, USDT 마켓 거래대금, 펀딩비, 미국장 시간대 이벤트를 결합해 알트 돌파 전략 실행 여부를 결정합니다.

## 7. 리스크/후속 질문
- 블로그 메인 목록만 기반으로 한 보조 아이디어라 개별 글 전문의 구체 매매 규칙은 추가 확인 필요합니다.
- 시장 레짐 필터가 너무 엄격하면 좋은 단타 기회를 놓칠 수 있습니다.
- 다음 배치에서 IU 개별 글(예: Hyper Scalping, Survive & Thrive in Volatile Markets) 본문 접근 가능 여부를 확인해 전략 문서화할 필요가 있습니다.
