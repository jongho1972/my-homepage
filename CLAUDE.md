# CLAUDE.md

이 파일은 이 저장소에서 작업하는 Claude Code(claude.ai/code)에게 안내를 제공합니다.

## 프로젝트 개요

이종호(J-Hawk)의 정적 개인 홈페이지입니다. 빌드 시스템·의존성·패키지 매니저 없이 순수 HTML, CSS, 이미지 파일로만 구성되어 있습니다. 외부 폰트 로드 없이 SF 시스템 폰트를 사용합니다.

## 배포

- **저장소**: https://github.com/jongho1972/my-homepage
- **서비스 URL**: https://j-hawk.netlify.app
- GitHub `main` 브랜치 푸시 시 Netlify 자동 배포

## 개발 방법

`index.html`을 브라우저에서 직접 열거나, 아래 명령으로 로컬 서버를 실행합니다:

```bash
python3 -m http.server 8000
```

## 디자인

- 단일 컬럼 macOS 톤 (max-width 560px frame, 좌우 미세 그림자, 모바일에서는 풀폭)
- 핵심 토큰: `--bg #f5f5f7` / `--surface #fff` / `--ink #1d1d1f` / `--accent #0071e3` (Apple 블루)
- 카드 radius 16, 알약 999, 그림자는 절제 (`0 1px 2px rgba(0,0,0,.04)`)
- Eyebrow: 모노 10–11px / letter-spacing 0.14em / uppercase / muted
- Hero / Colophon 두 카드만 다크 (`--ink` 배경)
- 인터랙션은 0.18s ease로 통일, 프로젝트 카드만 hover 시 살짝 떠오름 (`translateY(-2px)`)
- 모션 접근성: `@media (prefers-reduced-motion: reduce)`에서 모든 transition/transform 비활성화
- 모바일 UX: `.pill / .project-row / .song-row`에 `touch-action: manipulation` (더블탭 줌 지연 제거)
- 디자인 레퍼런스 원본은 `design_handoff_jhawk_homepage/` (gitignore, 로컬 보관)

## 구조

파일 구성:

- `index.html` — 단일 컬럼 모듈러 카드 페이지 (`.frame` 안에 6개 섹션)
- `index.css` — 모든 스타일 (CSS 변수로 토큰화); 외부 폰트 의존 없음; 프레임워크 없음
- `jh.jpg` — 프로필 사진(파비콘 폴백)
- `favicon.svg` — 기본 파비콘
- `QRCode_Homepage.png` — 홈페이지 URL QR 코드
- `design_handoff_jhawk_homepage/` — 리디자인 핸드오프 자료 (로컬 참고용, gitignore)
- `README.md` — 프로젝트 소개 (GitHub 표시용)
- `.gitignore` — `preview_macos.html` · `.DS_Store` · `.claude/` · `design_handoff_jhawk_homepage/`

`.frame` 내부 섹션 순서 (위에서 아래):

1. **Header** (`.page-header`) — 좌: `JH` 로고 박스 + `J-HAWK` 모노 라벨 / 우: `Seoul, KR`
2. **Hero** (`.card.card-dark.hero`) — Eyebrow `Hello — 안녕하세요` + H1 `이종호 / J-Hawk`(`.accent`만 블루) + 우측에 한 줄 소개(`"GD는 G-Dragon, JH는 J-Hawk"`) flex baseline 정렬 + 알약 버튼 2개 (콘텐츠 폭, 이메일 주소가 잘리지 않게 표시)
   - 이메일: `mailto:jongho1972@gmail.com` (흰 배경 + Gmail 멀티컬러 봉투 SVG)
   - Instagram: `https://www.instagram.com/jongho1972/?hl=ko` (Instagram 옐로→핑크→퍼플 그라데이션)
3. **Projects** (`§ 01 — Projects / 여섯 개의 작은 도구`) — 6개 카드 행 (`.project-row`): 이모지 박스 + 인덱스/태그 + 타이틀 + 부제 + chevron. 모두 현재 탭에서 열림.
   - `https://jhawk-etf-dashboard.streamlit.app` — ETF 투자 대시보드 · DASHBOARD
   - `https://lottery-number-generator.onrender.com/` — 통계 기반 복권번호 생성기 · TOOL
   - `https://saju-fortune.onrender.com/` — AI 사주팔자 · AI
   - `https://jhawk-edm-dj.netlify.app` — EDM DJ Console · PLAY
   - `https://shilla-icn-mkt.netlify.app/` — I'M PROJECT 🔒 · WORK (랜딩은 공개, 하위 페이지는 자체 비번 게이트)
   - `https://jhawk-east-europe-tour.netlify.app` — 동유럽 여행 코스 🔒 · FAMILY (목적지 페이지에 자체 비번 게이트 `0000`)
   - 비공개 표기는 타이틀 옆 작은 🔒 (`.proj-lock`)
   - 프로젝트 이모지(`.proj-icon`)는 `aria-hidden="true"` (스크린리더 중복 방지)
4. **History** (`§ 02 — History / 거쳐온 길`) — `.timeline-card` 인라인 타임라인 7개 (성균관대 학·석사 + 5개 회사). 마지막 항목 `.t-row-current`만 점이 액센트 블루
   - LG유플러스 · 호텔신라는 `.t-role-list`로 부서 다중 표기 (모노 미들닷 prefix)
5. **Favorites** (`§ 03 — Favorites / 좋아하는 노래`) — 한로로 3곡 YouTube 링크 (`그건 니 생각이고` / `거절할 거야` / `할건지말건지`)
6. **Colophon** (`.card.card-dark.colophon`) — `이 페이지는 Claude Code와 함께 만들었습니다.` + 푸터 (좌: `269 visitors` / 우: `v.YYYY.MM`)

## 방문자 카운터

- GoatCounter 트래킹: `https://jongho1972.goatcounter.com`
- 카운트 표시: `fetch('https://jongho1972.goatcounter.com/counter/%2F.json')` → Colophon 푸터의 `#visitor-count`에 `toLocaleString()`로 주입
- GoatCounter Settings → "Allow adding visitor counts on your website" 체크 필요 (CORS 허용). 로컬에서는 `localhost @` 경고로 카운트되지 않는 게 정상.

## 변경 시 주의

- 데스크탑/모바일 양쪽 폭에서 깨짐 없이 동작해야 함 (단일 브레이크포인트 `max-width: 600px`만 사용)
- 외부 프로젝트의 추가/제거가 발생하면 워크스페이스 루트 `CLAUDE.md` 표와 동기화 (홈페이지 동기화 원칙)
- 새 콘텐츠 추가 시에도 `--accent`는 강조 1~2곳에만 절제 사용. 다른 컬러로 흩뜨리지 말 것.
- CSS 수정 시 `index.html`의 `<link href="index.css?v=...">` 캐시 버스트 쿼리도 함께 올릴 것.
