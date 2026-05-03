# 040. 급등 갭업 과열주 숏 회피·클린 페이드 선별 필터

## 1. 출처
- 채널/작성자: Kristjan Kullamägi / Qullamaggie
- 제목: Lessons from a $140K loss
- URL: https://qullamaggie.com/lessons-from-a-140k-loss/
- 수집일: 2026-05-04
- 원문 위치: `sources/articles/raw/2026-05-04_qulla_lessons.txt`

## 2. 전략 요약
- 한 문장: 2주 +200% 이상 급등 후 저항대 갭업한 종목을 숏 후보로 보되, 장중 저점 이탈이 반복 실패하고 opening price 위를 유지하는 “range of death” 강한 종목은 제외하고, 약한 동종 테마의 clean fade만 거래하는 숏 선별/회피 전략입니다.
- 자산군: 미국 주식 사례. 국내 급등 테마주, 코인 과열 알트 숏/롱 청산 필터로 응용 가능.
- 시간프레임: 프리마켓/시초가, 5분봉, 일봉 2주 상승률.
- 전략 유형: 매도/숏 전략 + 회피 필터.

## 3. 매수 조건
- 본 전략의 주된 목적은 과열주 숏 선별입니다.
- 역방향 매수 관점에서는 다음을 만족하면 숏 금지 및 롱 관찰 가능:
  1. 큰 갭업 이후 시초가/opening price 위에서 계속 지지.
  2. 지수 약세에도 해당 종목이 장중 저점 이탈 실패.
  3. 여러 차례 하방 이탈처럼 보이다가 즉시 범위 안으로 복귀.
  4. 동종 약한 종목은 하락하는데 해당 종목만 상대강도 유지.

## 4. 매도/숏 조건
1. 후보: 최근 2주 내 +100~240% 이상 급등, 프리마켓/시초가 갭업, 상위 저항대 접근.
2. 시장/섹터가 갭업 후 유지 실패 또는 약세 전환.
3. 대상 종목이 opening price 아래로 내려오고, 5분봉 기준 명확한 하락 range를 형성.
4. 직전 장중 저점 또는 opening range low 이탈 후 반등이 약하고 lower high 형성.
5. 동종 카지노/크루즈/항공처럼 같은 테마 내 더 약한 종목들이 clean fade를 보이면, 가장 강한 종목보다 약한 종목을 우선 숏.

## 5. 손절 조건
- opening price 또는 VWAP 상향 회복 후 5분봉 종가 유지 시 숏 중단.
- range high 돌파 또는 저점 이탈 실패 후 range 내부 복귀 시 즉시 축소/청산.
- 강한 종목에서 평균단가 개선을 위한 반복 scale-in 금지. 원문 손실은 강한 종목에서 여러 차례 scale in/out한 것이 핵심 원인.

## 6. 익절 조건
- 1차: opening range low 이탈 후 다음 5분 지지/프리마켓 지지.
- 2차: 갭 일부 메우기, VWAP 하방 확장, 15~25% fade 시나리오 일부.
- 장중 clean fade가 지속되면 5분 lower high 또는 VWAP/9EMA 회복 전까지 트레일링.

## 7. 필터 조건
- 시간대: 프리마켓 갭과 장초반 30~60분 반응 중요.
- 거래량: 과열 갭업주는 거래량이 매우 커야 하지만, 호가 공백이 큰 종목은 제외.
- 변동성: 2주 +100% 이상, 당일 갭업, ATR 확대.
- 시장 방향: 지수 갭업 실패/하락 전환은 숏 우호. 그러나 종목이 지수 약세에도 강하면 숏 회피.
- 종목 선정: 같은 테마 내 가장 강한 대장주를 피하고, opening price 아래로 무너지는 약한 후발주/동종주 우선.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 중간~높음
- 이유: 2주 상승률, 갭업, opening price 유지, ORL 이탈, 상대강도는 정량화 가능. 다만 “range of death”, clean fade, 동종 테마 내 상대강도 정의가 필요합니다.

## 9. 기계화 규칙 초안
```text
1) short_candidate = return_10d >= +100% AND gap_open >= +5% AND open near 20d resistance/high.
2) market_weak = index intraday return from open < -0.5% or index close below first 30m low.
3) avoid_strong = stock price remains above open for first 30~60m OR failed_breakdowns >= 2 OR relative_strength_vs_theme > 0.
4) clean_fade = close below opening price AND close below ORL_15m AND pullback forms lower high below VWAP.
5) entry_short = retest of ORL/VWAP failure after clean_fade.
6) stop = reclaim of open/VWAP/range_high on 5m close.
7) target = prior intraday support, premarket support, or 2R. No averaging up into strength.
```

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 2주 급등률, 당일 갭상승, VI 이후 시초가/기준가 회복 여부를 필터화. 대장주는 공매도 제약이 있으므로 실제 숏보다는 롱 청산/신규 롱 회피 필터로 활용 가치가 큽니다.
- 코인: 최근 7~14일 +100% 이상 급등 알트가 펀딩비 과열 상태에서 BTC 약세에도 고점권 박스를 유지하면 섣부른 숏 금지. ORL 이탈 후 VWAP 회복 실패까지 기다리는 방식으로 변환.
- 선물 가능 종목에서는 가장 강한 코인보다 동일 테마 내 약한 알트를 숏 후보로 삼는 pair/relative weakness 아이디어 가능.

## 11. 리스크/반대 시나리오
- 과열은 더 과열될 수 있으며, 가장 강한 종목을 고점이라고 판단해 숏하면 squeeze 위험이 큽니다.
- 지수 약세가 개별주 호재/수급을 압도하지 못하는 경우, opening price 위 range가 숏의 함정이 됩니다.
- 국내주식은 공매도/대주/CFD 접근성, 상한가, VI로 인해 실제 숏 구현이 제한될 수 있습니다.
- 코인은 청산 레버리지와 펀딩비 변동으로 기술적 손절보다 빠른 강제청산 위험이 있습니다.

## 12. 후속 검증 질문
1. “range of death”를 failed ORL breakdown 횟수와 opening price 유지 시간으로 정의할 수 있는가?
2. 동종 테마 상대약세를 산업분류, 당일 수익률, VWAP 위치 중 무엇으로 측정할 것인가?
3. 2주 +100%, +150%, +200% 급등 조건별 숏 성공률 차이는?
4. 대장주 숏 회피 규칙이 롱 continuation 필터로도 유효한가?
