# CLAUDE.md

이 파일은 이 저장소에서 작업하는 Claude Code(claude.ai/code)에게 안내를 제공합니다.

## 프로젝트 개요

이종호(J-Hawk)의 정적 개인 홈페이지입니다. 빌드 시스템·의존성·패키지 매니저 없이 순수 HTML, CSS, 이미지 파일로만 구성되어 있습니다. 폰트는 프리텐다드(Pretendard)이며 jsDelivr CDN에서 불러옵니다. 불러오지 못하면 기기 폰트로 표시됩니다.

## 배포

- **저장소**: https://github.com/jongho1972/my-homepage
- **서비스 URL**: https://jhawk.kr
- **실서빙**: j-hawk VPS Caddy가 `/srv/homepage`(= `공용/deploy/docker-compose.yml`에서 `../my-homepage` git clone을 read-only 마운트)를 `file_server`로 직접 서빙
- **배포 절차**: my-homepage `main` 푸시 → **VPS `/opt/j-hawk/my-homepage`에서 `git pull`**(또는 `git reset --hard origin/main`). 빌드·컨테이너 재시작 불필요, 파일 교체 즉시 반영
- Netlify `j-hawk` 사이트(`j-hawk.netlify.app`)는 jhawk.kr로 **301 리디렉트만** 하는 스텁 — 실제 서빙 아님. Netlify 배포만으론 jhawk.kr이 갱신되지 않으니 주의

## 개발 방법

`index.html`을 브라우저에서 직접 열거나, 아래 명령으로 로컬 서버를 실행합니다:

```bash
python3 -m http.server 8000
```

## 디자인

2026-10-31 **다크 고정** 톤으로 전환 (전문가 톤앤매너 목적, Linear 계열 차분한 다크). 레이아웃·타이포 골격은 2026-10-30 Apple 가이드(`../Design_MD/DESIGN-apple.md`) A안을 유지. 라이트 모드·자동 전환 없음.

- 단일 컬럼 (max-width 560px frame, 좌우 1px 헤어라인, 모바일에서는 풀폭)
- 핵심 토큰: `--frame-outer #050607` / `--bg #0b0c0e` / `--surface #15171a` / `--ink #f2f3f5`(순백 금지 — OLED 번짐) / `--ink-80 #c9ccd2` / `--muted #8f949c` / `--accent #3d9bff` / `--accent-fill #0a6fe0`(이메일 알약 시작색) / 분야 색 `--tone-data #7cbdff`·`--tone-luck #bda8fc`·`--tone-travel #44d0c1`·`--tone-music #f197c2`·`--tone-gold #e8b762` / `--brand`(블루→청록 글자 그라데이션) / `--focus #5aa9ff` / `--rule #24272d` / `--live #3ecf8e`(라이브 점) / `--alert #ff6b6b`. 텍스트 대비는 전부 WCAG AA 이상(muted 5.89~6.41, accent 6.27, 분야 색 8.5 이상, 알약 흰 글자 4.81)
- `<meta name="color-scheme" content="dark">` · `theme-color #0b0c0e` (iOS 상단바·스크롤바 다크)
- 타이포: 본문 17px·line-height 1.47·letter-spacing -0.374px, 제목 굵기 600(히어로 46px · 섹션 28px), 캡션 14px. 작은 메타 라벨(`.proj-meta / .t-range / .colophon-foot / 헤더 Seoul, KR`)은 11px·500·대문자·자간 0.08em·tabular-nums로 통일. 모노 서체·10px 글씨 사용 안 함
- 카드: 1px 헤어라인 + radius 18, 그림자 없음. 알약 999
- 색(2026-11-25 사용자 결정, "색상 제한 없이 세련되게" → 전체 적용): **분야 4색(블루·보라·청록·핑크) + 자격증 골드**를 페이지 공통으로 사용. 요소에 `.cat-data / .cat-luck / .cat-travel / .cat-music / .cat-gold`를 붙이면 `--tile-a`·`--tile-b`(타일)·`--tone`(글자·선·점)이 정해짐 — 새 색을 요소마다 따로 만들지 말 것. 제목·본문은 흰색·회색, 이력·자격 글자 링크는 `--accent` 블루 유지. 적용처: 로고·히어로 4색 오로라·`J-Hawk` 그라데이션 / 알약(이메일 블루→남색, Instagram 핑크 테두리) / 프로젝트 카드(아이콘 뒤 번짐·태그 글자·초록 라이브 점·`OPEN`·데스크탑 hover 테두리) / 섹션 라벨(프로젝트 블루·이력 청록·자격 골드·노래 핑크) / 이력 타임라인 / 자격증 골드 타일 / 노래 재생 타일·링크 / 푸터 4색 선·방문자 수. chevron은 회색
- 프로젝트 아이콘(2026-11-25 사용자 결정, 4안 컬러 타일): **Lucide 흰 선 SVG**(stroke 1.6·26px, 인라인 `<svg viewBox="0 0 24 24">`, 선 속성은 `.tile svg`에서 지정) + **분야별 그라데이션 타일**(공용 `.tile` 48px·radius 13, 자격증 `.cert-tile`·노래 `.play-tile` 32px도 사용). 새 카드는 `.cat-*` 하나를 붙일 것(없으면 블루). 흰 아이콘 대비 3.15(골드)~3.95. Lucide 라이선스(ISC) 주석을 `index.html`에 유지. 컬러 이모지 사용 금지
- Hero는 박스 없이 타이포로 위계(하단 헤어라인). Colophon은 상단 4색 선 푸터
- 인터랙션: 누를 때 `scale(0.95)`(알약) / `scale(0.98)`(프로젝트 행). hover로 떠오르는 효과 없음. 데스크탑 hover 시 `OPEN` 슬라이드인만 유지
- 스크롤·진입 모션(2026-11-06, 라이브러리 없음): 첫 화면 순차 등장(CSS만, 0.5초 이내) · 섹션/카드 스크롤 등장(8px, 0.4초, 1회) · 이력 타임라인 색 선(`.timeline-draw::after`, 학업 보라 → 리서치 청록 → LG유플러스 핑크 → 호텔신라 블루)이 스크롤에 따라 드러나고 점이 행의 `.cat-*` 색으로 켜짐(되돌리지 않음). 색 선의 % 지점은 점 위치에 맞춘 값이라 이력 행을 추가·삭제하면 다시 맞출 것. 3D·마우스 추적 기울기·스크롤 가로채기는 넣지 않기로 결정(용량·모바일·톤)
- 모바일 "와우" 보강(2026-11-08): 히어로 뒤 4색 오로라(`.hero::before`, 16초 천천히 흐름) + 아래로 사라지는 점 격자(`.hero::after`) · 진입 직후 `J-Hawk`에 빛이 1회 지나감(`shine`) · 터치 기기(`hover: none`) 프로젝트 카드는 **누르는 동안만** 분야 색(`--tone`) 테두리 + 타일 밝아짐(`:active`, iOS용 `body ontouchstart`), 첫 등장 때 타일만 1회 밝아졌다 복귀(`icon-glow` 1.2초). 스크롤 위치로 카드를 켜던 `.spot`은 산만하고 `OPEN` 때문에 카드 높이가 약 20px 바뀌어 2026-11-25 제거 — 재도입 금지. 오로라 가로 넘침은 `.frame { overflow-x: clip }`로 차단
- 모션 구조: head 인라인 스크립트가 `html.motion`을 붙이고, 그때만 등장 대상을 숨김 → 클래스가 없으면 원래 화면. 등장 대상 목록은 `index.css`와 `index.html` 하단 스크립트 **두 곳**에 있어, 한쪽만 고치면 요소가 숨은 채 남을 수 있음. 모션 CSS는 `@media screen and (prefers-reduced-motion: no-preference)` 블록 안에 둠(인쇄 제외)
- 모션 접근성: `@media (prefers-reduced-motion: reduce)`에서 transition/transform 비활성화, 위 모션도 전부 꺼짐
- 모바일 UX: `.pill / .project-row / .song-row`에 `touch-action: manipulation` (더블탭 줌 지연 제거)
- 모바일 접근성(2026-10-31): `.pill` `min-height: 44px` · 이력 안 글자 링크(`.t-role-doc / .t-role-link / .t-thesis a`)는 `padding-block: 12px`로 터치 영역만 확장(레이아웃 불변) + 위아래 링크 사이 간격(`:has`)으로 겹침 방지 · 전역 `word-break: keep-all`
- 디자인 레퍼런스 원본은 `design_handoff_jhawk_homepage/` (gitignore, 로컬 보관)

## 구조

파일 구성:

- `index.html` — 단일 컬럼 모듈러 카드 페이지 (`.frame` 안에 7개 섹션)
- `index.css` — 모든 스타일 (CSS 변수로 토큰화); 폰트는 프리텐다드(`--font-sans`, CDN 로드는 HTML `<link>`); 프레임워크 없음
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

1. **Header** (`.page-header`) — 좌: `JH` 로고 박스(블루→청록) + `J-HAWK` 라벨 / 우: `Seoul, KR`
2. **Hero** (`section.hero`, 카드 박스 없음) — H1 `이종호 / J-Hawk`(`.accent`만 블루→청록 그라데이션) + 그 아래 줄에 회색 한 줄 소개(`"GD는 G-Dragon, JH는 J-Hawk"`) + 알약 버튼 2개 (콘텐츠 폭, 이메일 주소가 잘리지 않게 표시)
   - 이메일(1번째): `mailto:jongho1972@gmail.com` (`.pill-primary` 블루→남색 알약 + 단색 봉투 아이콘)
   - Instagram(2번째): `https://www.instagram.com/jongho1972/?hl=ko` (`.pill-ghost` 핑크 테두리 알약)
3. **Projects** (`프로젝트 / Claude Code로 만든 서비스`) — 10개 카드 행 (`.project-row`): 컬러 아이콘 타일 + 인덱스/태그 + 타이틀 + 부제 + chevron. 모두 현재 탭에서 열림.
   - 아이콘: (Lucide) ETF=`chart-spline`, 공개데이터=`chart-no-axes-combined`, 복권=`dices`, 사주=`moon-star`, 손금=`hand`, KTX 뚜벅이=`train-front`, 호남=`bridge`, 마쓰야마=`castle`, 동유럽=`church`, EDM=`disc-3`
   - 여행 카드 순서: **KTX 뚜벅이 여행지를 여행 카드 맨 위**(2026-11-24 사용자 지시) → 그다음 **국내 먼저, 해외 다음**(2026-11-24 사용자 지시로 변경, 이전 2026-11-23엔 해외 먼저), 묶음 안에서는 최근 것 먼저 — 06 KTX 뚜벅이 · 07 호남 · 08 마쓰야마 · 09 동유럽. EDM(MUSIC) 카드는 맨 마지막(10번, 2026-11-25 사용자 지시). 전주·강릉은 2026-11-24 지시로 홈페이지에서 내리고 KTX 뚜벅이 여행지의 해당 카드에서 연결. 새 여행 코스 카드는 해당 묶음(국내/해외) 맨 앞에 넣고 번호 재정렬
   - 10개 모두 `.project-row-live` 클래스: 타이틀 옆 라이브 점(`.proj-live`, 초록 `--live`) + 회색 chevron + 데스크탑 호버 시 `OPEN` 슬라이드인(`.proj-cta`, 분야 색). 모바일은 라이브 점·chevron만 노출(호버 없음).
   - 비공개 항목을 추가할 때는 `.project-row-live`를 빼면 라이브 점 없이 표시됨.
   - `https://etf.jhawk.kr` — ETF 투자 가이드 · GUIDE
   - `https://lottery.jhawk.kr/` — 통계 기반 복권번호 생성기 · TOOL
   - `https://fortune.jhawk.kr/` — AI 사주팔자 · AI
   - `https://sonkum.jhawk.kr/` — AI 손금풀이 · PALMISTRY
   - `https://edm-jahwk.netlify.app` — EDM DJ Console · MUSIC (10번, 맨 마지막)
   - `https://tour-matsuyama-jhawk.netlify.app` — 일본 마쓰야마 여행 추천 코스 · TRAVEL (08번, 링크 공개·noindex)
   - `https://tour-ktx-jhawk.netlify.app` — KTX 뚜벅이 여행지 · TRAVEL (06번, 여행 카드 맨 위, 2026-11-24 추가. 공개·라이브, 자차 없이 가는 서울 출발 36곳 비교 페이지)
   - `https://tour-jeolla-jhawk.netlify.app` — 호남 서남해안 여행 추천 코스 · TRAVEL (공개·라이브, 일반 추천 코스로 전환)
   - `https://tour-europe-jhawk.netlify.app` — 동유럽 여행 코스 · TRAVEL (공개·라이브, 일반 추천 코스로 전환 / 실제 여행 일정은 보류)
   - `https://opendata-jhawk.netlify.app/` — 공개 데이터 활용 사례 · DATA (공개·라이브, 02번 위치. 인천공항·관광·면세 공개 데이터 대시보드)
   - 비공개 표기는 타이틀 옆 작은 🔒 (`.proj-lock`)
   - 프로젝트 아이콘(`.proj-icon`)은 `aria-hidden="true"` (스크린리더 중복 방지)
4. **History** (`이력 / 거쳐온 길`) — `.timeline-card` 인라인 타임라인 7개 (성균관대 학·석사 + 5개 회사). 행마다 `.cat-*`로 단계 색, 마지막 항목 `.t-row-current`는 기간 글자도 분야 색
   - LG유플러스 · 호텔신라는 `.t-role-list`로 부서 다중 표기 (미들닷 prefix)
   - 학·석사 행의 `사회학과 (학사)`/`(석사)`는 `.t-role-doc` 클래스로 각 성적증명서 PDF에 새 탭 링크 (액센트 블루, 밑줄은 데스크탑 hover 시에만. `.t-thesis a`와 동일 톤)
5. **Certifications** (`자격 / 국가전문자격증`) — `.timeline-card` + `.cert-list`(타임라인 선 없이 골드 `.cert-tile`). 손해평가사(자격증번호 22-0726, 2022-11-23) 1행. 자격증명은 `.t-org-link` 클래스로 Q-Net 상세 페이지 새 탭 링크. 자격증번호(`22-0726`, 실물 카드 `제 22-0726호` 기준 — 2026-11-18 정정)는 `.t-role-doc` 클래스로 자격증 이미지 뷰어(`license.html`) 새 탭 링크.
6. **Favorites** (`즐겨 듣는 곡 / 좋아하는 노래`) — 한로로 3곡 YouTube 링크 (`그건 니 생각이고` / `거절할 거야` / `할건지말건지`). 왼쪽 핑크 재생 타일(`.play-tile`) + 우측 `YouTube에서 듣기 ›` 텍스트 링크(`.song-source`, 14px 핑크). 빨간 점·빨간 알약은 2026-10 제거.
7. **Colophon** (`footer.colophon`) — `이 페이지는 Claude Code와 함께 만들었습니다.` + 푸터 (좌: `N visitors` / 우: `v.YYYY.MM`)
   - 버전 라벨(`#version`)은 하드코딩이 아니라 인라인 JS가 방문 시점의 `new Date()`로 `v.YYYY.MM`을 주입(현재 월 자동 갱신). HTML의 값은 JS 미동작 시 폴백일 뿐이므로 수동 갱신 불필요.

## 방문자 카운터

- GoatCounter 트래킹: `https://jongho1972.goatcounter.com`
- 카운트 표시: `fetch('https://jongho1972.goatcounter.com/counter/%2F.json')` → Colophon 푸터의 `#visitor-count`에 `toLocaleString()`로 주입
- GoatCounter Settings → "Allow adding visitor counts on your website" 체크 필요 (CORS 허용). 로컬에서는 `localhost @` 경고로 카운트되지 않는 게 정상.

## 변경 시 주의

- 데스크탑/모바일 양쪽 폭에서 깨짐 없이 동작해야 함 (단일 브레이크포인트 `max-width: 600px`만 사용)
- 외부 프로젝트의 추가/제거가 발생하면 워크스페이스 루트 `CLAUDE.md` 표와 동기화 (홈페이지 동기화 원칙)
- 새 콘텐츠의 색은 `.cat-*` 분야 색에서만 고를 것. 글자 링크는 `--accent` 블루.
- CSS 수정 시 `index.html`의 `<link href="index.css?v=...">` 캐시 버스트 쿼리도 함께 올릴 것.
- 같은 파일명으로 PDF·이미지 자산을 교체하면 CDN/브라우저 캐시가 옛 버전을 줄 수 있음 → 링크 `href`에 `?v=YYYYMMDD` 캐시버스트를 붙여 교체 보장.
- 증명서·자격증 등 개인정보 문서를 공개 게시할 때: 단순 검은 박스가 아니라 PyMuPDF redaction(텍스트 레이어 제거)으로 블라인드. 전자증명서의 **문서확인번호**는 발급기관 검증 사이트(icert.skku.edu 등)에서 원본 조회가 가능해 다른 블라인드를 무력화하므로 함께 가릴 것.
