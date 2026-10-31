# J-Hawk's Homepage

이종호(J-Hawk)의 개인 홈페이지입니다.

**배포 URL**: https://jhawk.kr

## 소개

순수 HTML/CSS로 구성된 정적 개인 프로필 페이지입니다. 프로필 정보와 개인 프로젝트 링크를 제공합니다. 다크 고정 톤(2026-10-31~)이며 모바일 우선으로 설계했습니다.

## 프로젝트 링크

| 프로젝트 | URL |
|----------|-----|
| ETF 투자 가이드 | https://etf.jhawk.kr |
| 공개 데이터 활용 사례 | https://opendata-jhawk.netlify.app |
| 통계 기반 복권번호 생성기 | https://lottery.jhawk.kr |
| AI 사주팔자 | https://fortune.jhawk.kr |
| AI 손금풀이 | https://sonkum.jhawk.kr |
| EDM DJ Console | https://edm-jahwk.netlify.app |
| 일본 마쓰야마 여행 추천 코스 | https://tour-matsuyama-jhawk.netlify.app |
| 호남 서남해안 여행 추천 코스 | https://tour-jeolla-jhawk.netlify.app |
| 동유럽 여행 추천 코스 | https://tour-europe-jhawk.netlify.app |

## 기술 스택

- HTML / CSS (외부 폰트·프레임워크·빌드 도구 없음)
- j-hawk VPS의 Caddy가 정적 파일로 직접 서빙 (`main` 푸시 후 VPS에서 `git pull`)

## 파일 구조

```
├── index.html   # 단일 컬럼 프로필 페이지
├── index.css    # 전체 스타일 (CSS 변수 토큰화)
├── favicon.svg  # 기본 파비콘
└── jh.jpg       # 프로필 사진 / 파비콘 폴백
```

## 로컬 실행

```bash
python3 -m http.server 8000
# http://localhost:8000 에서 확인
```
