# 주원정 JOO WONJEONG — Portfolio

콘텐츠 & 브랜드 마케터 주원정의 개인 포트폴리오 사이트입니다.
순수 HTML / CSS / Vanilla JS 단일 페이지로, 별도 빌드 과정 없이 GitHub Pages에서 바로 동작합니다.

## 📁 폴더 구조

```
portfolio/
├─ index.html          # 메인 페이지 (GitHub Pages가 자동으로 띄우는 진입점)
├─ .nojekyll           # GitHub Pages의 Jekyll 처리를 끄는 빈 파일 (그대로 두세요)
├─ README.md
└─ assets/             # 이미지 · 영상 (전부 상대경로로 참조)
   ├─ xhs-reel.mp4 / cover-*.jpg / xhs-profile.jpg   (샤오홍슈)
   ├─ yt-*.jpg                                        (유튜브)
   ├─ f1-proto.mp4 / f1-deck-*.jpg / f1-guide-*-*.jpg (F1 기획서·가이드북)
   └─ ...
```

- 모든 이미지·영상은 `assets/…` **상대경로**로 연결되어 있어, `username.github.io/저장소이름/` 같은 하위 경로에서도 그대로 작동합니다.
- 글꼴(Pretendard·Space Grotesk·JetBrains Mono)과 스무스 스크롤 라이브러리(Lenis)는 CDN(`https://…`)에서 불러옵니다 — 인터넷 연결만 있으면 됩니다.

## 🚀 GitHub Pages 배포 방법

### 1. GitHub에서 빈 저장소 만들기
1. GitHub 로그인 → 우측 상단 **＋ → New repository**
2. Repository name 입력 (예: `portfolio` 또는 `joowonjeong-portfolio`)
3. **Public** 선택, README/.gitignore 등은 **추가하지 않음** (빈 저장소로)
4. **Create repository**

### 2. 이 폴더를 저장소에 올리기
이 폴더에서 터미널을 열고 아래를 순서대로 실행하세요.
(`<USERNAME>`과 `<REPO>`는 본인 것으로 바꿉니다.)

```bash
git init -b main
git add .
git commit -m "Deploy portfolio"
git remote add origin https://github.com/<USERNAME>/<REPO>.git
git push -u origin main
```

### ⚡ 더 빠른 방법 — GitHub CLI 한 번에 (저장소 생성 + 푸시 + Pages 켜기)
[GitHub CLI](https://cli.github.com)가 있으면 위 1~3단계를 명령 몇 줄로 끝낼 수 있습니다.

```bash
# (최초 1회) 설치 후 로그인 — 브라우저로 인증
#   macOS:  brew install gh
gh auth login

# 배포 폴더(이 폴더)로 이동
cd portfolio_site     # 또는 zip을 푼 폴더

# 1) git 초기화 + 커밋
git init -b main && git add . && git commit -m "Deploy portfolio"

# 2) 저장소 생성 + 푸시 (이름은 원하는 대로)
gh repo create joowonjeong-portfolio --public --source=. --remote=origin --push

# 3) GitHub Pages 활성화 (main / root)
gh api --method POST /repos/{owner}/{repo}/pages -f "source[branch]=main" -f "source[path]=/"

# 4) 공개 주소 확인 (1~2분 뒤 활성화)
gh api /repos/{owner}/{repo}/pages --jq .html_url
```

> `{owner}`/`{repo}` 는 gh가 현재 폴더의 저장소를 보고 자동으로 채워줍니다. 그대로 두고 실행하면 됩니다.

---

### 3. Pages 켜기 (웹 UI로 하는 경우)
1. 저장소 → **Settings → Pages**
2. **Build and deployment → Source** 를 **Deploy from a branch** 로 선택
3. **Branch** 를 `main` / 폴더 `/ (root)` 로 지정 후 **Save**
4. 1~2분 뒤 상단에 공개 주소가 표시됩니다:
   **`https://<USERNAME>.github.io/<REPO>/`**

### (선택) 사용자 페이지로 루트 주소 쓰기
저장소 이름을 **`<USERNAME>.github.io`** 로 만들면 주소가
`https://<USERNAME>.github.io/` 로 더 깔끔해집니다. 상대경로라 이 경우에도 그대로 동작합니다.

## 🖥 로컬에서 미리 보기
영상·이미지는 `file://` 로 열면 일부 브라우저에서 제한될 수 있어, 간단한 로컬 서버로 확인하는 걸 권장합니다.

```bash
# Python 3가 있다면
python3 -m http.server 8080
# 그 후 브라우저에서 http://localhost:8080 접속
```

## ✅ 점검 완료 사항
- 모든 이미지·영상 링크가 `assets/` 상대경로로 연결되어 GitHub Pages 하위 경로에서도 정상 동작
- 내부 메뉴 이동(#work, #about 등) 정상
- 연락처 메일: `joowj2002@naver.com`
- `.nojekyll` 포함으로 Jekyll 빌드 우회(에셋 그대로 서빙)
- `prefers-reduced-motion` 및 키보드 접근성(케이스 카드 Tab/Enter) 대응

## 🔧 수정하고 싶을 때
- 내용·문구: `index.html` 의 해당 섹션 텍스트를 직접 수정
- 이미지·영상 교체: `assets/` 안의 파일을 같은 이름으로 교체하거나, 새 파일을 넣고 `index.html` 의 `src` 경로를 변경
- 저장 후 `git add . && git commit -m "update" && git push` 하면 1~2분 뒤 자동 반영

## ⚠️ 참고
- 전체 용량은 약 18MB로, 대부분 F1 프로토타입 영상(`f1-proto.mp4`)과 기획서·가이드북 이미지입니다. GitHub Pages 무료 한도(저장소 1GB, 월 100GB 대역폭) 내에서 충분합니다.
- 더 가볍게 하고 싶다면 F1 영상을 더 짧게 자르거나, 가이드북 이미지를 줄일 수 있습니다.

---
© 2026 주원정 (JOO WONJEONG)
