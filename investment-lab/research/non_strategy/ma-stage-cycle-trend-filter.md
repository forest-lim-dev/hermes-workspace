# 3 Moving Average Stage Cycle Trend Filter (Qullamaggie/Kojirō 참고)

## 1. 출처
- 채널/작성자: 슈퍼트레이더
- 제목: 12 million KRW ➔ 140 billion KRW using a trading method with only 3 moving averages (How to read ...)
- URL: https://www.youtube.com/watch?v=HfrlrYC0s74
- 수집일: 2026-04-28
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/HfrlrYC0s74.txt`
- 주요 근거 구간: 04:39~05:10 정배열/역배열 엣지, 09:31~10:35 10/20/50 또는 5/20/40 이동평균, 11:55~17:23 대순환 6단계와 매매/관망 구간

## 2. 아이디어 요약
- 단타 진입 전략이라기보다, 단타 전략의 방향 필터와 종목 선정 필터로 사용할 수 있는 3개 이동평균 기반 시장 단계 분류입니다.
- 핵심은 단기·중기·장기 이평선의 배열, 간격, 기울기로 “롱 엣지 구간”, “숏/회피 엣지 구간”, “관망 구간”을 분리하는 것입니다.

## 3. 규칙 후보
1. 이동평균 조합은 `10/20/50` 또는 `5/20/40`을 후보로 둡니다.
2. 안정 상승기: 위에서부터 단기 > 중기 > 장기 순서이고 세 선의 기울기가 모두 양수입니다.
3. 안정 하락기: 위에서부터 장기 > 중기 > 단기 순서이고 세 선의 기울기가 모두 음수입니다.
4. 나머지 배열 전환 구간은 방향성이 불명확하므로 신규 단타 진입 빈도를 줄입니다.
5. 안정 상승기에는 롱 단타 전략만 허용하고, 안정 하락기에는 숏 전략 또는 국내주식 롱 회피만 허용합니다.

## 4. 단타 전략에 결합하는 방법
- ORB, FVG, demand pullback, pattern breakout 전략의 상위 방향 필터로 사용합니다.
- 1분봉 전략에는 15분/30분/60분 이평 단계, 5분봉 전략에는 60분/일봉 이평 단계를 비교 검증합니다.
- 개별 종목 선정에는 일봉 10/20/50 정배열과 5분봉 장초 setup을 결합하는 방식이 유력합니다.

## 5. 백테스트 가능성
- 등급: 정량화 가능
- 구현 난이도: 낮음
- 단독 매매 전략으로는 신호가 느릴 수 있으나, 필터로는 구현이 쉽고 과최적화 위험이 비교적 낮습니다.

## 6. 기계화 규칙 초안
```text
ma_s = SMA(close, 10)
ma_m = SMA(close, 20)
ma_l = SMA(close, 50)
slope_s = ma_s - ma_s[5]
slope_m = ma_m - ma_m[5]
slope_l = ma_l - ma_l[5]

stage_up = ma_s > ma_m > ma_l and slope_s > 0 and slope_m > 0 and slope_l > 0
stage_down = ma_l > ma_m > ma_s and slope_s < 0 and slope_m < 0 and slope_l < 0
stage_unclear = not stage_up and not stage_down

allow_long = stage_up
allow_short = stage_down
allow_new_trade = not stage_unclear
```

## 7. 국내주식/코인 적용 아이디어
- 국내주식: 당일 단타 후보를 전일 기준 일봉 10/20/50 정배열 종목으로 제한하거나, 최소 60분봉 정배열 종목만 롱 후보로 둡니다.
- 코인: BTC 1시간/4시간 stage가 상승이면 알트 롱 단타만, 하락이면 알트 롱 빈도를 줄이는 시장 레짐 필터로 사용합니다.

## 8. 리스크/반대 시나리오
- 이평선 필터는 후행성이 있어 반전 초입의 좋은 단타 기회를 제외할 수 있습니다.
- 장초 급등주는 일봉 이평 정배열 전에 먼저 움직이는 경우가 있어 모멘텀 전략과 충돌할 수 있습니다.
- 횡보장에서는 stage가 자주 바뀌어 진입/관망 전환이 잦아질 수 있습니다.

## 9. 후속 검증 질문
1. 단타 진입 필터는 일봉, 60분봉, 30분봉 중 어느 상위 프레임이 가장 적합한가?
2. 10/20/50과 5/20/40 중 국내주식 테마주에 더 적합한 조합은?
3. stage_unclear에서 거래를 완전히 차단할지, 포지션 크기만 줄일지?
4. 기존 ORB/FVG 전략에 결합할 때 승률 상승과 거래 수 감소의 균형은?
