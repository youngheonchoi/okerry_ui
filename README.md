# Okerry UI

Okerry UI는 여러 디자인 컨셉을 제공하는 CDN 전용 CSS 컴포넌트 라이브러리입니다. npm, 빌드 도구, JavaScript, 외부 폰트 없이 HTML, Thymeleaf, JSP 등에서 `<link>` 하나로 사용할 수 있습니다.

코딩 에이전트가 Okerry UI를 적용할 때는 [AGENTS.md](AGENTS.md)의 선택 기준, 클래스 API, 테마 및 구현 규칙을 우선 확인합니다.

## 디렉터리 구조

```text
concept/
  default/
    README.md
    v1.0.0/
      okerry-ui.css
      examples/
        index.html
```

- `concept/<컨셉>/README.md`: 컨셉의 디자인 방향과 사용법
- `concept/<컨셉>/<버전>/okerry-ui.css`: CDN에서 불러오는 고정 이름 CSS
- `concept/<컨셉>/<버전>/examples/index.html`: 해당 버전 전용 컴포넌트 예제

CSS 파일명은 모든 컨셉과 버전에서 `okerry-ui.css`로 고정하며 컨셉과 버전은 디렉터리 경로로 구분합니다. 각 CSS에는 해당 컨셉의 라이트 모드와 다크 모드가 함께 포함됩니다.

## 제공 컨셉

| 컨셉 | 설명 | 버전 | 문서 |
| --- | --- | --- | --- |
| Default | 중립적인 화면에 파스텔 연두색 포인트를 사용하는 범용 컨셉 | v1.0.0 | [Default 문서](concept/default/README.md) |

현재는 Default 컨셉만 제공합니다. 이후 컨셉은 `concept/` 아래에 독립된 디렉터리로 추가합니다.

## CDN 사용

최신 저장소 기준:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/youngheonchoi/okerry_ui@main/concept/default/v1.0.0/okerry-ui.css">
```

## 테마 모드

속성을 지정하지 않으면 운영체제의 라이트·다크 설정을 자동으로 따릅니다. 모드를 고정할 때는 `data-okerry-theme`을 사용합니다.

```html
<!-- 시스템 설정 자동 감지 -->
<html>

<!-- 라이트 모드 고정 -->
<html data-okerry-theme="light">

<!-- 다크 모드 고정 -->
<html data-okerry-theme="dark">
```

JavaScript 의존성은 없습니다. 실행 중 전환이 필요하면 사용하는 프로젝트에서 `<html>`의 `data-okerry-theme` 값을 변경하면 됩니다. 컨셉별 색상과 커스터마이징 변수는 각 컨셉 README에서 확인할 수 있습니다.

## 사용 예시

일반 HTML:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/youngheonchoi/okerry_ui@main/concept/default/v1.0.0/okerry-ui.css">
<button class="okerry-btn okerry-btn-primary">저장</button>
```

Thymeleaf:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/youngheonchoi/okerry_ui@main/concept/default/v1.0.0/okerry-ui.css">
<div class="okerry-card" th:text="${message}"></div>
```

JSP:

```jsp
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/youngheonchoi/okerry_ui@main/concept/default/v1.0.0/okerry-ui.css">
<button class="okerry-btn okerry-btn-primary">${buttonLabel}</button>
```

## 클래스 접두사

다른 CSS와의 충돌을 줄이기 위해 모든 컴포넌트 클래스는 `okerry-` 접두사를 사용합니다. 제한적인 `box-sizing` 적용이 필요하면 컴포넌트 영역을 `okerry_ui`로 감쌀 수 있습니다.

```html
<div class="okerry_ui">
  <input class="okerry-input" placeholder="이름">
</div>
```