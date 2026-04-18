# CLAUDE.md

이 파일은 이 저장소에서 작업하는 Claude Code(claude.ai/code)에게 안내를 제공합니다.

## 프로젝트 개요

이종호(J.Hawk)의 정적 개인 홈페이지입니다. 빌드 시스템, 의존성, 패키지 매니저 없이 순수 HTML, CSS, 이미지 파일로만 구성되어 있습니다.

## 배포

- **저장소**: https://github.com/jongho1972/my-homepage
- **서비스 URL**: https://j-hawk.netlify.app
- GitHub `main` 브랜치 푸시 시 Netlify 자동 배포

## 개발 방법

`index.html`을 브라우저에서 직접 열거나, 아래 명령으로 로컬 서버를 실행합니다:

```bash
python3 -m http.server 8000
```

## 구조

파일 구성:

- `index.html` — 단일 섹션: 전체 뷰포트 프로필 카드(`.container`)
- `index.css` — 모든 스타일; Google Fonts(JetBrains Mono) 사용; 프레임워크 없음
- `jh.jpg` — 프로필 사진, 파비콘으로도 사용
- `README.md` — 프로젝트 소개 (GitHub 표시용)
- `.gitignore` — `preview_macos.html` 제외

프로필 섹션 구성 (위에서 아래 순서):
- 프로필 사진 (`.profile_pic`)
- 이름: Jongho Lee, 닉네임: [J-Hawk]
- 이메일 링크: jongho1972@gmail.com
- 외부 프로젝트 버튼 (모두 현재 창에서 열림, `target="_blank"` 없음):
  - `https://jhawk-etf-dashboard.streamlit.app` — ETF 투자 대시보드
  - `https://lottery-number-generator.onrender.com/` — 통계 기반 복권번호 생성기 (로또 · 연금복권)
  - `https://saju-fortune.onrender.com/` — AI 사주팔자 (생년월일시로 보는 나의 사주)
  - `https://strudel-creator.netlify.app/` — Music Creator (DJ Top 10 · AI 생성 · 라이브 DJ 컨트롤)
  - `https://jeonju-tour.netlify.app` — 5월 전주 여행 코스 [가족 Only] (비밀번호 보호, `data-password="0000"`)
  - `https://east-europe-tour.netlify.app` — 동유럽 여행 코스 [가족 Only / On Hold] (목적지 페이지에 오버레이 비밀번호 게이트 `0000`)
  - `https://shilla-icn-mkt.netlify.app` — **I'm project** (신라면세점) — `is-disabled` 클래스로 외형만 비활성(흐림 처리), 클릭은 정상 동작 — **항상 맨 아래에 배치**
- 비밀번호 보호: `checkPassword(event, el)` 공용 함수가 `el.dataset.password`와 비교. 클릭 시 "비밀번호를 입력해 주세요" 프롬프트 → 일치 시 이동, 불일치 시 "죄송합니다. 접속이 제한되는 페이지입니다." 안내.
- Personal History 모달: 이메일 아래 `.career-link` 버튼 → `#careerModal` 팝업. 학력(성균관대 학사/석사) + 경력(현대리서치~호텔신라) 타임라인 표시. `openCareer()`/`closeCareer()` 함수, ESC·배경 클릭·X 버튼으로 닫힘.
- 바로가기 아이콘 (`.shortcuts`):
  - Instagram: `https://www.instagram.com/jongho1972/?hl=ko`
- 방문자 카운터 (`.visitor-counter`):
  - GoatCounter 트래킹: `https://jongho1972.goatcounter.com`
  - 카운터 표시: `fetch('https://jongho1972.goatcounter.com/counter/%2F.json')` → `d.count` 표시
  - GoatCounter Settings에서 "Allow adding visitor counts on your website" 체크 필요 (CORS 허용)
