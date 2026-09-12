# Assignment 02 - C01 22300133

## 학번 / 이름
- 학번: 22300133
- 이름: 김승현

## Assignment 02 수행 내용
w3schools의 [Same Page, Different Stylesheets](https://www.w3schools.com/css/demo_default.htm) 예제를 그대로 재현하는 과제입니다. 동일한 HTML 콘텐츠(헤더, 메뉴, 본문, 사이드바, 하단 영역)를 두고 서로 다른 CSS 파일(Stylesheet)을 적용해 같은 마크업이 얼마나 다르게 보일 수 있는지 실습했습니다.

- 원본 사이트의 실제 HTML/CSS 소스를 직접 확인(curl, 브라우저 스크린샷 비교)해서 `#top`, `#menubar`, `#main`, `#sidebar`, `#bottom` id 구조와 각 Stylesheet의 CSS를 그대로 재현
- 페이지마다 `<style>` 블록만 다르게 적용하고, 본문 HTML 구조는 페이지 간 동일하게 유지

## 각 페이지 설명 및 URL

| 페이지 | 설명 | URL |
|---|---|---|
| `style1.html` | 원본 데모의 기본(Stylesheet 1) 스타일 — 초록색 헤더 박스, 좌측 세로 메뉴, 우측 파란 사이드바, 하단 회색 바 | https://2026-oss-assign02-tau.vercel.app/style1.html |
| `style3.html` | Stylesheet 3 스타일 — 헤더 박스 없이 제목만 초록색, 메뉴가 가로로 나열되는 회색 버튼형, 사이드바는 연회색 박스 | https://2026-oss-assign02-tau.vercel.app/style3.html |
| `nostyle.html` | 스타일시트를 적용하지 않은 원본 HTML만의 모습 | https://2026-oss-assign02-tau.vercel.app/nostyle.html |

> 본 과제에서는 Stylesheet 1, 3과 No Stylesheet 세 가지만 구현했으며, Stylesheet 2·4는 범위에 포함하지 않았습니다.

## Vercel Deploy URL
https://vercel.com/molla4/2026-oss-assign02

---

## Weekly Review – Week 2

### Key Learning
1. HTML은 콘텐츠의 구조와 의미를 담당하고, CSS는 그 구조에 시각적 표현을 입히는 역할이라는 점을 실습으로 체감했다. 같은 HTML이라도 CSS만 바꾸면 완전히 다른 페이지처럼 보일 수 있었다.
2. `id`와 `class` 선택자를 어떻게 설계하느냐에 따라 같은 마크업을 여러 스타일로 재사용할 수 있다는 것을 배웠다 (`#top`, `#menubar`, `#main`, `#sidebar`, `#bottom` 구조를 그대로 두고 CSS만 교체).
3. `float`, `position: absolute`, 미디어 쿼리(`@media`)를 조합해 사이드바·메뉴 레이아웃을 잡는 방식과, HTML 태그가 짝이 안 맞으면(예: 열리지 않은 `</main>`) CSS가 정상인데도 레이아웃이 깨질 수 있다는 점을 알게 되었다.

### HTML vs CSS
HTML은 "무엇이 있는가"(제목, 목록, 문단, 사이드바 등 콘텐츠의 구조와 의미)를 정의하고, CSS는 "어떻게 보이는가"(색상, 배치, 크기, 여백 등 표현)를 정의한다. 같은 HTML 구조를 유지한 채 CSS 파일만 바꿔 끼우는 이번 과제를 통해 이 둘의 역할 분리가 왜 중요한지 직접 확인했다.

### Problem & Solution
- **문제:** `style1.html`의 CSS에는 `#top`, `#sidebar`, `#bottom` 스타일이 이미 정의되어 있었지만, 실제 HTML에는 그 id들이 쓰이지 않았고(`<main>` 닫는 태그가 짝이 안 맞고, `<No>`라는 존재하지 않는 태그까지 있었음) `#menubar`에 필요한 `float` 규칙도 CSS에서 통째로 빠져 있어 화면이 원본과 다르게 렌더링되었다. `style3.html`에서도 메뉴 항목 개수를 줄인 뒤 `:nth-child` 강조 규칙을 안 맞춰서 엉뚱한 메뉴 항목이 강조되는 문제가 있었다.
- **해결:** w3schools 원본 페이지를 브라우저로 직접 열어 실제 CSS/HTML 소스를 확인한 뒤, 빠진 CSS 규칙(`#menubar { float: left; width:200px }`, `.menuitem:hover`, `a`/`a:hover`, 반응형 미디어 쿼리 등)을 추가하고, HTML을 `#top`/`#menubar`/`#main`/`#sidebar`/`#bottom` 구조로 다시 정리해 해결했다. 메뉴 항목을 줄인 뒤에는 `:nth-child` 순번도 실제 위치에 맞게 다시 계산해서 고쳤다. 수정 후 로컬 서버를 띄워 원본과 스크린샷으로 비교해 동일한지 검증했다.

### AI Usage
- Claude Code에게 구조가 안 맞아서  개발자 툴에서 가져온 것을 바탕으로 이게 왜 연동이 왜 이렇게 되는지 비교 하고 내가 직접 짠 코드와 비교하는 것을 물어 보았다
- AI가 제안한 CSS/HTML 수정 내용은 로컬 HTTP 서버로 페이지를 띄워 스크린샷을 원본과 나란히 비교해 육안으로 검증했고, `style3.html`은 원본 사이트에 내장된 4개의 `<style>` 블록 중 실제 "Stylesheet 3" 블록 텍스트를 그대로 가져온 것인지 코드 diff로 직접 확인했다.
- 즉, AI에게 전체 코드를 맡기기보다 "원본과 실제로 일치하는지"를 매 단계 스크린샷·소스 비교로 검증하는 방식으로 활용했다.

### Reflection
w3schools 데모 페이지가 별도의 CSS 파일 4개를 두고 JS로 파일을 바꿔 끼우는 방식이 아니라, `<style>` 태그 4개를 한 문서 안에 모두 넣어두고 `document.styleSheets[n].disabled`로 켜고 끄는 방식이라는 걸 소스를 직접 열어보고 나서야 알게 됐다. 겉보기엔 "페이지가 바뀐다"처럼 보여도 실제 구현 방식은 예상과 달랐던 점이 흥미로웠고, 앞으로는 동작을 추측하기보다 실제 소스를 먼저 확인하는 습관을 들여야겠다고 느꼈다.
