# Okerry UI Agent Guide

이 문서는 코딩 에이전트가 다른 프로젝트에서 Okerry UI를 일관되게 적용하기 위한 작업 명세입니다.

## 목적

Okerry UI는 npm 설치나 빌드 없이 CDN `<link>` 하나로 사용하는 순수 CSS 컴포넌트 라이브러리다. HTML, Thymeleaf, JSP, Spring MVC, 정적 페이지에서 같은 클래스 API를 사용한다.

## 기본 선택

사용자가 별도의 컨셉이나 버전을 지정하지 않으면 다음을 사용한다.

- 컨셉: `default`
- 버전: `v1.0.0`
- CSS 파일: `concept/default/v1.0.0/okerry-ui.css`
- 컴포넌트 예제: `concept/default/v1.0.0/examples/index.html`
- 컨셉 문서: `concept/default/README.md`

Default 컨셉은 흰색·회색의 중립적인 화면에 파스텔 연두색을 포인트로 사용한다.

## CDN 연결

Okerry UI를 연결할 때는 `main` 브랜치와 컨셉 버전 디렉터리를 사용하는 다음 URL을 기본으로 한다.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/youngheonchoi/okerry_ui@main/concept/default/v1.0.0/okerry-ui.css">
```

CSS 링크는 문서의 `<head>`에 한 번만 추가한다. npm 패키지, JavaScript 번들 또는 외부 폰트는 필요하지 않다.

## 테마

`data-okerry-theme`이 없으면 운영체제의 `prefers-color-scheme` 설정을 따른다.

```html
<html>
```

테마를 고정할 때는 최상위 요소에 다음 중 하나를 지정한다.

```html
<html data-okerry-theme="light">
<html data-okerry-theme="dark">
```

페이지 일부에만 테마를 적용할 때는 해당 영역에 속성과 `okerry_ui` 클래스를 함께 사용한다.

```html
<section class="okerry_ui" data-okerry-theme="dark">
  <div class="okerry-card">
    <div class="okerry-card-body">내용</div>
  </div>
</section>
```

Okerry UI는 테마 스타일만 제공한다. 실행 중 테마 전환과 사용자 선택 저장은 사용하는 프로젝트에서 구현한다.

## 기본 사용 패턴

```html
<div class="okerry_ui">
  <div class="okerry-field">
    <label class="okerry-label" for="project-name">프로젝트 이름</label>
    <input id="project-name" class="okerry-input" type="text">
    <p class="okerry-help-text">사용할 이름을 입력하세요.</p>
  </div>

  <button class="okerry-btn okerry-btn-primary" type="button">저장</button>
</div>
```

컴포넌트는 기본 클래스와 variant 또는 size 클래스를 조합한다. 예를 들어 버튼에는 `okerry-btn`을 반드시 포함하고 `okerry-btn-primary`만 단독으로 사용하지 않는다.

## 클래스 API

- 버튼: `okerry-btn`, `okerry-btn-primary`, `okerry-btn-secondary`, `okerry-btn-danger`, `okerry-btn-ghost`, `okerry-btn-sm`, `okerry-btn-lg`, `okerry-btn-full`
- 입력: `okerry-field`, `okerry-label`, `okerry-input`, `okerry-input-error`, `okerry-textarea`, `okerry-select`, `okerry-help-text`, `okerry-error-text`
- 카드: `okerry-card`, `okerry-card-header`, `okerry-card-body`, `okerry-card-footer`, `okerry-card-title`, `okerry-card-description`
- 레이아웃: `okerry-container`, `okerry-section`, `okerry-stack`, `okerry-row`, `okerry-between`, `okerry-center`, `okerry-grid`, `okerry-grid-2`, `okerry-grid-3`
- 텍스트: `okerry-title-2xl`, `okerry-title-xl`, `okerry-title-lg`, `okerry-text`, `okerry-text-muted`, `okerry-caption`
- 배지: `okerry-badge`, `okerry-badge-primary`, `okerry-badge-success`, `okerry-badge-warning`, `okerry-badge-danger`
- 알림: `okerry-alert`, `okerry-alert-success`, `okerry-alert-warning`, `okerry-alert-danger`, `okerry-alert-info`
- 빈 화면: `okerry-empty`, `okerry-empty-title`, `okerry-empty-description`
- 로딩: `okerry-spinner`, `okerry-skeleton`

전체 조합과 상태는 해당 버전의 `examples/index.html`을 기준으로 확인한다.

## 구현 규칙

- 기존 Okerry UI 클래스가 제공하는 기능을 인라인 스타일이나 중복 프로젝트 CSS로 다시 만들지 않는다.
- `.btn`, `.card`, `.container`처럼 접두사 없는 대체 클래스를 만들지 않는다.
- Okerry UI 클래스 이름이나 내부 CSS를 임의로 변경하지 않는다.
- 프로젝트 전용 스타일이 필요하면 별도 클래스에 작성하고 Okerry UI를 불러온 뒤 적용한다.
- 색상과 간격을 변경할 때는 컴포넌트 규칙을 복사하지 말고 `--okerry-*` CSS 변수를 덮어쓴다.
- 접근성을 위해 `label`과 입력의 `for`/`id`, 버튼의 `type`, 로딩 상태의 대체 텍스트를 제공한다.
- 반응형 레이아웃은 먼저 `okerry-grid-2`, `okerry-grid-3`, `okerry-between`을 사용한다.
- 존재하지 않는 클래스를 추측하지 않는다. 클래스 API나 예제에 없으면 CSS 파일에서 확인한다.

## 커스터마이징

프로젝트 CSS에서 필요한 테마 범위의 변수를 덮어쓴다.

```css
:root,
[data-okerry-theme="light"] {
  --okerry-color-primary: #d9f4df;
  --okerry-color-primary-hover: #c2eacb;
}

[data-okerry-theme="dark"] {
  --okerry-color-primary: #95d5b2;
  --okerry-color-primary-hover: #74c69d;
}
```

## 작업 전 확인 순서

1. 사용자가 요청한 컨셉과 버전을 확인한다.
2. 지정이 없으면 Default v1.0.0을 선택한다.
3. 컨셉 README와 해당 버전의 examples를 확인한다.
4. CDN 링크가 한 번만 연결됐는지 확인한다.
5. 기존 클래스 조합으로 UI를 구현한다.
6. 라이트·다크 모드와 768px 이하 화면을 확인한다.
