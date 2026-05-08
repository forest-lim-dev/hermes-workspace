# 047. 볼린저밴드 + 거래량 CCI 스퀴즈 돌파 스캘프

## 1. 출처
- 채널/작성자: 차트슈타인
- 제목: The single trading method used to earn 10 billion won using Bollinger Bands
- URL: https://www.youtube.com/watch?v=Xfu-svNLAV8
- 수집일: 2026-05-08
- 원문 위치: `data/raw_transcripts/youtube/Xfu-svNLAV8.txt`

## 2. 전략 요약
- 한 문장: 볼린저밴드 20SMA 중심선으로 횡보/추세를 구분하고, 스퀴즈 후 거래량 가중 CCI가 0선 또는 ±100선을 강하게 돌파할 때 추세 방향으로 진입하는 양방향 단타 전략입니다.
- 자산군: 주식, 코인, 선물.
- 시간프레임: 5분~30분봉 단타, 1시간봉 이상 추세 확인.
- 전략 유형: 양방향 전략 / 스퀴즈 돌파 / 모멘텀 추세추종.

## 3. 매수 조건
1. 볼린저밴드 기본값 20SMA, 표준편차 2를 사용합니다.
2. 밴드폭이 축소되어 스퀴즈 상태가 형성됩니다.
3. 가격이 중심선 위로 회복하거나 상단 밴드 방향으로 강한 양봉을 형성합니다.
4. 거래량 CCI 또는 CCI가 0선을 상향 돌파하거나 +100 과매수선을 돌파합니다.
5. 직전 고점 또는 박스 상단을 종가 기준 돌파하면 롱 진입합니다.
6. 상승 추세 중 눌림에서는 중심선 기울기가 상승을 유지하고 CCI가 0선 아래에서 다시 위로 복귀할 때 재진입할 수 있습니다.

## 4. 매도/숏 조건
1. 밴드폭 축소 후 가격이 중심선 아래로 내려오거나 하단 밴드 방향 장대음봉을 형성합니다.
2. 거래량 CCI가 0선을 하향 돌파하거나 -100 과매도선을 돌파합니다.
3. 직전 저점 또는 박스 하단을 종가 기준 이탈하면 숏 진입합니다.
4. 하락 추세 중 되돌림 후 CCI가 0선 위에서 다시 아래로 복귀할 때 추가 숏 후보로 봅니다.

## 5. 손절 조건
- 롱: 진입 후 가격이 볼린저 중심선 아래로 종가 이탈하고 CCI도 0선 아래로 복귀하면 손절.
- 숏: 진입 후 가격이 중심선 위로 종가 회복하고 CCI도 0선 위로 복귀하면 손절.
- 스퀴즈 돌파 직후 반대편 밴드 방향으로 장대 캔들이 나오면 즉시 실패로 분류합니다.

## 6. 익절 조건
- 기본 익절: 강하게 터진 모멘텀이 과매수/과매도 영역에서 내부로 복귀할 때.
- 보조 익절: 가격이 볼린저 20SMA 중심선을 반대 방향으로 돌파할 때.
- 강한 추세 구간: 직전 스윙 저점/고점 이탈을 트레일링 기준으로 사용해 일부 추세를 더 보유합니다.

## 7. 필터 조건
- 시간대: 국내주식은 장 초반 첫 스퀴즈 돌파와 오후 재압축 돌파를 분리해 테스트.
- 거래량: CCI에 거래량 가중을 적용하거나, 별도로 돌파봉 거래량이 최근 평균 대비 증가했는지 확인.
- 변동성: 밴드폭 백분위가 낮은 구간에서만 스퀴즈로 인정.
- 시장 방향: 상위 시간봉 중심선 기울기와 같은 방향의 신호 우선.
- 종목 선정: 유동성 높고 스프레드가 좁은 종목/코인.

## 8. 백테스트 가능성
- 등급: 정량화 가능.
- 구현 난이도: 중간.
- 핵심 난점: 영상의 “거래량 CCI” 정확 산식이 공개 지표 의존일 수 있어 대체 산식 정의 필요.

## 9. 기계화 규칙 초안
```text
BB = Bollinger(close, length=20, stdev=2)
BandwidthPct = (upper-lower)/middle
Squeeze = BandwidthPct <= rolling_percentile(BandwidthPct, 20%)
VolCCI = CCI(typical_price * volume_weight or price CCI confirmed by volume_zscore)
LongEntry = Squeeze_recent and close > upper_or_box_high and VolCCI crosses above 0 or +100
ShortEntry = Squeeze_recent and close < lower_or_box_low and VolCCI crosses below 0 or -100
LongStop = close < BB_middle and VolCCI < 0
ShortStop = close > BB_middle and VolCCI > 0
ExitLong = VolCCI falls back below +100 or close < prior swing low
ExitShort = VolCCI rises back above -100 or close > prior swing high
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 거래량 CCI의 장점이 커질 수 있으나 점심 시간 저유동 구간의 가짜 신호를 제거하는 시간 필터가 필요합니다.
- 코인: 24시간 거래로 거래량 계절성이 강하므로 UTC/KST 시간대별 평균 거래량 대비 z-score를 사용해 가중 CCI를 보정합니다.

## 11. 리스크/반대 시나리오
- 볼린저밴드 평균회귀 신호와 추세 돌파 신호가 충돌할 수 있습니다.
- 밴드 상단 터치=숏, 하단 터치=롱을 기계적으로 적용하면 추세 분출 구간에서 큰 손실이 날 수 있습니다.
- 거래량 CCI 산식이 불명확하면 재현성이 떨어집니다.

## 12. 후속 검증 질문
1. 거래량 CCI를 `CCI(TP) * volume_zscore`로 근사해도 원신호와 유사한가?
2. 밴드폭 하위 20%와 10% 중 어떤 스퀴즈 기준이 더 유효한가?
3. 과매수/과매도 복귀 익절과 중심선 이탈 익절 중 어느 쪽이 기대값이 높은가?
4. 상위 시간봉 중심선 기울기 필터가 손실 거래를 줄이는가?
