# gunhee175 / profile

장건희(Jang Gun Hee)의 개인 소개 사이트입니다. Hugo와 Console 테마로 만들고 GitHub Pages로 배포합니다.

- 공개 사이트: https://gunhee175.github.io/profile/
- 테마 원본 README: `site/themes/template/README.md`

## 1. 필요 도구와 버전

| 도구 | 버전 | 비고 |
|------|------|------|
| Hugo (Extended) | 0.167.0 | 워크플로 `HUGO_VERSION`과 동일하게 맞춤 |
| Git | 최신 | |
| Python | 3.9 이상 | 배포 워크플로는 3.12 사용 |

설치: https://gohugo.io/installation/ 에서 OS에 맞는 Hugo Extended 0.167.0을 설치한 뒤 `hugo version`으로 확인합니다.

## 2. 로컬에서 실행하기

```bash
git clone https://github.com/gunhee175/profile.git
cd profile/site
hugo server
```

브라우저에서 터미널에 표시된 주소(예: `http://localhost:1313/profile/`)를 엽니다. 배포용 결과물만 만들려면 `site` 폴더에서 `hugo --minify`를 실행하면 `site/public/`에 생성됩니다. (`public/`은 `.gitignore`로 제외됩니다.)

## 3. 내용 수정 위치

| 수정할 내용 | 파일 |
|------------|------|
| 사이트 주소·제목·언어·메뉴 | `site/hugo.toml` |
| 소개·경력·활동·프로젝트·관심 분야 글 | `site/content/<메뉴명>/index.md` |
| 홈 화면(프로필 카드) | `site/themes/template/layouts/index.html` |
| 추가 스타일 | `site/assets/css/custom.css` |
| 프로필 이미지 | `site/static/images/profile.jpg` |

## 4. 재배포와 확인

1. 수정 후 `git add` → `git commit -m "변경 내용"` → `git push origin main`
2. 저장소 **Actions** 탭(https://github.com/gunhee175/profile/actions)에서 `Deploy Hugo to GitHub Pages` 실행이 push로 시작되어 build·deploy 모두 성공했는지 확인
3. https://gunhee175.github.io/profile/ 를 새로고침(캐시 없이: Ctrl+Shift+R)해 변경 반영 확인

배포 설정: Settings → Pages → Source = GitHub Actions, 워크플로 파일 `.github/workflows/hugo-pages.yml`

## 5. 출처와 라이선스

| 자료 | 구분 | 출처 | 조건 |
|------|------|------|------|
| Console 테마 (`site/themes/template/`) | 외부 | https://github.com/mrmierzejewski/hugo-theme-console | MIT, `LICENSE` 유지 |
| Terminal CSS 0.7.4, animate.css 4.1.1 | 외부 (테마 포함) | https://terminalcss.xyz/, https://animate.style/ | MIT |
| Nanum Gothic Coding 웹폰트 | 외부 | Google Fonts | SIL OFL |
| 콘텐츠 글, `custom.css`, 프로필 사진 | 직접 제작 | — | 본인 저작물 |
| 프로필 이미지 경로 수정 (`index.html`) | AI 보조 (Claude) | 커밋 2f10c62 | — |
