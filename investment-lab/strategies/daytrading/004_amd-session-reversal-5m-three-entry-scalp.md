# 전략 후보: AMD 세션 리버설 + 5분봉 3-entry 스캘핑

## 1. 출처
- 채널/작성자: Trade with Pat
- 제목: “My BEST 5 Minute Scalping Strategy (330 Backtests)”
- URL: https://www.youtube.com/watch?v=Bdgev1or-7M
- 수집일: 2026-04-25
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/Bdgev1or-7M.txt`

## 2. 전략 요약
- 한 문장: 아시아 range 축적, 런던 liquidity sweep/방향성 push, 뉴욕 reversal이라는 AMD 구조를 방향 필터로 삼고 5분봉에서 지지저항·수요공급·ORB 세 가지 entry model 중 하나로 진입하는 스캘핑 전략입니다.
- 자산군: 원 영상은 Forex 중심. 코인에는 비교적 이식 가능, 국내주식은 세션 변형 필요.
- 시간프레임: 방향 15m 세션 구조, 진입 5m.
- 전략 유형: 양방향 전략, session reversal + price action.

## 3. 매수 조건
1. 아시아 세션에서 상대적으로 tight range가 형성됩니다.
2. 런던 세션에서 아시아 저점 유동성을 sweep하거나 하방으로 공격적 push가 발생합니다.
3. 뉴욕 세션에서 반대 방향 reversal long을 기대합니다. 아시아 range가 너무 넓거나 런던 push가 약하면 다른 차트로 이동합니다.
4. 5분봉에서 다음 entry model 중 하나가 발생해야 합니다.
   - Model 1: 지지/저항 — sweep 이후 기존 support/resistance zone에서 bullish engulfing 발생.
   - Model 2: 수요/공급 — 빨간 캔들 뒤 3~4개 큰 양봉, FVG와 구조 돌파가 동반된 demand zone 생성 후 재테스트.
   - Model 3: ORB — 09:30~09:45 opening range 상단을 종가 돌파 후 FVG/demand 되돌림과 bullish engulfing 확인.

## 4. 매도/숏 조건
1. 아시아 range 형성 후 런던 세션에서 아시아 고점 유동성을 sweep하거나 상방 push가 발생합니다.
2. 뉴욕 세션에서 reversal short bias를 설정합니다.
3. 5분봉에서 다음 entry model 중 하나가 발생합니다.
   - Model 1: 저항 전환 구간에서 bearish engulfing.
   - Model 2: supply zone 생성 후 재테스트와 bearish reaction.
   - Model 3: ORB 하단 종가 이탈 후 bearish FVG/supply 되돌림.

## 5. 손절 조건
- Model 1: 지지/저항 zone 반대편 ± buffer.
- Model 2: demand/supply zone 반대편.
- Model 3: FVG 반대편 또는 ORB range 반대편. 원 영상에서는 FVG 아래 stop과 약 1:2 target 예시가 제시됩니다.

## 6. 익절 조건
- 기본: 1R~2R, 특히 ORB 모델은 약 1:2 목표 예시.
- 구조 목표: 이전 지지/저항, supply/demand, 아시아 range 반대편 liquidity.
- 런던이 아시아 상단과 하단을 모두 sweep한 날에는 뉴욕이 다시 전체 range를 관통하지 않을 수 있으므로 보수적 목표가 필요합니다.

## 7. 필터 조건
- 시간대: Asia/London/NY 세션 분리, 실행은 뉴욕 세션.
- 거래량: 직접 언급은 없으나 런던 push와 뉴욕 reversal의 body/ATR를 거래량 대체 신호로 사용 가능.
- 변동성: Asian range가 너무 넓으면 축적 실패로 간주. London push가 약하면 manipulation 실패로 간주.
- 시장 방향: AMD 패턴이 방향 필터. 조건 불충족 시 no trade.
- 종목 선정: 세션성이 뚜렷하고 스프레드/슬리피지가 낮은 자산 우선.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간~높음
- 정량화 쉬운 요소: 세션 range, high/low sweep, 5m engulfing, ORB high/low 돌파, FVG.
- 추가 정의 필요 요소: tight range 임계값, aggressive London push, support/resistance zone 자동 탐지, demand/supply quality score.

## 9. 기계화 규칙 초안
1. Asia range 폭, London 누적수익률, London high/low의 Asia range sweep 여부를 계산합니다.
2. Long bias: London이 Asia low를 sweep하고 NY 시작 전 가격이 반등 구조를 만들거나, London 하락 body가 임계값 이상.
3. Short bias: London이 Asia high를 sweep하고 NY 시작 전 약세 반전 구조를 만들거나, London 상승 body가 임계값 이상.
4. Entry Model 1: 최근 N개 pivot 기반 S/R zone을 생성하고 zone touch 후 5m engulfing 종가 진입.
5. Entry Model 2: 3개 이상 연속 body + FVG + 구조돌파를 demand/supply score로 산출하고, score >= threshold인 zone 재테스트에서 진입.
6. Entry Model 3: 09:30~09:45 ORB를 만든 뒤 bias 방향 종가 돌파, 이후 FVG/demand/supply 재테스트에서 진입.
7. 세 모델을 별도 전략 ID로 백테스트하고, 중복 신호는 첫 신호 우선 또는 score 우선으로 처리합니다.
8. TP는 1R/1.5R/2R/Asia opposite side, SL은 zone 반대편으로 테스트합니다.

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 원형 세션 대신 “전일 오후 range → 시초가 갭/초반 sweep → 09:30 이후 reversal” 형태로 변형할 수 있습니다. 또는 KOSPI200 야간선물/미국장 방향을 London push의 대용치로 둘 수 있습니다.
- 코인: BTC/ETH 및 거래대금 상위 알트에서 Asia=KST 야간/오전 range, London/NY 세션으로 직접 매핑 가능합니다. 선물 데이터로 long/short 모두 테스트하는 것이 원전략에 가깝습니다.

## 11. 리스크/반대 시나리오
- AMD 패턴은 설명력이 높아 보이나 사후적으로 끼워 맞추기 쉽습니다.
- 아시아 range가 넓은 날을 제외하면 거래 빈도가 낮아질 수 있습니다.
- 세 entry model을 동시에 허용하면 조건이 느슨해져 과최적화 위험이 커집니다.
- 국내주식은 공백 시간과 단일 정규장 구조 때문에 원 전략의 세션 논리가 약화됩니다.

## 12. 후속 검증 질문
- 세 entry model을 분리했을 때 Model 1/2/3 중 어느 것이 기대값과 MDD가 가장 좋은가?
- Asian range 폭 필터의 적정 분위수는 30%, 40%, 50% 중 어디인가?
- London both-side sweep을 skip할지, continuation으로 별도 전략화할지 검증할 필요가 있는가?
- 국내주식 장초반 reversal에도 AMD 유사 구조가 통계적으로 존재하는가?
