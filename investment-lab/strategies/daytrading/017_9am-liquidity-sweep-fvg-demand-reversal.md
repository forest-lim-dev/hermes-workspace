# 017. 9시 유동성 사냥 + FVG/Demand Zone Reversal

## 1. 출처
- 채널/작성자: 슈퍼트레이더
- 제목: This short-term trading method will change your life in just one hour a day. (Even beginners who ...)
- URL: https://www.youtube.com/watch?v=pGg_JBGLbdI
- 수집일: 2026-04-28
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/pGg_JBGLbdI.txt`
- 주요 근거 구간: 01:47~06:43 장초 박스권·유동성 사냥, 07:55~09:12 1시간봉 추세와 9~10시 5분봉 필터, 09:47~11:57 박스 하단 sweep 후 FVG 눌림 진입, 12:02~13:39 Fibonacci 목표, 17:08~18:44 1분봉 수요존 응용

## 2. 전략 요약
- 한 문장: 장 시작 후 9~10시 사이에 상위 1시간봉 추세와 반대 방향으로 장초 박스권 유동성을 sweep한 뒤 빠르게 박스 안으로 복귀하면, 이후 생성된 FVG 또는 수요존 재테스트에서 반전 캔들을 확인해 추세 방향으로 진입합니다.
- 자산군: 국내주식, 코인, 해외주식 장초 종목
- 시간프레임: 상위 1시간봉 추세, 실행 1분~5분봉
- 전략 유형: 양방향 전략 / 오픈 구간 liquidity sweep reversal

## 3. 매수 조건
1. 상위 1시간봉에서 고점과 저점이 높아지는 상승 추세를 확인합니다.
2. 실행 차트는 1분봉 또는 5분봉을 사용합니다.
3. 국내주식 기준 09:00~10:00 사이만 신규 진입을 탐색합니다.
4. 장 시작 직후 가격이 위아래 박스권을 형성합니다.
5. 상승 추세 종목에서 가격이 박스권 하단을 일시적으로 하향 이탈해 손절/공포 매도 유동성을 sweep합니다.
6. 이탈 후 빠르게 박스권 내부로 복귀하거나 긴 밑꼬리 양봉이 발생합니다.
7. sweep 이후 강한 상승 캔들 3개 내외로 bullish FVG가 형성됩니다.
8. 가격이 FVG 영역 또는 sweep 직후 형성된 demand zone으로 되돌아옵니다.
9. 첫 양봉 반전 캔들 또는 긴 밑꼬리 양봉이 확인되면 진입합니다.

## 4. 매도/숏 조건
1. 상위 1시간봉에서 고점과 저점이 낮아지는 하락 추세를 확인합니다.
2. 09:00~10:00 사이 실행 차트에서 장초 박스권을 식별합니다.
3. 하락 추세 종목에서 가격이 박스권 상단을 일시적으로 상향 돌파해 추격매수/숏 손절 유동성을 sweep합니다.
4. 돌파 후 빠르게 박스권 내부로 복귀하거나 긴 윗꼬리 음봉이 발생합니다.
5. sweep 이후 강한 하락 캔들로 bearish FVG 또는 supply zone이 생성됩니다.
6. 가격이 해당 FVG/supply zone으로 반등하고 첫 음봉 반전 캔들이 나오면 숏 진입합니다.
7. 국내주식 현물에서는 숏 조건을 롱 회피/청산 신호 또는 인버스·선물 전략으로 분리합니다.

## 5. 손절 조건
- 롱: sweep 저점 또는 demand zone 하단 아래.
- 숏: sweep 고점 또는 supply zone 상단 위.
- 시간 손절: 진입 후 3~5개 실행 캔들 안에 박스 중심선 또는 0.5R 이상 진행이 없으면 청산 후보.
- 무효화: 롱은 박스 하단을 재이탈, 숏은 박스 상단을 재돌파하면 setup 실패로 간주합니다.

## 6. 익절 조건
- 1차 목표: 장초 박스권 반대편 또는 최근 고점/저점.
- 확장 목표: Fibonacci extension -2.5 영역을 후보로 사용합니다. 영상에서는 0.79, 0.62, -1, -2, -2.5, -4 설정을 언급합니다.
- 상위 1시간봉의 이전 고점/저점과 Fib 확장 목표가 겹치면 우선 익절 구간으로 봅니다.
- 최소 손익비는 2R 이상을 권장 후보로 둡니다.

## 7. 필터 조건
- 시간대: 국내주식 09:00~10:00만 신규 진입. 09:00 직후 1~3분의 과도한 스프레드는 제외 후보.
- 거래량: sweep 및 복귀 캔들의 거래량이 직전 평균 대비 증가해야 합니다.
- 변동성: 박스 폭이 너무 좁으면 수수료/호가 비용이 크고, 너무 넓으면 손절폭이 과대합니다. ATR 대비 박스폭 필터 필요.
- 시장 방향: 1시간봉 추세와 같은 방향만 거래합니다.
- 종목 선정: 장초 거래대금 급증, 전일/당일 뉴스, 갭 상승/하락, 테마 대장주 우선.

## 8. 백테스트 가능성
- 등급: 정량화 가능에 가까운 부분 정량화 가능
- 구현 난이도: 중간
- 가능한 부분: 시간 필터, 장초 박스, 박스 이탈·복귀, FVG, demand/supply zone, Fib 목표, 손익비는 OHLCV로 구현 가능합니다.
- 어려운 부분: “세력 유동성 사냥”이라는 해석은 정량 변수로 바꿔야 하며, 박스권 정의 기간과 sweep 허용 폭이 결과에 민감합니다.

## 9. 기계화 규칙 초안
```text
higher_tf = 60m
exec_tf = 1m or 5m
session_window = 09:00-10:00
trend_up = HH_HL(higher_tf, lookback=20)
trend_down = LH_LL(higher_tf, lookback=20)

opening_box = high/low range of first N bars after 09:00 or pre-sweep consolidation
long_sweep = low < opening_box.low - buffer and close > opening_box.low
short_sweep = high > opening_box.high + buffer and close < opening_box.high

bull_fvg_after_sweep = exists(high[t-2] < low[t]) within M bars after long_sweep
bear_fvg_after_sweep = exists(low[t-2] > high[t]) within M bars after short_sweep

long_retest = price_touches(bull_fvg or demand_zone) and bullish_reversal_candle
short_retest = price_touches(bear_fvg or supply_zone) and bearish_reversal_candle

long_entry = trend_up and in_session and long_sweep and bull_fvg_after_sweep and long_retest
short_entry = trend_down and in_session and short_sweep and bear_fvg_after_sweep and short_retest
long_stop = sweep_low - buffer
short_stop = sweep_high + buffer
target1 = opposite_side_of_opening_box
target2 = fib_extension(-2.5) if aligns_with_60m_level
require_reward_risk >= 2.0
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 09:00~10:00 장초 테마주에서 가장 직접적으로 적용 가능합니다. 단, VI/정적·동적 변동성완화장치와 호가 공백을 별도 기록해야 합니다.
- 코인: 한국식 9시 오픈이 없으므로 바이낸스 일봉 마감, 런던/뉴욕 오픈, 펀딩비 정산 전후 등 유동성 집중 시간으로 대체합니다.
- 해외주식: 프리마켓 high/low와 정규장 첫 5~15분 박스를 함께 비교해 ORB-fakeout 형태로 검증할 수 있습니다.

## 11. 리스크/반대 시나리오
- 강한 추세장에서는 sweep 없이 바로 돌파가 진행되어 대기만 하다 기회를 놓칠 수 있습니다.
- 진짜 하락 시작을 liquidity sweep으로 오인하면 박스 재이탈 손절이 발생합니다.
- 장초 스프레드 확대와 체결 지연이 백테스트보다 실전 손익을 악화시킬 수 있습니다.
- 국내주식은 09:00 직후 단일가 잔여 물량과 VI로 인해 stop 체결이 불리할 수 있습니다.

## 12. 후속 검증 질문
1. opening_box를 첫 5분, 10분, 또는 sweep 직전 횡보 박스 중 무엇으로 정의할 때 안정적인가?
2. sweep 깊이를 박스폭의 5%, 10%, ATR 0.2배 등 어떤 기준으로 둘 것인가?
3. FVG 재테스트 진입과 demand zone 긴 밑꼬리 즉시 진입 중 어떤 방식이 손익비가 우수한가?
4. 국내주식 09:00~09:05를 제외하면 승률은 낮아지지만 체결 안정성은 개선되는가?
