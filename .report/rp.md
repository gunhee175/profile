# 과제 1 보고서 — Hugo 포트폴리오 웹사이트 제작

> **전북대학교 | 장건희 | 제출일: 2026-11-07**

---

## 1. 개요

Hugo 정적 사이트 생성기와 `hugo-theme-console` 테마를 활용하여 개인 포트폴리오 웹사이트를 제작하고 GitHub Pages로 배포하였다.

| 항목 | 내용 |
|------|------|
| **사이트 URL** | https://gunhee175.github.io/profile/ |
| **소스 저장소** | https://github.com/gunhee175/profile |
| **사용 테마** | hugo-theme-console (Terminal CSS 기반) |
| **Hugo 버전** | Extended v0.167.0 |
| **배포 방법** | GitHub Actions (CI/CD 자동 배포) |

---

## 2. 사용 기술 및 도구

### 2.1 Hugo 정적 사이트 생성기

Hugo(https://gohugo.io)는 Go 언어로 작성된 오픈소스 정적 사이트 생성기이다. 마크다운(.md) 파일로 콘텐츠를 작성하면 HTML 사이트로 빌드해준다.

- **테마**: [hugo-theme-console](https://themes.gohugo.io/) — 터미널 콘솔 UI 콘셉트의 미니멀 테마
- **설정 파일**: `site/hugo.toml` (사이트 제목, 메뉴, 애니메이션 등 설정)
- **콘텐츠 디렉토리**: `site/content/` (마크다운 파일)

### 2.2 GitHub Pages 배포

[Hugo GitHub Pages 공식 가이드](https://gohugo.io/host-and-deploy/deploy-to-github-pages/)를 참고하여 자동 배포 환경을 구성하였다.

- `.github/workflows/hugo-pages.yml`: GitHub Actions 워크플로우
- `main` 브랜치 푸시 시 자동으로 빌드 → 배포 수행
- `actions/checkout`, `actions/setup-go`, `actions/upload-pages-artifact`, `actions/deploy-pages` 사용

---

## 3. 사이트 구조

```
site/
├── hugo.toml               # 사이트 설정 (제목, 메뉴, 언어)
├── assets/css/custom.css   # 커스텀 스타일 (한국어 폰트, 프로필 등)
├── content/
│   ├── about/              # 소개 · 기술 스택
│   ├── experience/         # 연구 경력 (BCG 연구실)
│   ├── activities/         # 동아리 · 대외활동 (RAMS)
│   ├── projects/           # 프로젝트 · 자격증
│   └── interests/          # 관심 분야
└── themes/template/        # hugo-theme-console 테마
    └── layouts/
        ├── _default/baseof.html   # 기본 레이아웃 (웹 접근성 적용)
        ├── _default/single.html   # 단일 페이지 레이아웃
        ├── index.html             # 홈 페이지 (프로필 카드)
        └── partials/footer.html   # 푸터
```

### 메뉴 구성

| 메뉴 | URL | 내용 |
|------|-----|------|
| `about/` | /about/ | 개인 소개, 기술 스택, 연락처 |
| `experience/` | /experience/ | BCG 연구실 활동, 연구 주제 목록 |
| `activities/` | /activities/ | RAMS 보안동아리 운영진 활동 |
| `projects/` | /projects/ | 프로젝트 소개, 네트워크관리사 2급 자격증 |
| `interests/` | /interests/ | 관심 분야 (데이터 시각화, 전파 분석 등) |

---

## 4. 주요 구현 내용

### 4.1 홈 화면 (프로필 카드)

홈 화면(`index.html`)을 프로필 카드 형태로 재구성하였다. 인스타그램 프로필 이미지를 프로필 사진으로 사용하고, 이름·소속·소개·외부 링크를 한눈에 볼 수 있도록 구성하였다.

```html
<!-- 프로필 사진에 alt 텍스트 적용 (웹 접근성) -->
<img src="..." alt="장건희 프로필 사진" class="profile-img" width="150" height="150">
```

### 4.2 웹 접근성 (Web Accessibility)

[W3C WAI 페이지 구조 가이드](https://www.w3.org/WAI/tutorials/page-structure/) 및 [이미지 가이드](https://www.w3.org/WAI/tutorials/images/)를 참고하여 다음을 적용하였다.

- `<html lang="ko">`: 문서 언어 명시
- `<main role="main" id="main-content">`: 메인 콘텐츠 영역 명시
- `<header>`, `<nav aria-label="주요 메뉴">`, `<article>`, `<footer role="contentinfo">`: 시맨틱 HTML 태그 사용
- `<img alt="...">`: 모든 이미지에 대체 텍스트 제공
- `<nav aria-label="외부 링크">`: 네비게이션 목적 명시

### 4.3 한국어 고정폭 폰트

터미널 콘셉트 테마에 맞는 한국어 고정폭 폰트를 적용하였다.

```css
/* 나눔고딕코딩: 한국어 지원 고정폭 폰트 */
@import url('https://fonts.googleapis.com/css2?family=Nanum+Gothic+Coding:wght@400;700&display=swap');

:root {
    --font-stack: "Nanum Gothic Coding", "D2Coding", "Consolas", monospace;
}
```

### 4.4 콘텐츠 구성

**About 페이지**: 개인 소개, 프로그래밍 언어 숙련도, 연락처 정보

**Experience 페이지**: BCG 연구실 학부연구생 경력, 주요 연구 활동(시간순):
1. XZ 취약점 분석 탐구 (CVE-2024-3094)
2. WiFi-Sensing 연구 (CSI/BFI 전파 분석)
3. 현재: CSI/BFI 무선 전파 심층 분석

**Activities 페이지**: 전북대 보안동아리 RAMS 운영진 활동

**Projects 페이지**: 연구 프로젝트 소개 + **네트워크관리사 2급 자격증** 취득 기재

**Interests 페이지**: 데이터 시각화 · 전파 분석 · 악성코드 분석 · 차세대 표준 통신 기술

---

## 5. 배포 과정

### 5.1 GitHub Pages 설정

1. GitHub 저장소(`gunhee175/profile`)의 **Settings > Pages** 에서 소스를 **GitHub Actions**로 설정
2. `main` 브랜치에 푸시하면 자동으로 워크플로우 실행

### 5.2 GitHub Actions 워크플로우

```yaml
# .github/workflows/hugo-pages.yml 주요 단계
jobs:
  build:
    - uses: actions/checkout@v7
    - name: Install Hugo (v0.167.0 Extended)
    - name: Build Hugo site
      run: python .github/pages_build.py --build
    - uses: actions/upload-pages-artifact@v5
  deploy:
    - uses: actions/deploy-pages@v5
```

### 5.3 배포 URL

> **https://gunhee175.github.io/profile/**

---

## 6. 파일 구조 다이어그램

```
hugo-theme-console-master/          ← 프로젝트 루트
│
├── .github/
│   ├── workflows/hugo-pages.yml    ← GitHub Actions CI/CD
│   └── pages_build.py              ← 빌드 스크립트
│
├── site/                           ← Hugo 사이트 루트
│   ├── hugo.toml                   ← 사이트 설정
│   ├── pages.json                  ← GitHub Pages 빌드 설정
│   ├── assets/css/custom.css       ← 커스텀 스타일
│   ├── content/                    ← 마크다운 콘텐츠
│   │   ├── about/index.md
│   │   ├── experience/index.md
│   │   ├── activities/index.md
│   │   ├── projects/index.md
│   │   └── interests/index.md
│   └── themes/template/            ← 커스터마이징된 테마
│       ├── layouts/
│       │   ├── _default/baseof.html
│       │   ├── _default/single.html
│       │   ├── index.html
│       │   └── partials/footer.html
│       └── static/
│           └── hugo-theme-console/ ← CSS, 폰트 에셋
│
└── .github-pages.json              ← 설정 메타데이터
```

---

## 7. 결론

Hugo 정적 사이트 생성기와 `hugo-theme-console` 테마를 활용하여 터미널 콘셉트의 개인 포트폴리오 사이트를 제작하고 GitHub Pages로 배포하였다. 웹 접근성 가이드라인을 준수하여 시맨틱 HTML 태그와 이미지 대체 텍스트를 적용하였으며, 한국어 고정폭 폰트를 사용하여 테마 콘셉트와 일관성을 유지하였다. 사이버보안 연구자로서의 경력(BCG 연구실, RAMS 동아리, 각종 연구 프로젝트)을 체계적으로 구성하였다.

---
