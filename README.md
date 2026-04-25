# Hermes Workspace

이 폴더는 포레스트님의 Hermes 봇들이 로컬 산출물을 저장하는 작업 공간입니다.

## 구조

- `personal-assistant/`
  - 개인비서봇의 일반 업무, 메모, 리서치, 보고서 저장 공간
- `investment-lab/`
  - 투자연구소봇의 투자전략 리서치, 전략 메모, 데이터, 보고서 저장 공간
- `shared/`
  - 두 봇이 함께 사용할 템플릿, 공통 자료, 이미지/첨부, 내보내기 파일 저장 공간

## 원칙

- Hermes 내부 상태는 각 프로필 홈에 따로 저장됩니다.
  - 기본 프로필: `/Users/jiuklim/.hermes`
  - 투자연구소봇: `/Users/jiuklim/.hermes/profiles/investmentlab`
- 사람이 직접 열어볼 리서치/메모/보고서 파일은 이 워크스페이스에 저장합니다.
- 투자 관련 산출물은 기본적으로 `investment-lab/`에 저장합니다.
- 여러 봇이 같이 써야 하는 자료는 `shared/`에 저장합니다.
