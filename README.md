# J-Hawk's Homepage

이종호(J-Hawk)의 개인 홈페이지입니다.

**배포 URL**: https://j-hawk.netlify.app

## 소개

순수 HTML/CSS로 구성된 정적 개인 프로필 페이지입니다. 프로필 정보와 개인 프로젝트 링크를 제공합니다.

## 프로젝트 링크

| 프로젝트 | URL |
|----------|-----|
| ETF 투자 대시보드 | https://jhawk-etf-dashboard.streamlit.app |
| 통계 기반 복권번호 생성기 | https://lottery-number-generator.onrender.com |
| AI 사주팔자 | https://saju-fortune.onrender.com |
| Music Creator | https://strudel-creator.netlify.app |
| I'm project (Classified) | https://shilla-icn-mkt.netlify.app |
| 전주 여행 코스 (가족 Only) | https://jeonju-tour.netlify.app |
| 동유럽 여행 코스 (가족 Only / On Hold) | https://jhawk-east-europe-tour.netlify.app |

## 기술 스택

- HTML / CSS
- 빌드 도구, 프레임워크, 패키지 매니저 없음
- Netlify 자동 배포 (GitHub `main` 브랜치 푸시 시)

## 파일 구조

```
├── index.html   # 프로필 카드 (단일 페이지)
├── index.css    # 전체 스타일
└── jh.jpg       # 프로필 사진 / 파비콘
```

## 로컬 실행

```bash
python3 -m http.server 8000
# http://localhost:8000 에서 확인
```
