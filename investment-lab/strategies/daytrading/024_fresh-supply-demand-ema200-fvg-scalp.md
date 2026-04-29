# 024. 1분봉 신선한 수요·공급존 추세추종 스캘핑

## 1. 출처
- 채널/작성자: Trade with Pat
- 제목: The Silver Trading Strategy I Use to Catch Explosive Moves
- URL: https://www.youtube.com/watch?v=n5xZri8VxWs
- 수집일: 2026-04-30
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/n5xZri8VxWs.txt`
- 핵심 근거 타임스탬프: 01:07~02:38 큰 변동 시작점의 demand/supply zone, 03:26~05:20 FVG·200EMA·BOS·old supply 돌파, 05:23~07:07 회피 조건, 07:09~08:20 limit/candle close/engulfing entry, 09:19~09:53 range 위치 필터

## 2. 전략 요약
- 한 문장: 1분봉에서 200EMA 방향의 큰 displacement가 만든 신선한 수요/공급존을 표시하고, 가격이 처음 되돌아왔을 때 캔들 반응 또는 engulfing 확인으로 진입하는 양방향 스캘핑 전략입니다.
- 자산군: 원영상은 Silver/XAG, 적용 후보는 코인·지수선물·국내주식 급등주
- 시간프레임: 1분봉 중심, 보조 5분봉/상위 흐름 확인
- 전략 유형: 양방향 전략

## 3. 매수 조건
1. 가격이 200EMA 위에 있고, 고점·저점 구조가 상승 추세.
2. 큰 양봉 또는 연속 양봉의 displacement 발생.
3. displacement 중 FVG/imbalance가 관찰되고 직전 swing high 또는 old supply를 돌파(BOS).
4. 상승 시작점의 마지막 음봉 또는 마지막 캔들 범위를 demand zone으로 표시.
5. 가격이 해당 demand zone에 처음 재방문한 뒤 다음 중 하나로 진입:
   - 공격형: zone touch limit order.
   - 보수형: demand 존 방어 후 양봉 종가.
   - 최고 확인형: 작은 음봉을 완전히 감싸는 bullish engulfing.
6. range 필터: 롱은 최근 range 하단에 가까운 demand에서만 선호.

## 4. 매도/숏 조건
1. 가격이 200EMA 아래에 있고, 저점·고점 구조가 하락 추세.
2. 큰 음봉 또는 연속 음봉의 displacement 발생.
3. 하락 중 FVG/imbalance가 있고 직전 swing low 또는 old demand를 하향 돌파.
4. 하락 시작점의 마지막 양봉/직전 캔들을 supply zone으로 표시.
5. 가격이 supply zone에 처음 재방문한 뒤 limit, 음봉 종가, bearish engulfing 중 하나로 숏 진입.
6. 숏은 range 상단에 가까운 supply에서만 선호.

## 5. 손절 조건
- 롱: demand zone 하단을 1분봉 종가로 명확히 이탈하면 손절. limit 진입은 zone 하단 + buffer를 고정 손절로 설정.
- 숏: supply zone 상단을 1분봉 종가로 돌파하면 손절.
- 가격이 zone을 종가 기준으로 관통하면 해당 zone은 “dead zone”으로 분류하고 재사용 금지.
- 첫 반응이 약하고 즉시 큰 반대 캔들이 나오면 조기 청산.

## 6. 익절 조건
- 1차 목표: 직전 swing high/low 또는 range 반대편.
- 2차 목표: displacement 시작 후 형성된 다음 유동성 고점/저점.
- 최소 손익비는 1R 이상, 가능하면 zone 폭 대비 1.5~2R 이상 확보.
- 1차 목표 도달 후 잔여는 breakeven 또는 직전 1분봉 저점/고점 trailing.

## 7. 필터 조건
- 시간대: London 또는 New York session. 국내주식 적용 시 09:00~10:30, 14:00 이후 재가속 구간 별도 검증.
- 거래량: displacement 캔들 거래량이 직전 N봉 평균 이상이어야 함.
- 변동성: 너무 오래된 zone, 이미 한 번 반응한 used zone 제외. 최근 zone 우선.
- 시장 방향: 200EMA 및 swing structure 방향과 일치.
- 종목 선정: 유동성 충분하고 스프레드가 좁은 상품. 코인은 BTC/ETH/상위 알트, 국내주식은 거래대금 상위 급등주.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간~높음
- 가능 요소: 200EMA, displacement 크기, FVG, BOS, 첫 재방문, engulfing, zone 재사용 금지는 규칙화 가능.
- 어려운 요소: 수요/공급존을 어느 캔들 범위로 잡을지, “큰 캔들” 기준, range 상단/하단의 재량적 표시.

## 9. 기계화 규칙 초안
1. 1분봉에서 `abs(body) > 2.0 * median(body, 50)`인 displacement candle 또는 3봉 누적 이동폭 > 2ATR(50) 탐지.
2. 롱 zone: displacement 시작 직전 마지막 음봉의 high~low. 숏 zone: 직전 마지막 양봉의 high~low.
3. FVG 조건: 3캔들 구조에서 `low[t] > high[t-2]`(롱), `high[t] < low[t-2]`(숏).
4. 추세 필터: close > EMA200 & swing high 돌파; 숏은 반대.
5. Freshness: zone 생성 후 첫 touch만 거래, touch 전 60봉 초과 시 폐기.
6. 진입 모델별 비교:
   - A: touch limit.
   - B: zone touch 후 다음 1분봉이 방향성 종가.
   - C: engulfing 확인.
7. 손절: zone 반대편 + 0.1ATR buffer. 익절: 1.5R 또는 최근 range 반대편.

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 장초반 거래대금 상위 급등주에서 1분봉 displacement 후 첫 눌림 진입으로 테스트할 수 있습니다. 단, 호가 공백과 VI 발동 리스크를 필터링해야 합니다.
- 코인: 24시간 거래라 London/NY 세션의 유동성 증가 구간에서 BTC 방향 필터와 함께 적용 가능합니다. 수수료/슬리피지 민감도가 높습니다.

## 11. 리스크/반대 시나리오
- 공급/수요존은 사후적으로 좋아 보이는 경향이 있어 과최적화 위험이 큽니다.
- 1분봉은 노이즈와 슬리피지가 커 실제 체결 성과가 백테스트보다 낮을 수 있습니다.
- 강한 추세일수록 zone touch를 주지 않고 진행해 미체결이 많을 수 있습니다.
- limit 진입은 승률이 낮고, engulfing 진입은 거래 수가 줄어드는 trade-off가 있습니다.

## 12. 후속 검증 질문
1. Silver에서 제시된 1분봉 규칙이 BTC/ETH 1분봉에서도 유효한가?
2. 진입 모델 A/B/C 중 기대값과 MDD가 가장 안정적인 방식은 무엇인가?
3. FVG 필터를 넣으면 거래 수 감소 대비 승률/손익비가 개선되는가?
4. used zone 금지와 old zone 폐기 기준은 몇 봉이 최적인가?
