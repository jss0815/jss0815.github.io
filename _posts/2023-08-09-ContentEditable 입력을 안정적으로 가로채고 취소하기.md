---
title: ContentEditable 입력을 안정적으로 가로채고 취소하기
date: 2023-08-09 20:00:00 +0900
categories:
  - JavaScript
tags:
  - ContentEditable
---

## 문제 상황과 요구 사항

사용자가 웹 페이지에서 `contenteditable` 속성을 갖는 요소를 사용할 때, 모든 입력을 가로채거나 취소하는 방법이 필요합니다. 이것은 보통 웹 개발자가 사용자의 입력을 특정 조건에 맞게 제한하려고 할 때 유용하게 쓰입니다.

## JavaScript를 이용한 해결 방법

### 이벤트 리스너 활용

`contenteditable` 속성을 가진 요소에 대한 입력을 가로채거나 취소하려면, JavaScript의 `addEventListener` 메서드를 사용하여 이벤트를 감지하고 처리해야 합니다. 이 경우, 가장 적합한 이벤트는 `keydown` 이벤트입니다.

```javascript
const editableElement = document.querySelector('[contenteditable=true]');
editableElement.addEventListener('keydown', function(event) {
  // 코드 로직 작성
});
```

### 입력 취소하기

`keydown` 이벤트 내에서 입력을 취소하려면, `Event` 객체의 `preventDefault` 메서드를 호출해야 합니다.

```javascript
editableElement.addEventListener('keydown', function(event) {
  event.preventDefault();
});
```

이렇게 하면, `contenteditable` 요소에 대한 모든 키 입력이 취소됩니다.

## 주의 사항

### 다른 이벤트에 영향을 줄 수 있음

이 방법을 사용하면, 해당 요소에서 발생하는 다른 이벤트에도 영향을 줄 수 있습니다. 예를 들어, 복사와 붙여넣기 같은 클립보드 이벤트가 정상적으로 동작하지 않을 수 있습니다.

### 브라우저 호환성

대부분의 현대 브라우저에서는 `addEventListener`와 `preventDefault` 메서드를 지원하지만, 오래된 브라우저에서는 동작하지 않을 수 있으므로 테스트가 필요합니다.

## 결론

`contenteditable` 속성을 가진 요소에서 입력을 가로채거나 취소하려면, JavaScript의 `keydown` 이벤트와 `preventDefault` 메서드를 사용하면 됩니다. 하지만 이 방법은 다른 이벤트에 영향을 줄 수 있으므로 주의가 필요합니다.