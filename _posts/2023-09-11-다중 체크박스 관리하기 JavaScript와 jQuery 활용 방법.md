---
title: 다중 체크박스 관리하기 JavaScript와 jQuery 활용 방법
date: 2023-09-11 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트
  - JQUERY
---

## JavaScript를 이용한 다중 체크박스 처리

### 체크박스와 DOM 조작
웹 페이지에서 체크박스를 사용할 때는 JavaScript를 이용해서 Document Object Model(DOM, 웹 페이지의 구조를 표현하는 객체)을 조작합니다. 이렇게 하면 사용자의 동작에 따라 체크박스의 상태를 실시간으로 변경할 수 있습니다.

### 이벤트 리스너 활용
먼저, 체크박스 요소에 이벤트 리스너(Event Listener, 사용자의 액션을 감지하는 코드)를 추가합니다. `addEventListener` 메서드를 이용하면 됩니다.

```javascript
document.querySelector("#myCheckbox").addEventListener("change", function() {
  // 체크박스 상태 변경 시 수행할 작업
});
```

### 체크박스 상태 확인
체크박스가 선택되었는지 아닌지 확인하려면, `checked` 프로퍼티를 사용합니다.

```javascript
if(document.querySelector("#myCheckbox").checked) {
  // 체크박스가 선택된 경우
} else {
  // 체크박스가 선택되지 않은 경우
}
```

## jQuery를 이용한 다중 체크박스 처리

### jQuery 간략 소개
jQuery는 JavaScript 라이브러리로, DOM 조작이나 이벤트 처리 등을 더 쉽게 할 수 있도록 도와줍니다.

### 체크박스 선택
jQuery에서는 `$` 함수를 사용하여 체크박스를 선택할 수 있습니다.

```javascript
$("#myCheckbox")
```

### 이벤트 바인딩
이벤트 리스너를 추가하려면 `change` 이벤트와 `on` 메서드를 사용합니다.

```javascript
$("#myCheckbox").on("change", function() {
  // 체크박스 상태 변경 시 수행할 작업
});
```

### 상태 확인
`prop` 메서드를 이용하여 체크박스의 상태를 확인할 수 있습니다.

```javascript
if($("#myCheckbox").prop("checked")) {
  // 체크박스가 선택된 경우
} else {
  // 체크박스가 선택되지 않은 경우
}
```

이렇게 JavaScript와 jQuery를 활용하여 다중 체크박스를 효율적으로 관리할 수 있습니다. 어떤 방법을 선택할지는 프로젝트의 요구사항과 개발 환경에 따라 결정하면 됩니다.