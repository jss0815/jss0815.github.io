---
title: 자바스크립트에서 display none과 display block 사이에 전환 효과 적용하기
date: 2023-08-05 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트
  - display전환효과
---

## 문제 상황 설명

자바스크립트에서 웹 페이지의 요소(element)를 보이게 하거나 숨기려면 `display` 속성을 `none` 또는 `block`으로 변경합니다. 그런데 이렇게 하면 웹 요소가 갑자기 나타나거나 사라져서 자연스럽지 않습니다. 여기서는 `display:none`과 `display:block` 사이에 부드러운 전환 효과(transition)를 적용하는 방법을 자세히 알아보겠습니다.

## CSS `opacity`와 `visibility`를 사용한 해결 방법

`display` 속성은 CSS 전환 효과와 함께 작동하지 않습니다. 그래서 다른 속성을 사용해야 합니다. `opacity`와 `visibility` 속성을 조합하여 이 문제를 해결할 수 있습니다. 먼저, 원하는 요소에 다음과 같은 CSS를 적용합니다.

```css
.fade {
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.5s, visibility 0.5s;
}
```

그런 다음, 자바스크립트로 이 클래스를 추가하거나 제거합니다.

```javascript
// 요소를 보이게 하기
document.getElementById("myElement").classList.remove("fade");

// 요소를 숨기기
document.getElementById("myElement").classList.add("fade");
```

## JavaScript `setTimeout` 함수를 이용한 방법

`setTimeout` 함수를 사용하여 일정 시간 후에 `display` 속성을 변경할 수도 있습니다. 이렇게 하면 `opacity`가 완전히 사라진 후에 `display:none`을 적용할 수 있습니다.

```javascript
// 요소를 보이게 하기
document.getElementById("myElement").style.opacity = "1";
setTimeout(function() {
  document.getElementById("myElement").style.display = "block";
}, 500); // 0.5초 후에 실행

// 요소를 숨기기
document.getElementById("myElement").style.opacity = "0";
setTimeout(function() {
  document.getElementById("myElement").style.display = "none";
}, 500); // 0.5초 후에 실행
```

## 요약

웹 페이지에서 요소를 부드럽게 보이게 하거나 숨기려면 `display` 속성만으로는 부족합니다. `opacity`와 `visibility` 속성을 활용하거나 JavaScript의 `setTimeout` 함수를 사용하여 자연스러운 전환 효과를 만들 수 있습니다. 이러한 방법들은 사용자 경험을 향상시키는 데 큰 도움이 됩니다.