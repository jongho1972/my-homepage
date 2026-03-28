# CLAUDE.md

이 파일은 이 저장소에서 작업하는 Claude Code(claude.ai/code)에게 안내를 제공합니다.

## 프로젝트 개요

이종호(J.Hawk)의 정적 개인 홈페이지입니다. 빌드 시스템, 의존성, 패키지 매니저 없이 순수 HTML, CSS, 이미지 파일로만 구성되어 있습니다.

## 개발 방법

`index.html`을 브라우저에서 직접 열거나, 아래 명령으로 로컬 서버를 실행합니다:

```bash
python3 -m http.server 8000
```

## 구조

파일 3개로 구성:

- `index.html` — 단일 섹션: 전체 뷰포트 프로필 카드(`.container`)
- `index.css` — 모든 스타일; Google Fonts(JetBrains Mono) 사용; 프레임워크 없음
- `jh.jpg` — 프로필 사진, 파비콘으로도 사용

프로필 섹션 구성 (위에서 아래 순서):
- 프로필 사진 (`.profile_pic`)
- 이름: Jongho Lee, 닉네임: [J-Hawk]
- 이메일 링크: jongho1972@gmail.com
- 외부 프로젝트 버튼 3개 (iframe 없이 외부 링크만):
  - `https://jhawk-etf-dashboard.streamlit.app` — ETF 투자 대시보드
  - `https://lottery-number-generator.onrender.com/` — 통계 기반 복권번호 생성기 (로또 · 연금복권)
  - `https://east-europe-tour.netlify.app` — 동유럽 여행 코스 (비밀번호 보호: 클릭 시 비밀번호 입력 필요, 틀리면 "죄송합니다. 접속이 제한되는 페이지입니다." 안내)
- 바로가기 아이콘 (`.shortcuts`):
  - Instagram: `https://www.instagram.com/jongho1972/?hl=ko`
