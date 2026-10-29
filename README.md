# TRACE.LOG — 개인 보안 기술 블로그

[Chirpy Starter](https://github.com/cotes2020/chirpy-starter)를 바탕으로 만든 GitHub Pages용 Jekyll 블로그입니다. 한국어 메뉴, 자체 색상·아바타, 소개와 연구 분야 메뉴, 여섯 카테고리의 첫 글이 준비되어 있습니다.

## 맥에서 GitHub Pages에 올리기

아래의 `YOUR_ID`는 **본인의 실제 GitHub 사용자 이름**으로 바꾸세요.

1. GitHub에서 **Public** 저장소 `YOUR_ID.github.io`를 새로 만듭니다. 저장소를 만들 때 README나 라이선스는 추가하지 마세요.
2. `_config.yml`을 열고 다음 값을 설정합니다.

   ```yaml
   url: "https://YOUR_ID.github.io"
   github:
     username: YOUR_ID
   social:
     name: TRACE.LOG # 원한다면 공개용 이름으로 변경
     email:           # 공개할 연락처가 있을 때만 입력
     links:
       - /about/      # 첫 링크는 글의 작성자 소개로 사용
       - https://github.com/YOUR_ID
   baseurl: ""
   ```

   기존 `_config.yml`의 나머지 설정은 유지하세요. 기존 `social.links`의 `/about/`는 그대로 두고 GitHub 주소를 두 번째 항목으로 추가하면 됩니다.

3. Mac의 터미널에서 이 폴더로 이동한 뒤 아래 명령을 순서대로 실행합니다. `YOUR_ID`를 두 곳 모두 바꾸세요. `PUBLIC_NAME`과 `VERIFIED_EMAIL`은 본인이 선택한 공개 이름과 [GitHub 계정에 확인된 주소 또는 GitHub의 비공개 이메일 주소](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/setting-your-commit-email-address)로 바꾸세요.

   ```bash
   cd "$HOME/Downloads/github.io/trace-security-blog"
   git init -b main
   git config user.name "PUBLIC_NAME"
   git config user.email "VERIFIED_EMAIL"
   git add .
   git commit -m "Create TRACE.LOG security blog"
   git remote add origin https://github.com/YOUR_ID/YOUR_ID.github.io.git
   git push -u origin main
   ```

4. 저장소의 **Settings → Pages → Build and deployment → Source**를 **GitHub Actions**로 설정합니다. **Actions** 탭에서 `Build and Deploy` 작업이 성공하는지 확인하세요. 이미 실행되어 실패했다면 작업을 다시 실행합니다.
5. 배포가 끝나면 `https://YOUR_ID.github.io/`에서 확인합니다. 카테고리 페이지에는 아래 여섯 항목이 각각 한 개 이상 표시됩니다.

기존 프로젝트 저장소(예: `blog`)에 올린다면 `_config.yml`의 `url`은 `https://YOUR_ID.github.io`, `baseurl`은 `/blog`, `social.links`의 첫 항목은 `/blog/about/`로 설정하고 원격 주소를 `https://github.com/YOUR_ID/blog.git`로 바꾸세요. 이 경우 최종 주소는 `https://YOUR_ID.github.io/blog/`입니다.

## 준비된 콘텐츠

| 카테고리 | 첫 글의 초점 |
| --- | --- |
| 개발 | 로컬 JSONL 로그 요약기와 입력 검증 |
| CTF/Wargame | 포너블 문제의 초기 분석 순서 |
| Bug Bounty | 허가된 범위의 재현과 제보 정리 |
| 블로그/기술문서 | 재현 가능한 실습 문서 구조 |
| 논문/컨퍼런스 | 보안 논문 읽기를 위한 질문 |
| 공모전/자격증 | 준비 과정과 학습 기록 방법 |

총 9편의 글이 있고, 디지털 포렌식·프롬프트 인젝션·임베디드/차량 보안 주제도 포함합니다. 모두 **학습용 첫 글**이며 실제 대회 참가, 취약점 발견, 수상, 자격 취득을 주장하지 않습니다. 개인 프로젝트의 실제 자료를 공개할 때는 민감정보와 공개 가능 범위를 확인한 후 추가하세요.

## 글과 디자인 바꾸기

- 새 글: `_posts/YYYY-MM-DD-english-slug.md`를 만들고 YAML 머리말에 `title`, `date`, `description`, `categories`, `tags`를 적습니다. 카테고리는 반드시 위 표의 표기와 일치하는 **한 문자열**로 입력하세요. 예: `categories: ['CTF/Wargame']`.
- 소개: `_tabs/about.md`
- 연구 분야 메뉴: `_tabs/topics.md`
- 제목·설명·주소·GitHub 계정: `_config.yml`
- 색상·카드 스타일: `assets/css/jekyll-theme-chirpy.scss`
- 아바타: `assets/img/trace-avatar.svg`
- 브라우저·홈 화면 아이콘: `assets/img/favicons/`
- 배포 자동화: `.github/workflows/pages-deploy.yml`

폴더의 핵심 구조는 아래와 같습니다.

```text
trace-security-blog/
├── .github/workflows/pages-deploy.yml
├── _config.yml
├── _layouts/home.html
├── _posts/                  # 여섯 카테고리, 아홉 편의 글
├── _tabs/                   # 소개·연구 분야·카테고리 등 메뉴
├── assets/css/jekyll-theme-chirpy.scss
├── assets/img/trace-avatar.svg
├── assets/img/favicons/       # TRACE.LOG 전용 아이콘
├── Gemfile
├── licenses/                # 원본 Chirpy 라이선스 고지
└── index.html
```

로컬에서 미리 보려면 Ruby 3.1 이상(4.0 미만)과 Bundler를 준비한 뒤 `bundle install`, `bundle exec jekyll serve`를 실행하고 `http://127.0.0.1:4000/`을 엽니다. GitHub Actions에서는 Ruby 3.4로 자동 빌드됩니다.

원본 테마와 스타터는 MIT 라이선스이며 고지문은 `licenses/`에 보관했습니다. 새로 작성한 글과 아바타는 별도 허락 없이 재사용할 수 있도록 라이선스를 부여한 것이 아닙니다.
