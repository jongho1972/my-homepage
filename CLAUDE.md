# CLAUDE.md

이 파일은 이 저장소에서 작업하는 Claude Code(claude.ai/code)에게 안내를 제공합니다.

## 프로젝트 개요

이종호(J-Hawk)의 정적 개인 홈페이지입니다. 빌드 시스템·의존성·패키지 매니저 없이 순수 HTML, CSS, 이미지 파일로만 구성되어 있습니다. 외부 폰트 로드 없이 SF 시스템 폰트를 사용합니다.

## 배포

- **저장소**: https://github.com/jongho1972/my-homepage
- **서비스 URL**: https://jhawk.kr
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

- `index.html` — 단일 컬럼 모듈러 카드 페이지 (`.frame` 안에 7개 섹션)
- `index.css` — 모든 스타일 (CSS 변수로 토큰화); 외부 폰트 의존 없음; 프레임워크 없음
- `license.html` — 손해평가사 자격증 이미지 전용 뷰어 페이지 (다크 라이트박스, `max-width: min(380px,86vw)` · `max-height: 78vh`로 모바일 풀스크린 방지, `noindex`, 안전영역·reduced-motion 처리). index.css에 의존하지 않는 인라인 스타일 단일 파일
- `jh.jpg` — 프로필 사진(파비콘 폴백)
- `favicon.svg` — 기본 파비콘
- `QRCode_Homepage.png` — 홈페이지 URL QR 코드
- `transcript-skku-bachelor.pdf` / `transcript-skku-master.pdf` — 성균관대 학·석사 성적증명서. 생년월일·문서확인번호는 PyMuPDF redaction으로 블라인드(텍스트 레이어까지 제거). 한글 파일명 회피용 ASCII 슬러그
- `license-adjuster.jpg` — 손해평가사 자격증 이미지 (원본 1462×2295/774KB → 800×1256/88KB 리사이즈, progressive JPEG)
- `design_handoff_jhawk_homepage/` — 리디자인 핸드오프 자료 (로컬 참고용, gitignore)
- `README.md` — 프로젝트 소개 (GitHub 표시용)
- `.gitignore` — `preview_macos.html` · `.DS_Store` · `.claude/` · `design_handoff_jhawk_homepage/`

`.frame` 내부 섹션 순서 (위에서 아래):

1. **Header** (`.page-header`) — 좌: `JH` 로고 박스 + `J-HAWK` 모노 라벨 / 우: `Seoul, KR`
2. **Hero** (`.card.card-dark.hero`) — H1 `이종호 / J-Hawk`(`.accent`만 블루) + 우측에 한 줄 소개(`"GD는 G-Dragon, JH는 J-Hawk"`) flex baseline 정렬 + 알약 버튼 2개 (콘텐츠 폭, 이메일 주소가 잘리지 않게 표시)
   - Instagram: `https://www.instagram.com/jongho1972/?hl=ko` (Instagram 옐로→핑크→퍼플 그라데이션)
   - 이메일: `mailto:jongho1972@gmail.com` (흰 배경 + Gmail 멀티컬러 봉투 SVG)
3. **Projects** (`§ 01 — Projects / 여섯 개의 작은 도구`) — 6개 카드 행 (`.project-row`): 이모지 박스 + 인덱스/태그 + 타이틀 + 부제 + chevron. 모두 현재 탭에서 열림.
   - 활성 4개(MONEY·LOTTERY·FORTUNE·MUSIC)에 `.project-row-live` 클래스: 타이틀 옆 라이브 점(`.proj-live`, 펄스 애니메이션) + 액센트 블루 chevron + 데스크탑 호버 시 `OPEN` 슬라이드인(`.proj-cta`). 모바일은 라이브 점·블루 chevron만 노출(호버 없음).
   - 비공개 2개(WORK·동유럽 TRAVEL)는 라이브 점 없음, muted chevron 유지.
   - `https://etf.jhawk.kr` — ETF 투자 가이드 · GUIDE
   - `https://lottery.jhawk.kr/` — 통계 기반 복권번호 생성기 · TOOL
   - `https://fortune.jhawk.kr/` — AI 사주팔자 · AI
   - `https://sonkum.jhawk.kr/` — AI 손금풀이 · PALMISTRY (NEW 리본)
   - `https://edm-jahwk.netlify.app` — EDM DJ Console · PLAY
   - `https://tour-jeolla-jhawk.netlify.app` — 호남 서남해안 여행 추천 코스 · TRAVEL (공개·라이브, 일반 추천 코스로 전환)
   - `https://tour-europe-jhawk.netlify.app` — 동유럽 여행 코스 🔒 · FAMILY (자체 비번 게이트 `0000`)
   - `https://shilla-jhawk.netlify.app/` — I'M PROJECT 🔒 · WORK (랜딩은 공개, 하위 페이지는 자체 비번 게이트)
   - 비공개 표기는 타이틀 옆 작은 🔒 (`.proj-lock`)
   - 프로젝트 이모지(`.proj-icon`)는 `aria-hidden="true"` (스크린리더 중복 방지)
4. **History** (`§ 02 — History / 거쳐온 길`) — `.timeline-card` 인라인 타임라인 7개 (성균관대 학·석사 + 5개 회사). 마지막 항목 `.t-row-current`만 점이 액센트 블루
   - LG유플러스 · 호텔신라는 `.t-role-list`로 부서 다중 표기 (모노 미들닷 prefix)
   - 학·석사 행의 `사회학과 (학사)`/`(석사)`는 `.t-role-doc` 클래스로 각 성적증명서 PDF에 새 탭 링크 (액센트 블루 밑줄, `.t-thesis a`와 동일 톤)
5. **Certifications** (`§ 03 — Certifications / 국가전문자격증`) — `.timeline-card` 재활용. 손해평가사(자격증번호 2207226, 2022-11-23) 1행. 자격증명은 `.t-org-link` 클래스로 Q-Net 상세 페이지 새 탭 링크. 자격증번호(`2207226`)는 `.t-role-doc` 클래스로 자격증 이미지 뷰어(`license.html`) 새 탭 링크. 점은 액센트 블루(`.t-row-current`). ⚠️ 실물 카드 인쇄번호(`제 22-0726호`)와 표기 텍스트(`2207226`)가 다름 — 정정 여부 미확정
6. **Favorites** (`§ 04 — Favorites / 좋아하는 노래`) — 한로로 3곡 YouTube 링크 (`그건 니 생각이고` / `거절할 거야` / `할건지말건지`). 곡 타이틀 옆 YouTube 레드 점(`.song-live`, 펄스 애니메이션) + 우측에 `▶ YOUTUBE` 라벨(`.song-source`, 모노 10px 빨강). 모바일(`max-width: 600px`)에서는 라벨이 빨간 알약 버튼으로 변환되어 탭 어포던스 강화. 모든 노래 링크는 `target="_blank" rel="noopener noreferrer"`로 새 탭에서 열림 (홈페이지 이탈 방지).
7. **Colophon** (`.card.card-dark.colophon`) — `이 페이지는 Claude Code와 함께 만들었습니다.` + 푸터 (좌: `269 visitors` / 우: `v.YYYY.MM`)
   - 버전 라벨(`#version`)은 하드코딩이 아니라 인라인 JS가 방문 시점의 `new Date()`로 `v.YYYY.MM`을 주입(현재 월 자동 갱신). HTML의 값은 JS 미동작 시 폴백일 뿐이므로 수동 갱신 불필요.

## 방문자 카운터

- GoatCounter 트래킹: `https://jongho1972.goatcounter.com`
- 카운트 표시: `fetch('https://jongho1972.goatcounter.com/counter/%2F.json')` → Colophon 푸터의 `#visitor-count`에 `toLocaleString()`로 주입
- GoatCounter Settings → "Allow adding visitor counts on your website" 체크 필요 (CORS 허용). 로컬에서는 `localhost @` 경고로 카운트되지 않는 게 정상.

## 변경 시 주의

- 데스크탑/모바일 양쪽 폭에서 깨짐 없이 동작해야 함 (단일 브레이크포인트 `max-width: 600px`만 사용)
- 외부 프로젝트의 추가/제거가 발생하면 워크스페이스 루트 `CLAUDE.md` 표와 동기화 (홈페이지 동기화 원칙)
- 새 콘텐츠 추가 시에도 `--accent`는 강조 1~2곳에만 절제 사용. 다른 컬러로 흩뜨리지 말 것.
- CSS 수정 시 `index.html`의 `<link href="index.css?v=...">` 캐시 버스트 쿼리도 함께 올릴 것.
- 같은 파일명으로 PDF·이미지 자산을 교체하면 CDN/브라우저 캐시가 옛 버전을 줄 수 있음 → 링크 `href`에 `?v=YYYYMMDD` 캐시버스트를 붙여 교체 보장.
- 증명서·자격증 등 개인정보 문서를 공개 게시할 때: 단순 검은 박스가 아니라 PyMuPDF redaction(텍스트 레이어 제거)으로 블라인드. 전자증명서의 **문서확인번호**는 발급기관 검증 사이트(icert.skku.edu 등)에서 원본 조회가 가능해 다른 블라인드를 무력화하므로 함께 가릴 것.
