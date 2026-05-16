# 074. ATR/SuperTrend 변동성 확장 돌파·추세전환 전략

## 1. 출처
- 채널/작성자: 차트슈타인
- 제목: `A super easy day trading method that only you do not know about`
- URL: https://www.youtube.com/watch?v=uVNzYNiPrUE
- 수집일/문서화: 2026-05-17
- 원문 위치: `data/raw_transcripts/youtube/uVNzYNiPrUE.txt`
- 주요 근거 타임스탬프: 01:32~02:49 ATR 낮은 횡보 회피 후 ATR 증가 방향 진입, 03:33~04:25 ATR 2배 손절, 05:31~06:18 SuperTrend는 ATR 배수 지지/저항선·계수 2 선호, 06:28~07:26 빨간 저항선 돌파 양봉 매수·1:2 목표, 09:44~10:20 200/202MA 방향과 신호 강도로 가짜 반등 구분, 10:35~11:46 선 색 역전/ATR 기반 목표가로 익절.

## 2. 전략 분류
- 혼합: 신고점돌파매매 / 눌림목매매 보조 / 양방향 전략
- 전략 유형: 매수·매도 양방향, 변동성 필터, 손절/트레일링 모듈

## 3. 전략 요약
- ATR이 낮아진 횡보 구간을 피하다가 ATR 기반 SuperTrend 저항선을 강한 양봉으로 돌파하면 진입하고, ATR 2배 또는 SuperTrend 선을 손절·트레일링 기준으로 삼는 변동성 확장 돌파 전략입니다.
- 자산군: 코인/선물/국내주식 모두 가능
- 시간프레임: 1분~1시간. 단타 자동매매는 3분/5분 권장

## 4. 시장/종목 선행 조건
1. 직전 구간에서 ATR이 하락하며 변동성 압축이 발생합니다.
2. 가격이 횡보 박스 또는 SuperTrend 저항선 근처에서 대기합니다.
3. 상위 추세 필터: 200/202 이동평균선이 상승이면 롱 우선, 하락이면 숏 우선.
4. 거래량은 돌파봉에서 직전 평균 대비 증가해야 합니다. 원문은 ATR 중심이나 자동매매에는 거래량 필터가 필요합니다.

## 5. 진입 준비 조건
- ATR percentile이 최근 N봉 기준 하위권(예: 20~40%)에서 벗어나는지 확인합니다.
- SuperTrend 설정: ATR period 10~14, multiplier 2를 기본 후보로 둡니다.
- 손절폭이 `2 * ATR`일 때 계좌 허용 손실과 목표 손익비 1:2가 가능한지 선검증합니다.

## 6. 매수 조건 / 진입 트리거
### 롱 트리거
1. 가격이 하락/횡보 후 SuperTrend 빨간 저항선 아래에 있습니다.
2. ATR이 최근 저점 대비 상승 전환합니다.
3. 강한 양봉이 SuperTrend 저항선 또는 박스 상단을 종가로 돌파합니다.
4. 종가 진입 또는 다음 봉 눌림에서 진입합니다.
5. stop은 SuperTrend 선 또는 진입가 - 2ATR 중 더 보수적인 값.
6. 1차 목표는 2R, 이후 SuperTrend 초록선 유지 시 트레일링.

### 숏 트리거
1. 200/202MA가 하락하고 가격이 SuperTrend 초록 지지선 위에서 약한 반등을 보입니다.
2. 하락 신호 강도 또는 음봉 돌파가 상승 신호보다 큽니다.
3. SuperTrend 지지선 하향 돌파 종가에서 숏 진입.
4. stop은 SuperTrend 선 또는 진입가 + 2ATR.

## 7. 진입 금지 조건
- ATR이 낮은 상태가 아니라 이미 급등 후 ATR이 과도하게 치솟은 과열 말미.
- 200/202MA 하락 중 약한 상승 신호만 보고 롱 진입.
- 손절폭 2ATR이 목표가/HOD까지 거리보다 커서 1:2 손익비가 나오지 않습니다.
- 횡보장에서 SuperTrend 색이 잦게 바뀌는 whipsaw 구간.
- 거래량 없는 돌파, 윗꼬리 긴 돌파봉.

## 8. 손절 조건
- 기본: SuperTrend 선 색 반전 또는 선 이탈 종가.
- 고정 변동성: 진입가 기준 2ATR 역방향 도달.
- 구조 손절: 돌파한 박스 상단/저항선 재이탈.
- 시간 손절: 진입 후 3~5봉 이내 ATR/거래량 확장이 이어지지 않으면 축소.

## 9. 익절 조건 / 트레일링 조건
- 1차: +1R 또는 +2R에서 분할 익절. 원문 예시는 1:2 목표.
- 2차: SuperTrend 선 유지 시 추세 추종.
- 최종: 선 색 반전, 강한 반대 신호, 또는 ATR 급등 후 장대 윗꼬리/아랫꼬리.
- 레버리지 선물은 목표가 도달마다 분할익절하여 멘탈/청산 리스크를 낮춥니다.

## 10. 필터 조건
- 시간대: 국내주식은 9:30 이후, 코인은 주요 세션 개시 후 거래량 증가 구간.
- 거래량: 돌파봉 거래량이 직전 20봉 평균 대비 1.3배 이상.
- 변동성: ATR percentile이 하위권에서 중상위권으로 상승 전환. 이미 상위 90% 이상이면 추격 제한.
- 시장 방향: 200/202MA 방향과 같은 쪽 신호만 우선 테스트.
- 종목 선정: 당일 거래대금 상위, 스프레드 좁고 2ATR 손절이 허용 가능한 종목.

## 11. 실패 패턴과 회피 규칙
- SuperTrend 지연: 빠른 장에서 진입/청산 신호가 늦어 본절 청산 → 1차 고정 R 익절 병행.
- whipsaw: ATR 낮은 횡보가 계속되며 색 반전 반복 → ADX/ATR 확장 필터 추가.
- 과열 뒤늦은 돌파: ATR 급등 후 마지막 양봉에 진입 → ATR percentile 상단 진입 금지.

## 12. 백테스트 가능성
- 등급: A
- 정량화 가능: ATR, SuperTrend, 200MA 방향, 거래량 증가율, 손익비, 선 색 반전.
- 구현 난이도: 낮음. 대부분 OHLCV만으로 가능.
- 추가 정의: ATR period/multiplier, ATR percentile lookback, 돌파봉 몸통 비율, 거래량 임계값.

## 13. 기계화 규칙 초안
```pseudo
atr = ATR(14)
st = SuperTrend(period=10 or 14, multiplier=2)
atr_pct = percentile_rank(atr, lookback=100)
trend_long = close > SMA(200) and SMA(200).slope > 0
trend_short = close < SMA(200) and SMA(200).slope < 0
vol_ok = volume > 1.3 * SMA(volume,20)

if trend_long and atr_pct crosses above 40 and close crosses above st.resistance and bullish_body and vol_ok:
  buy(stop=min(st.line, close - 2*atr), target=close + 2*(close-stop))
if trend_short and atr_pct crosses above 40 and close crosses below st.support and bearish_body and vol_ok:
  short(stop=max(st.line, close + 2*atr), target=close - 2*(stop-close))
if position and st.color_reversal:
  exit()
```

## 14. 국내주식/코인 적용 아이디어
- 국내주식: 상한가/VI 때문에 ATR이 급변할 수 있으므로 5분봉 기준, VI 직후 3봉은 신규 진입 금지.
- 코인: 24시간 연속 거래와 숏 가능성이 있어 양방향 적용이 쉽습니다. 다만 펀딩비·청산맵·급격한 spread 확대를 추가 필터로 둡니다.

## 15. 리스크/반대 시나리오
- SuperTrend 계수 2는 빠르지만 노이즈가 많을 수 있습니다. 코인 저유동성 알트에서는 계수 2.5~3 비교가 필요합니다.
- ATR 손절은 변동성 큰 종목에서 손절폭이 커져 포지션 크기를 자동으로 줄이지 않으면 계좌 리스크가 커집니다.

## 16. 후속 검증 질문
- 3분/5분봉에서 ATR multiplier 2 vs 3의 손익비·회전율 차이는?
- ATR percentile 하위권에서 상향 돌파하는 조건이 단순 SuperTrend 돌파보다 실패율을 얼마나 낮추는가?
- 국내주식 9:30 이후 필터를 결합하면 장초반 whipsaw가 감소하는가?
