# Default

Default는 중립적인 흰색·회색 화면에 파스텔 연두색을 포인트로 사용해 편안하고 부드러운 인상을 주는 Okerry UI의 기준 컨셉입니다. 읽기 쉬운 간격과 명확한 상태 표현을 유지해 관리자 화면부터 일반 웹 페이지까지 범용적으로 적용할 수 있습니다.

## 디자인 원칙

- 배경과 기본 UI는 중립적인 흰색·회색 계열을 사용합니다.
- 채도가 낮은 파스텔 연두색은 주요 액션과 강조 요소에만 사용합니다.
- 밝은 녹색 위에서도 충분히 읽히도록 주요 버튼에는 짙은 녹색 텍스트를 사용합니다.
- 작은 화면에서도 동일한 정보 위계를 유지합니다.
- 버튼, 입력, 카드 등 기본 컴포넌트의 시각적 일관성을 우선합니다.
- CSS 변수로 색상, 간격, radius, shadow를 조정할 수 있습니다.
- JavaScript와 외부 에셋에 의존하지 않습니다.

## 버전

| 버전 | CSS | 예제 |
| --- | --- | --- |
| v1.0.0 | [`okerry-ui.css`](v1.0.0/okerry-ui.css) | [`examples/index.html`](v1.0.0/examples/index.html) |

각 버전 디렉터리는 독립적으로 사용할 수 있는 `okerry-ui.css`와 해당 CSS를 확인하는 `examples/index.html`을 포함합니다.
예제 페이지 상단의 라이트 모드·다크 모드 버튼으로 전체 컴포넌트의 테마를 즉시 비교할 수 있습니다. 이 버튼의 스크립트는 예제 전환용이며 `okerry-ui.css` 자체에는 JavaScript 의존성이 없습니다.

## 라이트 및 다크 모드

라이트·다크 스타일은 하나의 CSS에 포함됩니다. 별도의 테마 CSS를 추가로 불러올 필요가 없습니다.

테마 속성이 없으면 브라우저의 `prefers-color-scheme` 설정을 자동으로 따릅니다.

```html
<html>
```

특정 모드로 고정하려면 최상위 요소에 `data-okerry-theme`을 지정합니다.

```html
<!-- 라이트 모드 고정 -->
<html data-okerry-theme="light">

<!-- 다크 모드 고정 -->
<html data-okerry-theme="dark">
```

페이지 일부에만 테마를 적용할 수도 있습니다.

```html
<section class="okerry_ui" data-okerry-theme="dark">
  <div class="okerry-card">
    <div class="okerry-card-body">다크 모드 카드</div>
  </div>
</section>
```

Okerry UI는 속성에 맞는 스타일을 제공합니다. 실행 중 모드를 전환하거나 사용자의 선택을 저장하는 로직은 사용하는 프로젝트에서 구현해야 합니다.

## 사용법

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/youngheonchoi/okerry_ui@main/concept/default/v1.0.0/okerry-ui.css">
```

배포 태그로 저장소 상태까지 고정하려면 다음과 같이 사용합니다.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/youngheonchoi/okerry_ui@v1.0.0/concept/default/v1.0.0/okerry-ui.css">
```

```html
<button class="okerry-btn okerry-btn-primary">저장</button>
<input class="okerry-input" placeholder="이름">
<div class="okerry-card">
  <div class="okerry-card-body">카드 내용</div>
</div>
```

## 커스터마이징

CSS를 불러온 다음 변수를 덮어쓸 수 있습니다.

```css
:root,
[data-okerry-theme="light"] {
  --okerry-color-primary: #7c3aed;
  --okerry-color-primary-hover: #6d28d9;
  --okerry-radius-md: 12px;
}

[data-okerry-theme="dark"] {
  --okerry-color-primary: #8b5cf6;
  --okerry-color-primary-hover: #7c3aed;
}
```
