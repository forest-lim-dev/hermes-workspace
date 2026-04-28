# 020. Liquidity Sweep + ORB Displacement + Demand/Supply Reversal

## 1. 출처
- 채널/작성자: Trade with Pat
- 제목: The ONLY Liquidity Trading Strategy WORTH Learning (3 Steps)
- URL: https://www.youtube.com/watch?v=sclIAK3x2dw
- 수집일: 2026-04-29
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/sclIAK3x2dw.txt`

## 2. 전략 요약
- 한 문장: 상위 시간봉의 명확한 지지/저항 뒤 stop-loss 유동성이 sweep된 뒤, 5분봉 ORB 방향 돌파와 demand/supply 재테스트·engulfing 확인으로 반전 방향에 진입하는 전략입니다.
- 자산군: 원 영상은 Gold/FX 예시, 코인·국내주식 단타에 적용 가능
- 시간프레임: 1시간봉 sweep 확인 + 5분봉 실행, 09:30~09:45 첫 15분 range 예시
- 전략 유형: 양방향 전략 / liquidity sweep reversal + momentum confirmation

## 3. 매수 조건
1. 1시간봉에서 여러 번 존중된 명확한 지지선이 존재합니다.
2. 가격이 지지선 아래로 내려가 stop-loss 유동성을 가져가지만, 충격적 종가 이탈이 아니라 wick/sweep 후 다시 회복합니다.
3. sweep 이후 5분봉으로 전환해 세션 첫 15분 range의 고가·저가를 표시합니다.
4. 5분봉에서 range 상단을 강하게 종가 돌파하며 displacement가 발생합니다.
5. 장대 상승 이전의 마지막 음봉 또는 FVG를 demand zone으로 표시합니다.
6. 가격이 demand zone으로 되돌아온 뒤 bullish engulfing 등 반전 확인 캔들이 종가로 완성되면 롱 진입합니다.

## 4. 매도/숏 조건
1. 1시간봉에서 여러 번 존중된 명확한 저항선이 존재합니다.
2. 가격이 저항선 위로 올라가 숏 포지션의 stop 유동성을 sweep하지만, 강한 종가 돌파로 이어지지 않습니다.
3. sweep 이후 5분봉에서 세션 첫 15분 range를 설정합니다.
4. range 하단을 강하게 종가 이탈하며 displacement가 발생합니다.
5. 장대 하락 이전의 마지막 양봉 또는 FVG를 supply zone으로 표시합니다.
6. 가격이 supply zone으로 되돌아온 뒤 bearish engulfing 등 하락 확인 캔들이 종가로 완성되면 숏 진입합니다.

## 5. 손절 조건
- 매수: demand zone 하단 또는 최근 swing low 아래 buffer.
- 매도: supply zone 상단 또는 최근 swing high 위 buffer.
- sweep level 재이탈이 발생하거나, 확인 engulfing 캔들의 반대쪽을 종가로 돌파하면 무효화로 간주합니다.

## 6. 익절 조건
- 원 영상은 반대편의 강한 supply/demand, 최근 swing high/low를 take-profit 후보로 사용합니다.
- 기계화 초안:
  - 1차: 1R 또는 최근 구조 고점/저점
  - 2차: 상위 시간봉 supply/demand 또는 2R 이상
  - 중간 저항/지지에서 20~30% 부분익절 후 손절을 본전으로 이동하는 규칙을 검증합니다.

## 7. 필터 조건
- 시간대: 영상 예시는 09:30~09:45 첫 15분 range. 국내주식은 09:00~09:15, 코인은 세션별 첫 15분을 테스트합니다.
- 거래량: sweep 이후 ORB 돌파 캔들의 거래량이 직전 N봉 평균 대비 높을수록 신뢰도가 높습니다.
- 변동성: sweep이 ATR 대비 과도하게 크면 추격/반전 리스크가 커집니다.
- 시장 방향: 상위 시간봉 sweep 방향과 실행 시간봉 displacement 방향이 일치해야 합니다.
- 종목 선정: 명확한 수평 지지/저항을 가진 유동성 상위 종목, 갭/뉴스로 유동성이 쏠린 종목이 우선 후보입니다.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간~높음
- 이유: sweep, ORB, engulfing은 정량화 가능하나 “명확한 지지/저항”, demand/supply zone의 자동 식별 규칙이 성과에 민감합니다.

## 9. 기계화 규칙 초안
```text
HTF = 1h
obvious_support = level touched >= 2 times within tolerance 0.2*ATR(1h)
long_sweep = low < support - buffer and close > support
run_filter_fail = close < support - 0.5*ATR(1h) with body > 0.7*range  # run이면 제외

LTF = 5m after sweep
first_15m_range = first three 5m candles after session_open
long_momentum = close > ORH and body > 0.8*ATR(5m) and close near high
POI = last bearish candle before displacement or bullish FVG
entry = retest(POI) + bullish_engulfing_close
stop = min(POI_low, recent_swing_low) - buffer
target = next_HTF_supply or 2R

short rules are symmetric.
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 전일 고가/저가, 당일 시초 15분 range, 전일 종가 부근의 stop sweep을 결합합니다. 다만 VI와 시초가 갭으로 sweep 판정이 왜곡될 수 있어 체결 가능성 필터가 필요합니다.
- 코인: BTC/ETH 1시간봉의 아시아/런던/뉴욕 세션 직전 고저점 sweep 후 5분봉 displacement-retest 진입으로 테스트합니다.
- 알트코인은 거래대금 상위와 스프레드 제한을 둬야 wick 노이즈를 줄일 수 있습니다.

## 11. 리스크/반대 시나리오
- sweep이 아니라 진짜 liquidity run이면 반대매매가 큰 손실로 이어질 수 있습니다.
- 상위 시간봉 level이 너무 주관적이면 과최적화 위험이 큽니다.
- demand/supply 재테스트 없이 곧바로 추세가 진행되면 진입 기회를 놓칩니다.
- 급등주/저유동 코인은 wick가 많아 sweep 신호의 거짓 양성이 많을 수 있습니다.

## 12. 후속 검증 질문
1. 1시간봉 level touch 횟수와 허용오차는 얼마가 적절한가?
2. sweep 이후 몇 개 5분봉 안에 ORB displacement가 나와야 유효한가?
3. FVG와 마지막 반대색 캔들 zone 중 어떤 POI가 더 안정적인가?
4. 국내주식에서는 전일 고저점 sweep과 당일 15분 ORB 조합이 유효한가?
