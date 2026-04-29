# 025. ORB 리테스트·즉시 되돌림 자동화 스캘핑 모델

## 1. 출처
- 채널/작성자: Trade with Pat
- 제목: I Coded my Trading Strategy into a ROBOT
- URL: https://www.youtube.com/watch?v=s0I0JUCsldY
- 수집일: 2026-04-30
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/s0I0JUCsldY.txt`
- 핵심 근거 타임스탬프: 05:49~06:11 opening range와 entry modes, 06:13~06:51 range 돌파 후 retest same direction, 06:54~08:10 EMA/SR/news filter, 08:11~08:53 American session instant retrace, 09:22~11:39 grid/lot 증가와 리스크 목표

## 2. 전략 요약
- 한 문장: 특정 세션 opening range의 상·하단을 기준으로 돌파 후 같은 방향 리테스트 또는 range 내부 즉시 되돌림 지지/저항 반응을 자동 진입하되, EMA·S/R·뉴스·저변동성 필터와 낮은 리스크 설정을 결합하는 스캘핑 모델입니다.
- 자산군: 원영상은 FX/CFD 자동매매, 적용 후보는 코인·국내주식 장초반 ORB
- 시간프레임: 세션 range 설정 5~30분, 실행 1~5분봉
- 전략 유형: 양방향 전략, 자동화/기계화 아이디어

## 3. 매수 조건
### A. Retest range same direction 롱
1. 세션 시작 후 지정 시간 동안 opening range high/low 산출.
2. 가격이 range high 위로 종가 돌파.
3. 돌파 후 range high를 지지로 재테스트.
4. EMA 필터 사용 시 가격이 EMA 위에 있어야 함.
5. S/R 필터 사용 시 range high가 과거 저항→지지 전환 레벨과 겹쳐야 함.

### B. Instant retrace 롱
1. opening range가 형성된 뒤 가격이 range low 또는 내부 지정 support retrace level로 되돌림.
2. 해당 레벨을 즉시 지지로 사용하는 반응에서 진입.
3. 저변동성 환경 및 뉴스 회피 조건을 만족.

## 4. 매도/숏 조건
### A. Retest range same direction 숏
1. opening range low 아래로 종가 이탈.
2. 돌파 후 range low를 저항으로 재테스트.
3. EMA 필터 사용 시 가격이 EMA 아래.
4. S/R 필터 사용 시 range low가 과거 지지→저항 전환 레벨.

### B. Instant retrace 숏
1. range high 또는 내부 지정 resistance retrace level로 되돌림.
2. 해당 레벨에서 저항 반응이 나오면 숏.
3. 고충격 뉴스 전후 회피.

## 5. 손절 조건
- Retest 모델: 롱은 range high 재이탈, 숏은 range low 재돌파 시 손절.
- Instant retrace 모델: 롱은 range low 하단, 숏은 range high 상단 이탈 시 손절.
- ATR/points/stop-loss ratio 중 하나로 자동 손절폭 설정 가능.
- 중요: 영상 후반의 grid 및 lot size 증가는 계좌 폭발 위험이 있으므로 기본 연구 모델에서는 비활성화합니다.

## 6. 익절 조건
- 고정 pip/points 또는 range 폭의 0.5~1.0배를 1차 목표로 설정.
- 손절폭 대비 최소 1R, 저변동성 스캘핑에서는 0.8~1.2R의 고승률 모델도 별도 테스트.
- 자동매매에서는 take-profit을 사전에 설정하고 임의 확장보다 반복성 우선.

## 7. 필터 조건
- 시간대: Asian, European, London, American, NYSE open 등 세션별 range를 선택 가능. 국내주식은 09:00~09:15 또는 09:00~09:30 ORB 후보.
- 거래량/변동성: 전략 설명상 “low volatility” 선호. 고충격 뉴스 전후 60분 회피.
- 시장 방향: EMA 필터로 롱/숏 방향 제한 가능.
- S/R: 과거 지지·저항과 opening range 레벨이 겹칠 때만 거래하는 보수형 필터.
- 종목 선정: 스프레드 낮고 체결 안정적인 FX/대형 코인/국내 거래대금 상위 종목.

## 8. 백테스트 가능성
- 등급: 정량화 가능
- 구현 난이도: 중간
- 가능 요소: 세션 range, breakout close, retest, instant retrace, EMA, S/R, 뉴스 회피, ATR 손절/익절 모두 규칙화 가능.
- 주의 요소: 영상의 robot 내부 세부 파라미터는 공개되지 않았으므로 독립 모델로 재정의해야 합니다.

## 9. 기계화 규칙 초안
1. 세션 정의:
   - 코인: Asia 09:00 KST, London 16:00 KST, NY 22:30/23:30 KST 전후.
   - 국내주식: 09:00~09:15 또는 09:00~09:30.
2. OR high/low 계산.
3. Retest same direction:
   - 롱: OR high 상향 종가 돌파 → 1~10봉 내 OR high ±0.1ATR 재방문 → 양봉 종가 진입.
   - 숏: OR low 하향 종가 이탈 → 재테스트 저항 확인 → 음봉 종가 진입.
4. Instant retrace:
   - OR 형성 후 OR low 부근에서 롱, OR high 부근에서 숏. 단, EMA 방향 또는 상위 추세 필터와 충돌하면 제외.
5. 필터:
   - 고충격 뉴스 ±60분 제외.
   - ATR percentile이 과도하게 높으면 제외, 너무 낮으면 목표폭 축소.
   - EMA200 방향과 일치하는 거래만 테스트하는 버전 추가.
6. 리스크:
   - trade당 계좌 0.25~0.5% 위험.
   - grid/martingale/lot 증가 금지 버전과 제한적 grid 버전을 분리 검증.

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 09:00~09:15 ORB 후 09:15~10:00 재테스트 매매에 적합합니다. 단, 시초가 갭과 VI/호가 공백을 반영해야 합니다.
- 코인: 24시간 시장에서는 세션별 유동성 변화가 있으므로 London/NY open 기준 ORB를 테스트할 수 있습니다. 뉴스 필터는 FOMC/CPI/금리 이벤트에 특히 중요합니다.

## 11. 리스크/반대 시나리오
- Opening range 돌파 후 리테스트는 흔한 패턴이라 수수료·슬리피지 차감 후 edge가 작을 수 있습니다.
- Instant retrace는 range 내부 평균회귀와 추세 돌파가 충돌할 수 있어 시장 상태 필터가 필요합니다.
- Grid/lot 증가 자동화는 작은 변동에도 계좌 손실이 비선형으로 커지는 tail risk가 있습니다.
- 뉴스 회피 필터가 없으면 전략이 저변동성 전제와 맞지 않게 작동할 수 있습니다.

## 12. 후속 검증 질문
1. 국내주식 ORB는 5분, 15분, 30분 중 어느 range가 기대값이 높은가?
2. Retest same direction과 Instant retrace 중 자산별로 어느 모드가 더 안정적인가?
3. EMA200 필터와 S/R 필터를 동시에 쓰면 거래 수 감소 대비 MDD가 개선되는가?
4. 뉴스 ±60분 회피가 코인/국내주식에서도 유의미한 성과 차이를 만드는가?
