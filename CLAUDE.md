# CLAUDE.md

이 파일은 이 저장소에서 작업하는 Claude Code(claude.ai/code)에게 안내를 제공합니다.

## 프로젝트 개요

이종호(J-Hawk)의 정적 개인 홈페이지입니다. 빌드 시스템·의존성·패키지 매니저 없이 순수 HTML, CSS, 이미지 파일로만 구성되어 있습니다. 외부 폰트 로드 없이 SF 시스템 폰트를 사용합니다.

## 배포

- **저장소**: https://github.com/jongho1972/my-homepage
- **서비스 URL**: https://jhawk.kr
- **실서빙**: j-hawk VPS Caddy가 `/srv/homepage`(= `deploy/docker-compose.yml`에서 `../my-homepage` git clone을 read-only 마운트)를 `file_server`로 직접 서빙
- **배포 절차**: my-homepage `main` 푸시 → **VPS `/opt/j-hawk/my-homepage`에서 `git pull`**(또는 `git reset --hard origin/main`). 빌드·컨테이너 재시작 불필요, 파일 교체 즉시 반영
- Netlify `j-hawk` 사이트(`j-hawk.netlify.app`)는 jhawk.kr로 **301 리디렉트만** 하는 스텁 — 실제 서빙 아님. Netlify 배포만으론 jhawk.kr이 갱신되지 않으니 주의

## 개발 방법

`index.html`을 브라우저에서 직접 열거나, 아래 명령으로 로컬 서버를 실행합니다:

```bash
python3 -m http.server 8000
```

## 디자인

2026-10-30 Apple 디자인 가이드(`../Design_MD/DESIGN-apple.md`) 기준으로 다듬음 (A안). 이전 macOS 톤(모노 10px 라벨·카드 그림자·브랜드 그라데이션)에서 전환.

- 단일 컬럼 (max-width 560px frame, 좌우 1px 헤어라인, 모바일에서는 풀폭)
- 핵심 토큰: `--bg #f5f5f7` / `--surface #fff` / `--ink #1d1d1f` / `--tile #272729`(히어로) / `--accent #0066cc` / `--accent-on-dark #2997ff`(다크 위 링크) / `--focus #0071e3`(포커스 링) / `--muted #7a7a7a` / `--rule #e0e0e0`
- 타이포: 본문 17px·line-height 1.47·letter-spacing -0.374px, 제목 굵기 600(히어로 40px · 섹션 28px), 캡션 14px, 보조 라벨 12px. 모노 서체·10px 글씨 사용 안 함
- 카드: 1px 헤어라인 + radius 18, **그림자 없음**. 알약 999
- 강조색은 파랑 하나만. Instagram 그라데이션·YouTube 빨강 같은 브랜드 색 쓰지 않음
- 다크는 Hero 카드 한 곳만. Colophon은 밝은 푸터(상단 헤어라인)
- 인터랙션: 누를 때 `scale(0.95)`(알약) / `scale(0.98)`(프로젝트 행). hover로 떠오르는 효과 없음. 데스크탑 hover 시 `OPEN` 슬라이드인만 유지
- 모션 접근성: `@media (prefers-reduced-motion: reduce)`에서 transition/transform 비활성화
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

1. **Header** (`.page-header`) — 좌: `JH` 로고 박스 + `J-HAWK` 라벨 / 우: `Seoul, KR`
2. **Hero** (`.card.card-dark.hero`) — H1 `이종호 / J-Hawk`(`.accent`만 블루) + 우측에 한 줄 소개(`"GD는 G-Dragon, JH는 J-Hawk"`) flex baseline 정렬 + 알약 버튼 2개 (콘텐츠 폭, 이메일 주소가 잘리지 않게 표시)
   - 이메일(1번째): `mailto:jongho1972@gmail.com` (`.pill-primary` 파란 알약 + 단색 봉투 아이콘)
   - Instagram(2번째): `https://www.instagram.com/jongho1972/?hl=ko` (`.pill-ghost` 테두리 알약, `#2997ff`)
3. **Projects** (`프로젝트 / Claude Code로 만든 서비스`) — 9개 카드 행 (`.project-row`): 이모지 박스 + 인덱스/태그 + 타이틀 + 부제 + chevron. 모두 현재 탭에서 열림.
   - 9개 모두 `.project-row-live` 클래스: 타이틀 옆 라이브 점(`.proj-live`, 정지된 파란 점) + 액센트 블루 chevron + 데스크탑 호버 시 `OPEN` 슬라이드인(`.proj-cta`). 모바일은 라이브 점·블루 chevron만 노출(호버 없음).
   - 비공개 항목을 추가할 때는 `.project-row-live`를 빼면 라이브 점 없이 muted chevron으로 표시됨.
   - `https://etf.jhawk.kr` — ETF 투자 가이드 · GUIDE
   - `https://lottery.jhawk.kr/` — 통계 기반 복권번호 생성기 · TOOL
   - `https://fortune.jhawk.kr/` — AI 사주팔자 · AI
   - `https://sonkum.jhawk.kr/` — AI 손금풀이 · PALMISTRY
   - `https://edm-jahwk.netlify.app` — EDM DJ Console · PLAY
   - `https://tour-jeolla-jhawk.netlify.app` — 호남 서남해안 여행 추천 코스 · TRAVEL (공개·라이브, 일반 추천 코스로 전환)
   - `https://tour-europe-jhawk.netlify.app` — 동유럽 여행 코스 · TRAVEL (공개·라이브, 일반 추천 코스로 전환 / 실제 여행 일정은 보류)
   - `https://opendata-jhawk.netlify.app/` — 공개 데이터 활용 사례 · DATA (공개·라이브, 02번 위치. 인천공항·관광·면세 공개 데이터 대시보드)
   - 비공개 표기는 타이틀 옆 작은 🔒 (`.proj-lock`)
   - 프로젝트 이모지(`.proj-icon`)는 `aria-hidden="true"` (스크린리더 중복 방지)
4. **History** (`이력 / 거쳐온 길`) — `.timeline-card` 인라인 타임라인 7개 (성균관대 학·석사 + 5개 회사). 마지막 항목 `.t-row-current`만 점이 액센트 블루
   - LG유플러스 · 호텔신라는 `.t-role-list`로 부서 다중 표기 (미들닷 prefix)
   - 학·석사 행의 `사회학과 (학사)`/`(석사)`는 `.t-role-doc` 클래스로 각 성적증명서 PDF에 새 탭 링크 (액센트 블루, 밑줄은 데스크탑 hover 시에만. `.t-thesis a`와 동일 톤)
5. **Certifications** (`자격 / 국가전문자격증`) — `.timeline-card` 재활용. 손해평가사(자격증번호 2207226, 2022-11-23) 1행. 자격증명은 `.t-org-link` 클래스로 Q-Net 상세 페이지 새 탭 링크. 자격증번호(`2207226`)는 `.t-role-doc` 클래스로 자격증 이미지 뷰어(`license.html`) 새 탭 링크. 점은 액센트 블루(`.t-row-current`). ⚠️ 실물 카드 인쇄번호(`제 22-0726호`)와 표기 텍스트(`2207226`)가 다름 — 정정 여부 미확정
6. **Favorites** (`즐겨 듣는 곡 / 좋아하는 노래`) — 한로로 3곡 YouTube 링크 (`그건 니 생각이고` / `거절할 거야` / `할건지말건지`). 우측에 `YouTube에서 듣기 ›` 텍스트 링크(`.song-source`, 14px 액센트 블루). 빨간 점·빨간 알약은 2026-10 제거.
7. **Colophon** (`footer.colophon`, 밝은 푸터) — `이 페이지는 Claude Code와 함께 만들었습니다.` + 푸터 (좌: `N visitors` / 우: `v.YYYY.MM`)
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
