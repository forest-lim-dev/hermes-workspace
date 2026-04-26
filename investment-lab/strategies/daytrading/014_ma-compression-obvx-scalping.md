# 014. 200/60 Moving Average Compression + OBV-X Scalping

## 1. 출처
- 채널/작성자: 차트슈타인
- 제목: Day Trading of Madness (Chart Analysis Lecture by a Wall Street Legend Trader)
- URL: https://www.youtube.com/watch?v=Wly-gUZy_i0
- 수집일: 2026-04-27
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/Wly-gUZy_i0.txt`
- 주요 근거 구간: 06:23~10:57 200/60선 압축 및 OBV-X 롱 스캘핑, 11:08~14:54 숏/관망 기준과 압축·확장 해석

## 2. 전략 요약
- 한 문장: 200 이동평균의 대세 방향과 60 이동평균의 단기 수급 약화가 만나 두 선 간격이 압축된 뒤, OBV-X 교차 신호가 대세 방향과 일치할 때만 진입하는 초단타 스캘핑 전략입니다.
- 자산군: 코인, 국내주식, 해외주식
- 시간프레임: 초단타/스캘핑. 영상상 정확한 봉 주기는 명시되지 않았으나 1분~5분봉 후보.
- 전략 유형: 양방향 전략 / 추세 방향 필터 + 거래량 누적 타이밍

## 3. 매수 조건
1. 200 이동평균선이 상승 중입니다.
2. 60 이동평균선이 상승하다가 둔화/횡보하며 200선 쪽으로 접근해 두 선 간격이 압축됩니다.
3. 가격이 압축 공간 안에서 움직이다가 200선의 대세 방향인 위쪽으로 탈출하기 시작합니다.
4. OBV-X 지표에서 매수 신호가 발생합니다.
5. OBV-X가 반대 신호를 먼저 내면 무시하고, 200/60선 구조와 같은 방향의 다음 신호를 기다립니다.
6. 진입은 신호 캔들의 종가 또는 다음 캔들 시가로 가정합니다.

## 4. 매도/숏 조건
1. 200 이동평균선이 하락 중입니다.
2. 60 이동평균선이 반등하거나 상승하면서 200선 쪽으로 접근해 두 선 간격이 압축됩니다.
3. 60선이 다시 대세 방향인 하락으로 꺾이거나, 가격이 압축 공간 아래로 이탈합니다.
4. OBV-X 지표에서 숏/매도 신호가 발생합니다.
5. 반대 방향 OBV-X 신호는 무시하거나 기존 포지션 청산에만 사용합니다.

## 5. 손절 조건
- 롱: 직전 스윙 저점 아래.
- 숏: 직전 스윙 고점 위.
- 시간 손절: 진입 후 즉시 분출하지 않으면 틀린 타점으로 간주하고 빠르게 정리합니다. 기계화 시 2~3개 캔들 안에 0.5R 이상 유리한 움직임이 없으면 청산 후보.
- 방향 무효화: 60선이 200선과 반대 방향으로 확장하거나, 200선 기울기가 평탄/반전되면 청산합니다.

## 6. 익절 조건
- OBV-X에서 반대 교차 신호가 발생하면 종가 기준 익절합니다.
- 스캘핑 특성상 1R~2R 고정 익절과 반대 OBV 신호 청산을 비교 검증합니다.
- 추세 방향의 반복 신호는 재진입 가능하되, 각 진입은 독립 거래로 기록합니다.

## 7. 필터 조건
- 시간대: 국내주식은 09:05~10:30, 13:30~14:50처럼 거래가 몰리는 구간 우선. 점심 저유동성 구간은 제외 후보.
- 거래량: OBV 기반 전략이므로 거래량이 낮은 종목은 제외합니다. 당일 거래대금 상위 또는 분당 거래대금 기준 필요.
- 변동성: 압축 후 확장이 핵심이므로 ATR 백분위가 너무 낮거나 스프레드가 큰 종목은 제외합니다.
- 시장 방향: 롱은 지수/섹터 상승 또는 보합 이상, 숏은 지수/섹터 하락과 일치할 때 우선합니다.
- 종목 선정: 당일 강한 테마, 거래량 급증, 추세가 명확한 종목. 코인은 24시간 거래대금 상위 페어.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 높음
- 가능한 부분: 200/60 이동평균 기울기, 두 선 간격 축소/확장, 직전 저점 손절은 OHLCV로 계산 가능합니다.
- 어려운 부분: OBV-X 지표의 정확한 산식이 영상에서 완전 공개되지 않았습니다. “OBV length 30, MA length 30, fast/slow OBV 선 교차”로 추정 구현해야 합니다.

## 9. 기계화 규칙 초안
```text
ma_long = SMA(close, 200)
ma_short = SMA(close, 60)
long_slope = slope(ma_long, 10)
short_slope = slope(ma_short, 5)
gap = abs(ma_short - ma_long) / close
compression = gap < rolling_percentile(gap, 100, 25%) and gap has decreased for M bars

obv = OBV(close, volume)
obv_fast = EMA(obv, 30)   # 추정
obv_slow = SMA(obv, 30)   # 추정 또는 다른 MA 조합 검증 필요
obv_buy = obv_fast crosses above obv_slow
obv_sell = obv_fast crosses below obv_slow

long_bias = long_slope > 0 and ma_short >= ma_long or ma_short approaching ma_long from above
short_bias = long_slope < 0 and ma_short <= ma_long or ma_short approaching ma_long from below
long_entry = long_bias and compression_recent and price_breaks_up_from_compression and obv_buy
short_entry = short_bias and compression_recent and price_breaks_down_from_compression and obv_sell
long_stop = prior_swing_low
short_stop = prior_swing_high
long_exit = obv_sell or time_stop
short_exit = obv_buy or time_stop
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 1분봉/3분봉에서 거래대금 상위 종목만 대상으로 테스트합니다. 호가 스프레드와 체결강도 필터를 추가하면 스캘핑 체결 현실성을 높일 수 있습니다.
- 코인: 유동성이 높은 BTC/ETH 및 상위 알트 1분봉에 적용합니다. 수수료 부담이 크므로 최소 기대 R 또는 최소 변동폭 필터가 필요합니다.
- 국내주식은 숏이 제한적이므로 하락 구조는 인버스 ETF, 선물, 또는 롱 회피/청산 신호로 활용합니다.

## 11. 리스크/반대 시나리오
- 이동평균 압축은 사후적으로 보기 쉬우나 실시간으로는 압축 지속 시간이 길어질 수 있습니다.
- OBV-X 산식이 불명확해 동일한 신호 재현성이 낮을 수 있습니다.
- 초단타는 수수료, 세금, 슬리피지, 호가 공백이 기대값을 크게 훼손할 수 있습니다.
- 200선 대세 방향이 평탄한 횡보장에서는 반대 신호가 빈번해질 수 있습니다.

## 12. 후속 검증 질문
1. 200/60 이동평균 조합이 1분봉과 5분봉 모두에서 유효한가, 아니면 특정 타임프레임 전용인가?
2. OBV-X를 어떤 fast/slow 산식으로 구현해야 영상 신호에 가장 근접하는가?
3. “진입 후 즉시 분출”을 몇 캔들, 몇 R로 정의할 때 기대값이 가장 안정적인가?
4. 국내주식 거래세와 코인 수수료를 반영해도 스캘핑 빈도 전략이 유지되는가?
