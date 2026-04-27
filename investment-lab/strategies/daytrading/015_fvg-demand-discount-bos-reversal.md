# 015. Fair Value Gap 기반 Demand/Supply Discount Reversal

## 1. 출처
- 채널/작성자: Trade with Pat
- 제목: Fair Value Gap Trading Strategy (Tested 1001+ Times)
- URL: https://www.youtube.com/watch?v=yFPrP6nJRYQ
- 수집일: 2026-04-28
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/yFPrP6nJRYQ.txt`
- 주요 근거 구간: 00:38~02:36 FVG 정의와 단독 진입 금지, 02:45~05:04 demand zone/50% discount/손절·목표, 07:37~10:19 구조 전환 및 engulfing 확인, 10:38~11:48 부분익절·트레일링 청산

## 2. 전략 요약
- 한 문장: 강한 임펄스가 만든 FVG는 “진입 신호”가 아니라 되돌림 가능성을 알려주는 단서로만 쓰고, 실제 진입은 임펄스 시작점의 수요/공급 구간이 50% 할인/프리미엄 영역에서 재테스트될 때 구조 전환과 모멘텀 캔들을 확인해 실행합니다.
- 자산군: 코인, 해외주식, 국내주식 대형/테마주
- 시간프레임: 1분~15분 단타, 상위 구조 확인은 15분~1시간 후보
- 전략 유형: 양방향 전략 / FVG + 수요·공급존 + 구조 전환

## 3. 매수 조건
1. 최근 가격 범위의 상단/하단을 먼저 표시해 현재 거래 범위를 정의합니다.
2. 상위 구조가 저점 상승·고점 상승 또는 최소한 매수 방향으로 전환 가능한 위치여야 합니다.
3. 강한 상승 임펄스가 발생하고 3캔들 기준 bullish FVG가 생성됩니다. 예: 1번 캔들 고가 < 3번 캔들 저가.
4. 임펄스 직전 마지막 하락 캔들 또는 횡보 박스를 demand zone으로 표시합니다.
5. Fibonacci를 임펄스 저점→고점에 적용했을 때 가격이 50% 아래, 즉 discount 영역까지 되돌립니다.
6. 되돌림이 FVG 중간이 아니라 demand zone 근처까지 깊게 들어옵니다.
7. 단기 하락 구조의 break of structure가 먼저 나오거나, demand zone에서 bullish engulfing/강한 양봉이 확인됩니다.
8. 진입은 확인 캔들 종가 또는 demand zone 상단 재돌파 시점으로 가정합니다.

## 4. 매도/숏 조건
1. 최근 가격 범위 상단에서 하락 임펄스와 bearish FVG가 발생합니다. 예: 1번 캔들 저가 > 3번 캔들 고가.
2. 임펄스 직전 마지막 상승 캔들 또는 횡보 박스를 supply zone으로 표시합니다.
3. Fibonacci를 임펄스 고점→저점에 적용했을 때 가격이 50% 위, 즉 premium 영역까지 반등합니다.
4. 가격이 supply zone으로 되돌아오고 단기 상승 구조가 하락으로 break of structure 되거나 bearish engulfing/강한 음봉이 출현합니다.
5. 진입은 확인 캔들 종가 또는 supply zone 하단 재이탈 시점으로 가정합니다.

## 5. 손절 조건
- 롱: demand zone 하단 또는 되돌림 중 형성된 주요 wick 저점 아래.
- 숏: supply zone 상단 또는 되돌림 중 형성된 주요 wick 고점 위.
- 구조 무효화: 롱은 demand zone을 종가 기준 하향 이탈하면 무효, 숏은 supply zone을 상향 돌파하면 무효.
- 시간 손절: 진입 후 N개 캔들 안에 최소 0.5R 진행이 없으면 약한 반응으로 간주해 청산 후보.

## 6. 익절 조건
- 1차 목표: 최근 반응 가격대 또는 임펄스 고점/저점.
- 2차 목표: 이전 거래 범위 상단/하단 또는 상위 저항·지지.
- 강한 돌파가 나오면 일부 익절 후 직전 swing low/high 이탈을 trailing stop으로 사용합니다.
- 최소 손익비는 2R 이상 후보. 영상 예시에서는 약 2.15R 이상을 언급합니다.

## 7. 필터 조건
- 시간대: 국내주식은 09:05~10:30과 14:00 이후 변동성 구간 우선. 코인은 런던/뉴욕 오픈 또는 거래량 급증 구간 후보.
- 거래량: 임펄스 캔들의 거래량이 직전 20캔 평균 대비 높아야 합니다.
- 변동성: FVG 폭이 너무 작으면 수수료/스프레드에 묻히므로 ATR 대비 최소 폭 기준 필요.
- 시장 방향: 상위 구조와 같은 방향 거래를 우선합니다. 상위 상승 구조에서는 demand 롱만, 하락 구조에서는 supply 숏만 우선 검증합니다.
- 종목 선정: 당일 거래대금 상위, 뉴스/테마/갭으로 임펄스가 생긴 종목 또는 코인 거래대금 상위 페어.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간~높음
- 가능한 부분: 3캔들 FVG, 임펄스 크기, 50% retracement, demand/supply 후보 캔들, engulfing, 손익비는 OHLCV로 정의 가능합니다.
- 어려운 부분: “의미 있는 demand/supply zone”, “break of structure”의 swing pivot 민감도에 따라 결과가 크게 달라집니다.

## 9. 기계화 규칙 초안
```text
bull_fvg = high[t-2] < low[t]
bear_fvg = low[t-2] > high[t]
impulse_up = close[t-1] > open[t-1] and body[t-1] > 1.5 * avg_body(20) and volume[t-1] > 1.5 * avg_volume(20)
impulse_down = close[t-1] < open[t-1] and body[t-1] > 1.5 * avg_body(20)

demand_zone = range(last_bearish_candle_before_impulse_up)
supply_zone = range(last_bullish_candle_before_impulse_down)

discount = close <= impulse_low + 0.5 * (impulse_high - impulse_low)
premium = close >= impulse_low + 0.5 * (impulse_high - impulse_low)

bull_confirm = bullish_engulfing or close > prior_minor_swing_high
bear_confirm = bearish_engulfing or close < prior_minor_swing_low

long_entry = bull_fvg_recent and impulse_up and price_touches(demand_zone) and discount and bull_confirm
short_entry = bear_fvg_recent and impulse_down and price_touches(supply_zone) and premium and bear_confirm
long_stop = demand_zone.low - buffer
short_stop = supply_zone.high + buffer
long_target1 = prior_reaction_high
short_target1 = prior_reaction_low
require_reward_risk >= 2.0
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 장 초반 강한 테마주가 1차 급등 후 깊은 눌림을 줄 때, FVG를 추격 진입 근거가 아니라 demand zone 재테스트 대기 신호로 사용합니다.
- 코인: 24시간 거래라 세션 범위가 모호하므로 최근 4~8시간 high/low range와 펀딩·미결제약정 급증을 보조 필터로 추가합니다.
- 국내주식 숏 제약 때문에 bearish setup은 인버스 ETF, 선물, 또는 롱 회피/청산 신호로 우선 활용합니다.

## 11. 리스크/반대 시나리오
- 강한 추세장에서는 demand/supply까지 깊은 되돌림이 오지 않아 기회를 놓칠 수 있습니다.
- 횡보장에서는 FVG가 빈번히 생기지만 실제 방향성이 부족해 zone 돌파 손절이 반복될 수 있습니다.
- FVG와 수요/공급존은 사후적으로 명확해 보이는 경향이 있어 pivot 정의를 엄격히 해야 합니다.
- 뉴스 급등주는 호가 공백 때문에 손절 위치가 실제 체결가와 크게 다를 수 있습니다.

## 12. 후속 검증 질문
1. FVG 폭을 ATR 대비 몇 % 이상으로 제한할 때 노이즈를 줄일 수 있는가?
2. demand/supply zone을 “직전 반대색 1캔들”로 할지 “임펄스 전 횡보 박스”로 할지 어떤 정의가 더 안정적인가?
3. BOS 확인 없이 zone 터치만 진입하는 방식과 engulfing/BOS 확인 후 진입하는 방식의 기대값 차이는?
4. 국내주식 장 초반 테마주에서 2R 이상 손익비가 실제 호가·거래세 반영 후 유지되는가?
