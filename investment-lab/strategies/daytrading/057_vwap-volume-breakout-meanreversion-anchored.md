# 057. VWAP 거래량 돌파·평균회귀·앵커드 VWAP 단타 전략

## 1. 출처
- 채널/작성자: 차트슈타인
- 제목: 지표 하나로 차트의 역사를 바꾼 단 하나의 사건(이동평균, 거래량 통합 매매법)
- URL: https://www.youtube.com/watch?v=mGpwO_XD1e0
- 수집일: 2026-05-10
- 원문 위치: `data/raw_transcripts/youtube/mGpwO_XD1e0.txt`

## 2. 전략 요약
- 한 문장: 당일 VWAP의 기울기·이격·거래량 동반 여부를 기준으로 횡보장 평균회귀와 추세장 돌파/눌림을 구분하고, 주요 고저점에는 앵커드 VWAP로 지지·저항을 재설정하는 전략입니다.
- 자산군: 국내주식, 코인, 선물
- 시간프레임: 1분~15분봉 중심
- 전략 유형: 양방향 전략 / VWAP 추세·평균회귀

## 3. 매수 조건
1. 횡보장 평균회귀: VWAP가 평평한데 가격만 VWAP 아래로 과도하게 이격된 뒤 회복 신호가 나오면 VWAP 회귀를 노립니다.
2. 추세 돌파: 가격이 VWAP를 상향 돌파하고 해당 구간 최고 수준의 거래량이 동반되면 롱 진입합니다.
3. 추세 눌림: VWAP가 상승 기울기이고 가격이 VWAP 또는 앵커드 VWAP를 터치한 뒤 위로 재돌파할 때 진입합니다.
4. 코인 예시처럼 급락 꼬리 중에는 잡지 않고, VWAP/앵커드 VWAP를 다시 상향 통과하는 순간을 기다립니다.

## 4. 매도/숏 조건
1. VWAP 하향 돌파가 강한 음봉·구간 최대 거래량과 동반되면 숏 진입합니다.
2. 하락 추세에서 가격이 VWAP에 되돌림으로 닿고 재차 밀리면 추가 숏 후보입니다.
3. 쌍고점에서 가격은 고점을 높이지만 VWAP는 따라오르지 못하고 거래량이 감소하면 숏 또는 롱 청산 신호로 봅니다.

## 5. 손절 조건
- 롱: 거래량 실린 강한 음봉이 VWAP/앵커드 VWAP를 몸통으로 하향 돌파하면 손절.
- 숏: 거래량 실린 강한 양봉이 VWAP/앵커드 VWAP를 몸통으로 상향 돌파하면 손절.
- 돌파 진입 직후 반대색 고거래량 캔들이 나오면 즉시 무효화합니다.

## 6. 익절 조건
- 횡보 평균회귀: VWAP 근처 또는 반대편 박스/밴드에서 익절.
- 추세 추종: VWAP를 몸통으로 반대 돌파할 때까지 보유.
- 긴 윗꼬리, 하락장악형/상승장악형, 거래량 다이버전스가 나오면 조기 익절합니다.

## 7. 필터 조건
- 시간대: 당일 VWAP는 매일 리셋되므로 데이트레이딩에 적합합니다.
- 거래량: 돌파 신뢰도는 거래량 동반 여부가 핵심입니다.
- 변동성: VWAP가 평평하면 평균회귀, 기울기가 뚜렷하면 추세추종으로 분기합니다.
- 시장 방향: 상위 시간봉 추세와 같은 방향의 VWAP 돌파를 우선합니다.
- 종목 선정: 거래대금 상위, 스프레드 낮은 종목/코인.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간
- 이유: 일반 VWAP 규칙은 정량화가 쉽지만, 앵커드 VWAP의 시작점(주요 고점/저점·뉴스 시점) 정의와 캔들 힘/다이버전스 정량화가 필요합니다.

## 9. 기계화 규칙 초안
```text
VWAP = intraday volume weighted average price reset daily
FlatVWAP = abs(slope(VWAP, n)) < threshold
TrendVWAP = slope(VWAP, n) > threshold or < -threshold
VolumeBreakout = volume >= rolling_volume_max(M) or volume >= avg_volume * x
LongBreakout = close crosses above VWAP and VolumeBreakout
ShortBreakout = close crosses below VWAP and VolumeBreakout
LongPullback = TrendVWAP up and low <= VWAP/AVWAP and close reclaims VWAP/AVWAP
ShortPullback = TrendVWAP down and high >= VWAP/AVWAP and close rejects VWAP/AVWAP
Stop = opposite high-volume body close across VWAP/AVWAP
AVWAP anchors = confirmed swing high/low, session open, major news timestamp
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 1분/3분봉 거래대금 상위 급등주에서 당일 VWAP 회복·이탈을 기준으로 돌파와 눌림을 분리합니다.
- 코인: 15분봉 BTC/알트에서 꼬리 하락을 직접 잡지 않고 AVWAP 재돌파를 확인해 진입하는 방식으로 변형합니다.

## 11. 리스크/반대 시나리오
- VWAP가 평평한 횡보장과 추세장 구분이 틀리면 평균회귀와 추세추종 신호가 충돌합니다.
- 앵커드 VWAP 시작점을 사후적으로 고르면 백테스트가 과대평가됩니다.
- 거래량 급증은 진짜 돌파뿐 아니라 클라이맥스 반전 신호일 수도 있습니다.

## 12. 후속 검증 질문
1. VWAP 기울기 임계값을 어떻게 정량화할 것인가?
2. AVWAP anchor를 swing high/low 확정 후 몇 봉 뒤에 설정할 것인가?
3. 고거래량 돌파 후 다음 봉 확인 진입과 즉시 진입 중 어느 방식의 기대값이 높은가?
