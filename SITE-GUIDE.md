# 내 홈페이지 설명서 (yjchoi.dev)

웹 개발을 따로 공부하지 않았어도 읽히도록, 이 사이트가 **무엇으로 이루어져
있고 / 어떻게 동작하고 / 어디를 고치면 되는지**를 처음부터 풀어 쓴 문서입니다.

> **⚠️ 2026-09-19 개편 이전 기준으로 쓰인 문서입니다.** 웹페이지의 기본 원리,
> 폴더 구조, 본문(경력·프로젝트·학력·연락처) 고치는 법, 배포 방법은 그대로
> 맞습니다. 아래 세 가지는 달라졌으니 해당 부분을 읽을 때 감안하세요.
>
> 1. **라이트 모드와 다크모드 버튼이 없어졌습니다.** 사이트는 어두운 테마
>    하나뿐입니다. `:root` 색상 변수 블록도 하나만 남았고, 테마를 고르던
>    스크립트(`localStorage`, `prefers-color-scheme`, `data-theme`)는 전부
>    삭제됐습니다. 이 문서의 "테마가 정해지는 순서"와 "① 다크모드 토글" 설명은
>    더 이상 해당하지 않습니다.
> 2. **맨 위에 히어로 띠가 생겼습니다.** 메뉴와 이름이 `<div class="hero">`
>    안으로 들어갔고, 그 뒤에서 `<canvas id="mesh">`에 물결치는 메시가
>    그려집니다. 그리는 코드는 파일 맨 끝의 두 번째 `<script>`이고, 맨 위
>    상수(`RADIUS`, `ELEV`, `BLUR`, `ORBIT` 등)만 바꾸면 크기·각도·흐림·회전
>    속도가 조정됩니다.
> 3. **줄 번호가 전부 밀렸습니다.** 파일이 614줄에서 900줄 안팎으로 늘었으니,
>    이 문서에 적힌 "줄 358" 같은 번호는 검색(⌘F)으로 대신 찾으세요.

---

## 0. 먼저, 웹페이지가 뭔지 30초

웹페이지는 언어 **세 개**로 만들어집니다.

| 언어 | 역할 | 비유 |
| --- | --- | --- |
| **HTML** | 내용과 구조 | 뼈대 — "여기는 제목, 여기는 문단, 여기는 이미지" |
| **CSS** | 생김새 | 옷·화장 — "제목은 크고 굵게, 배경은 미색" |
| **JavaScript** | 동작 | 근육 — "이 버튼을 누르면 다크모드로 바뀐다" |

보통 사이트는 이 셋을 파일 여러 개로 쪼개고, 거기에 React·Jekyll 같은
도구까지 얹습니다. **이 사이트는 셋을 `index.html` 파일 하나에 다 넣었습니다.**
도구도 없습니다.

왜냐면 개인 홈페이지는 1년에 두세 번 고치는 물건인데, 도구를 쓰면 6개월 뒤에
한 줄 고치려고 열었을 때 "빌드가 안 됨 → 라이브러리 버전 충돌 → 하루 날림"이
벌어지기 때문입니다. 이건 5년 뒤에 열어도 그냥 열립니다.

**그래서 이 사이트를 고치는 절차는 이게 전부입니다:**

```
index.html 을 에디터에서 연다  →  고친다  →  저장한다
                                    ↓
                          브라우저에서 새로고침 (끝)
```

컴파일도, 서버 실행도, 설치도 없습니다.

---

## 1. 저장소에 뭐가 있나

```
index.html    ← 사이트 전체. 사실상 이 파일이 곧 홈페이지다
logos/        ← 로고 이미지들 (학교, 회사, 파비콘)
og-image.png  ← 카톡에 링크 붙였을 때 뜨는 미리보기 그림
CNAME         ← "이 사이트 주소는 yjchoi.dev 다" 라고 GitHub에 알려주는 파일
.nojekyll     ← "GitHub야, 내 파일 건드리지 말고 그대로 내보내" 라는 신호
README.md     ← 영문 짧은 요약
SITE-GUIDE.md ← 지금 읽고 있는 이 문서
```

### 이 파일들이 왜 필요한지

**`CNAME`** — 원래 GitHub Pages 주소는 `yjchoi00.github.io`입니다. 이 파일 안에
`yjchoi.dev` 한 줄이 적혀 있어서, GitHub가 내 도메인으로 들어온 요청도
이 사이트로 연결해 줍니다.

**`.nojekyll`** — GitHub Pages는 기본적으로 **Jekyll**이라는 블로그 생성기를
한 번 돌립니다. 그 과정에서 `_`로 시작하는 파일을 무시하는 등 파일을 멋대로
손댑니다. 이 파일이 있으면 그 단계를 통째로 건너뜁니다. **파일 내용은
비어 있어도 되고, 존재한다는 사실 자체가 신호**입니다.

**`og-image.png`** — 카톡·슬랙·링크드인에 링크를 붙이면 뜨는 카드 그림입니다.
1200×630 크기가 표준입니다. (자세한 사연은 §3.1)

### `logos/` 안

| 파일 | 어디에 쓰이나 |
| --- | --- |
| `sogang.png` | Experience — 서강대 |
| `shinkim.png` | Experience — 법무법인 세종 |
| `army.png` | Experience — 육군 3사단 |
| `ucl.png` | Education — UCL (두 항목이 같은 파일을 공유) |
| `dankook.svg` | Education — 단대부고 |
| `favicon-32.png`, `favicon-64.png` | 브라우저 탭에 뜨는 작은 아이콘 |
| `apple-touch-icon.png` | 아이폰에서 "홈 화면에 추가" 했을 때 아이콘 |

---

## 2. 페이지가 화면에 어떻게 생겼나

실제 페이지를 글자로 그리면 이렇습니다.

```
┌──────────────────────────────────────────────────┐
│              Experience  Projects  Contact  ☾    │  ← <nav>  (오른쪽 정렬)
│                                                  │
│  Youngjun Choi · 최영준                           │  ← <header class="intro">
│  BSc Data Science, University College London     │     이름 / 한 줄 소개 /
│                                                  │     자기소개 두 문단
│  I am a Data Science undergraduate at UCL...     │
│  My interests sit at the intersection of...      │
│                                                  │
│  EXPERIENCE ─────────────────────────────────    │  ← <section id="experience">
│  [로고]  Sogang University      2026.6 – 2026.10 │
│          Undergraduate AI Researcher             │     ← .item 블록 하나
│          Game-theoretic modelling...             │
│  [로고]  Shin & Kim LLC          2026.6 – 2026.7 │     ← 같은 블록 반복
│  [로고]  Republic of Korea Army  2022.1 – 2023.7 │
│                                                  │
│  PROJECTS ───────────────────────────────────    │  ← <section id="projects">
│  Document Reader QA Bot (RAG)              2025  │     (로고 없는 버전)
│  Python · LangChain · ChromaDB                   │
│  ... 3개 더                                       │
│                                                  │
│  EDUCATION ──────────────────────────────────    │  ← <section id="education">
│  [로고]  UCL                       2025 – 2028   │
│  ... 2개 더                                       │
│                                                  │
│  CONTACT ────────────────────────────────────    │  ← <section id="contact">
│  Email     youngjun.choi.24@ucl.ac.uk / gmail    │
│  LinkedIn  linkedin.com/in/youngjun-choi         │
│                                                  │
│  ────────────────────────────────────────────    │
│  © 2026 Youngjun Choi          Seoul ⇄ London    │  ← <footer>
└──────────────────────────────────────────────────┘
```

`<nav>`, `<header>`, `<section>`, `<footer>`는 HTML이 제공하는 **의미 있는
이름표**입니다. 전부 `<div>`로 해도 화면은 똑같이 나오지만, 이렇게 쓰면
검색엔진과 스크린리더가 "여기가 내비게이션이구나"를 알아먹습니다.

**중요한 사실 하나:** `#experience`, `#projects` 같은 `id`는 두 가지 일을
동시에 합니다 —
① 위 내비게이션의 `<a href="#experience">` 링크가 그 위치로 점프하는 목적지이고,
② CSS가 "이 구역"을 지목할 때 쓰는 이름입니다.

---

## 3. `index.html` 안을 열어보면

파일이 610줄쯤 되지만, 실제로는 **네 덩어리**뿐입니다.

```
줄 1 – 356    <head>     화면에 안 보이는 정보 + CSS 전체
줄 358 – 366  <nav>      상단 메뉴 + 다크모드 버튼
줄 367 – 561  <div class="wrap">   ← 진짜 내용 (§2 그림의 본문 전부)
줄 563 – 612  <script>   자바스크립트 (딱 세 가지 기능)
```

`<head>`가 356줄이나 되는 이유는 **CSS가 통째로 그 안에 들어 있기** 때문입니다
(64~355줄). 순수 정보는 앞의 60줄뿐입니다.

### 3.1 `<head>` — 사람은 못 보고 기계만 읽는 부분

여기 적힌 건 화면에 하나도 안 나옵니다. 대신 **구글, 카톡, 링크드인**이 읽습니다.
개인 홈페이지의 실질적 목적이 "내 이름을 검색했을 때 이게 첫 결과로 뜨는 것"
이라서, 이 부분을 꼼꼼히 채워뒀습니다.

**(a) 검색 결과에 뜨는 글자**

```html
<title>Youngjun Choi | yjchoi.dev</title>
<meta name="description" content="Youngjun Choi (최영준) — BSc Data Science at ..." />
```

구글 검색 결과의 파란 제목 = `title`, 그 아래 회색 설명문 = `description`
입니다. `keywords`에 한글 이름 "최영준"도 넣어놔서 한글 검색에도 걸립니다.

**(b) `canonical` — 중복 방지**

```html
<link rel="canonical" href="https://yjchoi.dev/" />
```

같은 페이지가 `yjchoi.dev`, `www.yjchoi.dev`, `yjchoi00.github.io` 세 주소로
접근됩니다. 구글이 이걸 서로 다른 세 페이지로 착각하면 순위가 셋으로 쪼개집니다.
이 한 줄이 "정식 주소는 하나뿐이다"라고 못 박습니다.

**(c) Open Graph — 카톡 미리보기** ([index.html:24-43](index.html#L24-L43))

`og:`로 시작하는 태그들이, 링크를 붙였을 때 뜨는 카드의 제목·설명·그림을
결정합니다. 코드에 이런 주석이 달려 있습니다:

> *Without an explicit og:image, scrapers pick an image out of the page —
> which meant the first logo in Experience.*

**실제로 있었던 일입니다.** `og:image`를 안 정해두면 카톡·링크드인이
페이지 안에서 아무 이미지나 골라 오는데, 그게 하필 Experience 첫 번째
로고(서강대 마크)였습니다. 그래서 `og-image.png`를 지정해 못 박았습니다.

**(d) JSON-LD — 구글에게 기계어로 자기소개** ([index.html:47-61](index.html#L47-L61))

```json
{ "@type": "Person", "name": "Youngjun Choi", "alternateName": "최영준",
  "affiliation": { "@type": "CollegeOrUniversity", "name": "University College London" } }
```

위의 `description`은 사람이 읽는 문장이지만, 이건 **구글이 파싱하는 데이터**
입니다. "이 페이지는 회사도 제품도 아니고 **사람**에 관한 것이고, 다른 이름은
최영준, 소속은 UCL"이라고 구조화해서 알려줍니다. schema.org라는 표준 형식이고,
이름 검색 시 정확한 인물로 인식되는 데 유리합니다.

> ⚠️ **주의:** 자기소개를 고칠 일이 생기면 **세 군데를 같이** 고쳐야 앞뒤가
> 맞습니다 — 본문 `<p class="bio">`, `<meta name="description">`,
> `<meta property="og:description">`.

### 3.2 CSS — 색깔은 전부 한 곳에 모아뒀다

CSS에서 제일 흔한 사고가 "색을 바꾸려고 파일 전체에서 `#1a1a1a`를 찾아
바꾸다가 몇 개를 빠뜨리는 것"입니다. 그래서 **CSS 변수**를 씁니다.

파일 맨 위 [index.html:64-73](index.html#L64-L73)에 색을 이름으로 정의해두고:

```css
:root {
  --bg: #fbfbfa;      /* 페이지 배경 */
  --fg: #1a1a1a;      /* 본문 글자 */
  --muted: #6b6b6b;   /* 흐린 글자 — 날짜, 직책, 섹션 제목 */
  --rule: #e3e3e0;    /* 구분선 */
  --link: #1a1a1a;    /* 링크 글자 */
  --accent: #8a5a2b;  /* 강조색 — 링크에 마우스 올렸을 때 갈색 */
  --tile: #ffffff;    /* (지금은 안 쓰임 — 아래 설명) */
  --measure: 46rem;   /* 본문 최대 너비 */
}
```

아래 CSS는 전부 이름으로 갖다 씁니다:

```css
body { background: var(--bg); color: var(--fg); }
```

**→ 색을 바꾸고 싶으면 위 블록만 고치면 사이트 전체가 따라옵니다.**

> `--tile`은 예전에 로고 뒤에 흰 타일을 깔았을 때 쓰던 색입니다. 지금은
> 배경이 투명한 PNG/SVG를 페이지 위에 그대로 올리는 방식으로 바뀌어서
> 아무 데도 안 쓰입니다. 지워도 아무 일 안 일어납니다.

`--measure: 46rem`은 본문이 아무리 넓은 모니터에서도 46rem을 넘지 않게 합니다.
한 줄이 너무 길면 눈이 다음 줄 첫머리를 못 찾아서 읽기가 힘들어지는데,
그걸 막는 장치입니다.

#### 다크 모드가 세 겹인 이유

이 부분이 이 사이트에서 제일 까다로운 코드입니다. 경우가 **세 가지**라서 그렇습니다.

| 상황 | 어떻게 보여야 하나 |
| --- | --- |
| 1. OS 라이트 + 사용자가 아무것도 안 누름 | 라이트 |
| 2. **OS 다크** + 사용자가 아무것도 안 누름 | 다크 (알아서 맞춰주기) |
| 3. 사용자가 ☾ 버튼을 **직접 누름** | **누른 대로** (OS 설정 무시) |

코드가 이 셋에 하나씩 대응합니다:

```css
:root { --bg: #fbfbfa; ... }                    /* ① 기본값 = 라이트 */

:root[data-theme="dark"] { --bg: #16161a; ... } /* ③ 버튼으로 다크를 고름 */

@media (prefers-color-scheme: dark) {           /* ② OS가 다크일 때 */
  :root:not([data-theme="light"]) { --bg: #16161a; ... }
}
```

②의 `:not([data-theme="light"])`가 핵심입니다. 이게 없으면 —
**OS는 다크인데 나는 라이트로 보고 싶어서 버튼을 눌러도, OS 설정이 이겨서
계속 어둡게 나옵니다.** "사용자가 라이트를 명시적으로 고른 게 아닐 때만"
이라는 단서를 붙여서 그걸 막았습니다.

#### CSS 나머지

주석으로 구획이 나뉘어 있어서 찾기 쉽습니다:

```
/* ---------- nav ---------- */              124줄
/* ---------- header ---------- */           166줄
/* ---------- sections ---------- */         194줄
/* ---------- contact / footer ---------- */ 289줄
@media (max-width: 34rem)                    341줄  ← 휴대폰
```

맨 끝 `@media (max-width: 34rem)`는 **화면 폭이 34rem(약 544px)보다 좁을 때만**
적용되는 규칙입니다. 즉 휴대폰용입니다. 하는 일은 두 가지 — 이름 크기를 줄이고,
날짜를 제목 오른쪽이 아니라 **아랫줄로 내립니다**. 폰에서는 "Republic of Korea
Army"와 "2022.1 – 2023.7"이 한 줄에 같이 들어갈 자리가 없기 때문입니다.

### 3.3 본문 — 블록 하나만 이해하면 전부 이해한 것

Experience와 Education의 **모든 항목이 똑같은 틀**입니다. 이 틀 하나만 알면 됩니다.

```html
<div class="item">                                    ← 항목 하나 전체를 감싸는 상자
  <span class="logo" data-mono="SG">                  ← 왼쪽: 로고 자리
    <img src="logos/sogang.png" alt="Sogang University" />
  </span>
  <div class="item-body">                             ← 오른쪽: 글자 전부
    <div class="item-head">
      <span class="item-title">Sogang University</span>   ← 굵은 제목
      <span class="item-meta">Jun 2026 – Oct 2026</span>  ← 날짜 (오른쪽 끝)
    </div>
    <div class="item-sub">Undergraduate AI Researcher</div>  ← 직책 (흐린 색)
    <p>Game-theoretic modelling for strategic interaction...</p>  ← 설명
  </div>
</div>
```

화면에서는 이렇게 배치됩니다:

```
┌────────┬─────────────────────────────────────────────┐
│        │  Sogang University        Jun 2026 – Oct 2026│  ← .item-head
│ [로고] │  Undergraduate AI Researcher                 │  ← .item-sub
│        │  Game-theoretic modelling for strategic...   │  ← <p>
└────────┴─────────────────────────────────────────────┘
  .logo             .item-body
```

**왼쪽 로고 / 오른쪽 내용의 2단 배치는 `display: flex`가 만듭니다.** flex는
"상자 안의 것들을 가로로 나란히 놓아라"라는 뜻입니다. 그리고 날짜가 오른쪽
끝에 붙는 건 이 한 줄 덕분입니다:

```css
.item-meta { margin-left: auto; }   /* 왼쪽 여백을 최대로 → 오른쪽 끝으로 밀림 */
```

**Projects 섹션**은 같은 틀에서 로고를 빼고, 설명문 대신 사용 기술 한 줄
(`.tech`)만 씁니다.

#### 항목 추가하는 법

위 블록을 복사해서 붙여넣고 **글자만 갈아끼우면** 됩니다. 새 경력 하나를
Experience 맨 위에 넣는다면:

```html
<div class="item">
  <span class="logo" data-mono="XX"><img src="logos/새로고.png" alt="회사 이름" /></span>
  <div class="item-body">
    <div class="item-head">
      <span class="item-title">회사 이름</span>
      <span class="item-meta">Jan 2027 – Present</span>
    </div>
    <div class="item-sub">직책 · 도시</div>
    <p>한두 줄 설명.</p>
  </div>
</div>
```

CSS는 손댈 필요가 전혀 없습니다. `class="item"`을 붙이는 순간 기존 스타일이
그대로 적용됩니다.

#### 눈여겨볼 자잘한 장치 두 개

**`.logo.nudge`** ([index.html:249-251](index.html#L249-L251))

```css
.logo.nudge img { transform: scale(1.14); }
```

로고는 전부 같은 크기의 정사각형 칸에 들어갑니다. 그런데 육군 마크는
**삼각형**이라 정사각형의 절반도 안 채웁니다. 그래서 규격상으로는 같은
크기인데 눈에는 혼자 작아 보였습니다. 14% 키워서 **눈으로 맞췄습니다.**
(수치가 아니라 시각적으로 맞추는 건 타이포그래피에서 흔한 보정입니다.)

**`data-mono="SG"`**

```html
<span class="logo" data-mono="SG"><img src="logos/sogang.png" ... /></span>
```

이미지 로딩이 실패했을 때 대신 보여줄 **글자 약어**를 미리 적어둔 것입니다.
`data-`로 시작하는 속성은 HTML이 "여기에 원하는 값을 넣어두고 나중에
자바스크립트로 꺼내 써라"고 열어둔 자리입니다. 실제 교체는 아래 스크립트가 합니다.

### 3.4 자바스크립트 — 딱 세 가지만 한다

[index.html:563-612](index.html#L563-L612). 전체가 50줄이고, 하는 일은 셋뿐입니다.

**① 다크모드 토글**

```js
function current() {
  var stored = null;
  try { stored = localStorage.getItem("theme"); } catch (e) {}
  if (stored) return stored;                       // 예전에 고른 게 있으면 그거
  return window.matchMedia("(prefers-color-scheme: dark)").matches
    ? "dark" : "light";                            // 없으면 OS 설정 따라감
}
```

우선순위가 **저장된 선택 > OS 설정**입니다. `localStorage`는 브라우저가
제공하는 작은 저장 공간이라, 한 번 고르면 다음에 다시 와도 기억합니다.

`apply()`는 세 가지를 동시에 바꿉니다 — `<html>`에 `data-theme` 속성을 붙이고
(§3.2의 CSS가 이걸 보고 색을 바꿉니다), 버튼 아이콘을 ☾ ↔ ☀ 로 바꾸고,
`aria-label`(스크린리더가 읽어주는 설명)도 갱신합니다.

**`try { ... } catch (e) {}`가 왜 붙어 있나:** 사파리 시크릿 모드처럼
저장소 접근을 막는 환경이 있는데, 거기서 `localStorage`를 그냥 부르면 에러가
납니다. 자바스크립트는 **에러가 나면 그 뒤 코드를 전부 중단**하기 때문에,
감싸지 않으면 시크릿 모드에서 테마 토글뿐 아니라 아래 ②③까지 다 죽습니다.

**② 연도 자동 갱신**

```js
document.getElementById("year").textContent = new Date().getFullYear();
```

푸터의 `© 2026`을 오늘 연도로 덮어씁니다. 해가 바뀌어도 손댈 일이 없습니다.

**③ 로고 폴백**

```js
img.addEventListener("error", function () {
  var tile = img.parentNode;
  tile.textContent = tile.getAttribute("data-mono") || "";
});
```

로고 이미지가 안 뜨면(파일명 오타, 파일 삭제 등) 그 자리에 §3.3에서 적어둔
`data-mono` 값(`UCL`, `SG`, `S&K`, `ROK`, `DK`)을 글자로 채웁니다.
깨진 이미지 아이콘이 뜨는 것보다 훨씬 낫습니다.

---

## 4. 실제로 고칠 때

### 작업 방법

```bash
open index.html          # 브라우저로 열기 (미리보기)
```

에디터에서 고치고 저장 → 브라우저에서 ⌘R. 끝입니다. 로컬 서버도 필요 없습니다.
(단, 카톡 미리보기는 실제 배포된 URL을 참조하므로 로컬에서는 확인이 안 됩니다.)

### 자주 하게 될 수정

| 하고 싶은 것 | 어디를 고치나 |
| --- | --- |
| 자기소개 문구 | `<p class="bio">` 두 문단 ([index.html:372-384](index.html#L372-L384)) — ⚠️ `description`·`og:description`도 같이 |
| 경력 추가 | `#experience` 안에 `.item` 블록 복붙 (§3.3) |
| 프로젝트 추가 | `#projects` 안에 `.item` 블록 복붙 (로고 없는 버전) |
| 색·다크모드 톤 | 맨 위 `:root` 변수 블록만 |
| 본문 폭 | `--measure` 값 (46rem → 크게/작게) |
| 새 로고 추가 | `logos/`에 파일 넣고 → `<img src>` · `alt` · `data-mono` 세 개 갱신 |
| 카톡 미리보기 그림 | `og-image.png`를 1200×630으로 교체 |
| 이메일·링크드인 | `#contact` 섹션 + `<head>`의 JSON-LD |

### 고칠 때 주의할 것

- **HTML에서 `<` `>` `&`는 특수문자입니다.** 글자로 쓰려면 `&amp;`처럼 써야
  합니다. 그래서 코드에 `Shin &amp; Kim LLC`라고 적혀 있습니다. 화면에는
  `Shin & Kim LLC`로 나옵니다.
- **여는 태그와 닫는 태그는 짝**입니다. `<div>` 하나를 지웠는데 `</div>`가
  남으면 레이아웃이 무너집니다. 항목을 지울 땐 `.item` 블록 전체를 통으로
  지우세요.
- **CSS는 위에서 아래로 읽히고, 나중 것이 이깁니다.** 새 규칙은 관련 구획
  주석 아래에 넣는 게 안전합니다.

---

## 5. 배포 — 푸시하면 끝

GitHub Pages가 `main` 브랜치의 루트 폴더를 **그대로** 인터넷에 내보냅니다.
그래서 별도 배포 명령이 없습니다. **푸시가 곧 배포입니다.**

```bash
git pull                                    # 다른 데서 고친 게 있을 수 있으니
# ... index.html 수정 ...
git add -A
git commit -m "무엇을 왜 바꿨는지"
git push
```

약 1분 뒤 https://yjchoi.dev 에 반영됩니다.

**자주 겪는 일:** 미리보기 이미지나 설명을 바꿨는데 카톡·링크드인에서
옛날 게 계속 나옵니다. 배포가 안 된 게 아니라 **각 플랫폼이 미리보기를
캐시해 두기 때문**입니다. 링크드인은 Post Inspector, 페이스북은
Sharing Debugger에서 강제로 다시 긁어오게 할 수 있습니다.

---

## 6. 설계 원칙 (왜 이렇게 만들었나)

**정적 HTML 한 장.** 프레임워크를 쓰면 안 건드리는 사이에 의존성이 낡고,
한 줄 고치려다 빌드부터 고쳐야 합니다. 여기엔 고장 날 것이 없습니다.

**외부 요청 0건.** 구글 폰트나 CDN을 부르는 순간 방문자의 IP가 남의 서버로
갑니다. 시스템에 이미 깔린 폰트(`ui-sans-serif`, 한글은 `Apple SD Gothic Neo`
/ `Noto Sans KR`)만 쓰면 그럴 일도 없고, 다운로드가 없으니 더 빠릅니다.
분석 스크립트도 없습니다.

**보이는 건 미니멀하게, 안 보이는 건 꼼꼼하게.** 화면은 흑백에 가깝고 장식이
거의 없지만, `<head>`의 메타데이터·JSON-LD·OG 태그는 꽉 채웠습니다.
개인 홈페이지의 실제 목적은 예쁜 게 아니라 **검색됐을 때 제대로 뜨는 것**이라서.

**접근성 기본은 지킴.** 모든 이미지에 `alt`, 다크모드 버튼에 `aria-label`,
의미에 맞는 태그(`nav`/`header`/`section`/`footer`) 사용.

---

## 7. 이력

이 저장소에는 원래 [al-folio](https://github.com/alshedivat/al-folio) 기반의
Jekyll 사이트가 있었습니다. 그 버전과 MIT 라이선스는
`Replace al-folio with a single static page` 커밋 **이전**의 git 히스토리에
그대로 남아 있습니다. 필요하면 언제든 꺼내 볼 수 있습니다.

```bash
git log --oneline | tail -20     # 초기 커밋들 보기
```
