# 김가현 포트폴리오

축산 AI 개발자를 목표로 하는 김가현(Olivia)의 개인 소개 웹사이트입니다.
Hugo 테마 [Spectra](https://github.com/JoeYang1412/hugo-theme-spectra)를 기반으로 만들었습니다.

- **사이트**: https://rosoefox.github.io/KGH_Olivia/
- **저장소**: https://github.com/rosoefox/KGH_Olivia
- **배포 상태**: https://github.com/rosoefox/KGH_Olivia/actions

## 필요한 도구

| 도구 | 버전 | 용도 |
|---|---|---|
| Hugo **Extended** | 0.167.0 | 사이트 빌드 (SCSS 처리에 Extended 판 필요) |
| Git | - | 버전 관리, push |
| Python | 3.9 이상 | 배포용 빌드 스크립트 (`.github/pages_build.py`) |

Hugo Extended 설치 (Windows):

```powershell
winget install Hugo.Hugo.Extended
hugo version   # "extended"와 버전이 표시되는지 확인
```

다른 OS는 [Hugo 설치 안내](https://gohugo.io/installation/)를 참고합니다.

## 로컬에서 실행하기

실제 사이트 소스는 `site/` 폴더에 있습니다.

```bash
git clone https://github.com/rosoefox/KGH_Olivia.git
cd KGH_Olivia/site
hugo server --config hugo.toml,pages.json --theme template --themesDir themes
```

브라우저에서 http://localhost:1313/KGH_Olivia/ 를 열면 미리 볼 수 있습니다. 파일을 저장하면 자동으로 새로고침됩니다.

배포와 같은 방식으로 빌드만 해보려면 저장소 루트에서 실행합니다. 결과는 `public/`에 생성됩니다.

```bash
python .github/pages_build.py --build
```

## 수정할 파일 위치

| 바꾸고 싶은 것 | 파일 |
|---|---|
| 사이트 제목, 배너 문구, 메뉴, 소셜 링크, 폰트 | `site/hugo.toml` |
| 화면에 나오는 한국어 문구 (footer, 사이드바 제목 등) | `site/i18n/ko.toml` |
| 색상 팔레트 | `site/static/css/custom.css` |
| 배너 레이아웃 | `site/layouts/partials/banner.html` |
| 소개 페이지 | `site/content/about/index.md` |
| 글 | `site/content/posts/<카테고리>/` 폴더 안의 `.md` 파일 |
| 대표 활동 글 (GLOTIZ) | `site/content/posts/projects/glotiz.md` |
| 브라우저 탭 아이콘 | `site/static/favicon.ico` (설정: `site/hugo.toml`의 `favicon`) |
| 화면 읽기용 버튼 이름 (접근성 라벨) | `site/layouts/_default/baseof.html`, `site/layouts/posts/single.html` 등 |
| 키보드 초점·링크 밑줄 등 접근성 스타일 | `site/static/css/custom.css` (아래쪽), 검색창 닫을 때 초점 되돌리기는 `site/layouts/_default/baseof.html` 끝부분 |
| 카테고리 이름·순서 | `site/content/posts/<카테고리>/_index.md` |

테마 원본(`site/themes/template/`)은 직접 수정하지 않고, 바꿀 파일만 `site/layouts/`에 같은 경로로 복사해 덮어씁니다.

## 수정 후 배포하기

1. 파일을 수정하고 로컬에서 확인합니다.
2. 커밋 후 `main` 브랜치에 push합니다.
   ```bash
   git add <수정한 파일>
   git commit -m "수정 내용 설명"
   git push origin main
   ```
3. push하면 GitHub Actions의 **Deploy Hugo to GitHub Pages** 워크플로(`.github/workflows/hugo-pages.yml`)가 자동으로 실행됩니다.
4. [Actions 탭](https://github.com/rosoefox/KGH_Olivia/actions)에서 해당 커밋의 실행이 초록색 체크(성공)인지 확인합니다.
5. 1~2분 뒤 [공개 사이트](https://rosoefox.github.io/KGH_Olivia/)에서 변경 사항을 확인합니다. 바로 반영되지 않으면 `Ctrl+Shift+R`로 강력 새로고침합니다.

**배포가 실패(빨간 X)했을 때**

- 실패한 실행을 눌러 어느 단계에서 멈췄는지 확인합니다.
- `Prepare dependencies`처럼 도구 설치 단계에서 실패했다면 일시적인 네트워크 문제일 수 있습니다. 실행 화면 오른쪽 위 **Re-run jobs**를 누르거나, 다음 커밋을 push하면 다시 실행됩니다.
- `Build` 단계에서 실패했다면 로컬에서 `python .github/pages_build.py --build`로 같은 오류가 나는지 확인하고 고친 뒤 다시 push합니다.

## 출처와 라이선스

| 구분 | 내용 | 출처 / 이용 조건 |
|---|---|---|
| 테마 | Spectra (`site/themes/template/`) | [JoeYang1412/hugo-theme-spectra](https://github.com/JoeYang1412/hugo-theme-spectra), MIT License ([LICENSE](LICENSE)) |
| 배포 스크립트 | `prepare_github_pages.py`, `.github/pages_build.py`, `.github/workflows/hugo-pages.yml` | 초급프로젝트 수업 제공 스크립트로 생성 |
| 웹폰트 | Noto Sans KR, Outfit, JetBrains Mono | [Google Fonts](https://fonts.google.com/), SIL Open Font License |
| 직접 작성 | 사이트 설정, 한국어 번역, 색상 팔레트, 소개·글 내용 | 본인 작성 |
| AI 생성 | 파비콘 `site/static/favicon.ico` | Claude Code가 Python(Pillow) 스크립트로 생성, 본인이 디자인 확인 후 사용 |
| AI 도움 | 설정 수정, 접근성 라벨 한글화, 동작 줄이기 CSS, 키보드 초점·링크 밑줄·태그 대비 CSS, 글 초안·표 정리(소개·GLOTIZ 글), 이 README 초안 | Claude Code (Anthropic) 사용 후 본인이 검토·수정 |

---

테마 원본 사용 설명서(영문)는 [THEME_README.md](THEME_README.md)에 보존했습니다.
