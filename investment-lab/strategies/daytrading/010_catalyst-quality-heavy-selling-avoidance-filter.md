# 전략 후보: Catalyst Quality + Heavy Selling 회피 필터

## 1. 출처
- 채널/작성자: Ross Cameron - Warrior Trading
- 제목: “+$2,306.80 Trading Leading Percentage Gainers”
- URL: https://www.youtube.com/watch?v=hrZJKJ9NGbk
- 수집일: 2026-04-26
- 원문 위치: `investment-lab/data/raw_transcripts/youtube/hrZJKJ9NGbk.txt`

## 2. 전략 요약
- 한 문장: 당일 상승률 상위 종목이라도 뉴스 catalyst의 질, 공모/매도 가능성, ask 매물 두께, 반복된 고점 실패를 확인해 “거래하지 않을 종목”을 걸러내는 장초반 모멘텀 회피/선별 전략입니다.
- 자산군: 원 영상은 미국 소형주 day trading.
- 시간프레임: 프리마켓~장초반, 1분/5분 intraday 차트.
- 전략 유형: 매수 전략의 필터/회피 규칙, ambiguous idea에 가까우나 기계화 가능한 리스크 필터로 분류.

## 3. 매수 조건
1. 기본 universe는 당일 leading % gainer 또는 scanner 포착 종목입니다.
2. 뉴스 catalyst가 존재하고, 내용이 실제 실적/계약/승인처럼 가격 재평가를 유발할 수 있어야 합니다.
3. 프리마켓에서 고점 돌파 시 거래량이 증가하고, MACD 등 모멘텀 지표가 양호하며, ask 매물이 얇아야 합니다.
4. 직전 고점/심리적 가격대를 돌파할 때 빠른 squeeze가 나올 수 있으면 단기 매수 후보입니다.
5. 영상 사례 NTIP처럼 뉴스가 있고 volume이 증가하며 high break가 나올 때만 짧게 진입합니다.

## 4. 매도/숏 조건
- 원 영상은 숏 진입 전략보다 매수 회피/청산 판단에 초점이 있습니다.
- 회피/청산 신호:
  1. Catalyst가 없거나 확인되지 않는 급등.
  2. 전일/최근 이미 급등했던 종목이 다시 뜨지만 뉴스가 없는 경우.
  3. 고점 돌파 시도 후 double top 또는 false breakout.
  4. ask에 매도 물량이 두껍게 쌓이고 가격이 “pull away”하지 못하는 경우.
  5. 공모, shelf registration, ATM, placement agent 등 공급 매물 가능성이 있는 filings.
  6. “Projected revenue surge”처럼 실제 확정 실적이 아닌 홍보성/예상성 헤드라인.

## 5. 손절 조건
- 돌파 매수 진입 시 직전 breakout level 또는 직전 pullback low 이탈.
- 첫 시도 실패 후 같은 레벨에서 반복 rejection이 나오면 손절 또는 추가 진입 금지.
- 작은 수익/본전 수준이어도 heavy selling이 확인되면 즉시 위험 축소.

## 6. 익절 조건
- 빠른 high break squeeze에서는 직후 spike 구간에서 부분/전량 청산.
- 목표가보다 “작동하지 않으면 바로 줄인다”가 핵심입니다.
- 당일 시장이 약하거나 금요일 후반처럼 catalyst 품질이 낮을 때는 작은 green day에 만족하고 거래 빈도를 줄이는 규칙이 포함됩니다.

## 7. 필터 조건
- 시간대: 프리마켓 07:00 이후~장초반. 금요일/주 후반에는 좋은 뉴스 빈도가 낮고 bad news가 늦게 나올 수 있다는 계절성/요일성 관찰.
- 거래량: scanner 포착, high break 시 volume pickup 필요. 그러나 pop 후 대량 매도 volume profile이면 경계.
- 변동성: +50~100% 급등 종목이어도 round trip이면 제외.
- 시장 방향: 개별 catalyst 우선. 다만 cold market에서는 목표를 낮추고 선택적으로 거래.
- 종목 선정: leading % gainer, 가격이 너무 낮은 penny stock은 제외 가능, 중국/HK 기업·공모 이력·shelf registration은 리스크 태그.

## 8. 백테스트 가능성
- 등급: 부분 정량화 가능
- 구현 난이도: 높음
- 정량화 쉬운 요소: 당일 상승률, gap%, 뉴스 유무, high break 실패 횟수, volume profile, 고점 재돌파 후 유지 실패, price pull-away 여부.
- 어려운 요소: catalyst 품질 평가, SEC filing 해석, ask stack/호가 두께, 실제 스캐너 포착 시점.
- 전략 성격: 독립 진입 전략보다 기존 leading gainer/micro pullback 전략의 negative filter로 가치가 큽니다.

## 9. 기계화 규칙 초안
1. Universe: premarket 또는 intraday gainers 상위, 가격 1~20달러, 상대거래량 상위.
2. Catalyst_score:
   - +2: 실적/승인/계약/인수 등 확정성 높은 뉴스.
   - +1: analyst rating/목표가/전망성 뉴스.
   - 0: 뉴스 없음.
   - -2: offering, shelf/ATM 사용 가능성, placement agent 이해상충, 확정되지 않은 projection.
3. Supply_risk_score: 최근 S-3/F-3, ATM, offering, warrant, insider/등록 매물 키워드 존재 시 감점.
4. Heavy_selling_flag: 고점 돌파 후 1~3분 안에 거래량 증가와 함께 range의 50% 이상 반납하거나, 동일 고점에서 2회 이상 rejection.
5. Pull_away_rule: high break 후 N초/분 내 +0.5R 이상 전진하지 못하고 ask imbalance가 크면 no-add/exit.
6. Trade_allowed = Catalyst_score >= 1 and Supply_risk_score >= 0 and Heavy_selling_flag == false.
7. If Trade_allowed false: 매수 전략 신호가 있어도 skip, 또는 position size 50~75% 축소.

## 10. 국내주식/코인 적용 아이디어
- 국내주식: 공시/뉴스의 질을 “실적·계약·정부정책·테마성 보도·풍문”으로 점수화하고, 전환사채/유상증자/대주주 매도 가능성을 공급 리스크로 태깅할 수 있습니다. 상한가/VI 이후 round trip과 매도호가 잔량 급증을 heavy selling flag로 사용할 수 있습니다.
- 코인: catalyst 품질은 거래소 상장, 메인넷/파트너십/토큰언락/재단 매도 가능성으로 변환합니다. 낮은 유동성 알트의 CEX 상장 직후 펌프 후 덤프를 회피하는 필터로 활용 가능합니다.

## 11. 리스크/반대 시나리오
- 좋은 catalyst라도 시장 전체 유동성이 약하면 돌파가 실패할 수 있습니다.
- 반대로 뉴스가 없어도 숏스퀴즈/커뮤니티 수급만으로 강한 상승이 나올 수 있어 과도한 필터는 기회비용을 만듭니다.
- SEC filing/공시 해석 자동화는 오류 가능성이 높고, 실제 공급 매물 출회 여부는 사후에야 확인될 수 있습니다.
- “거래 안 함” 전략은 백테스트에서 성과 측정이 어렵지만 손실 회피 효과를 별도로 평가해야 합니다.

## 12. 후속 검증 질문
- Catalyst_score가 낮은 leading gainer를 제외하면 기존 micro pullback 전략의 MDD와 승률이 얼마나 개선되는가?
- Offering/shelf/CB 리스크 태그가 실제 intraday round trip 확률을 유의미하게 설명하는가?
- 동일 고점 2회 rejection 후 3회째 돌파는 피하는 것이 나은가, 아니면 compression breakout으로 봐야 하는가?
- 국내주식 VI 이후 heavy selling flag를 어떤 호가/체결 지표로 정의할 수 있는가?
