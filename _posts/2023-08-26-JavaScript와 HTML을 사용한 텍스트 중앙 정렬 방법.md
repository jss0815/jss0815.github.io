---
title: JavaScript와 HTML을 사용한 텍스트 중앙 정렬 방법
date: 2023-08-26 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트
  - html
---

## 문제 상황과 에러 코드

"Centering JavaScript HTML text 50-50 width"라는 제목으로 StackOverflow에 게시된 문제에서 사용자는 HTML과 JavaScript를 사용하여 텍스트를 화면 가운데로 정렬하려고 합니다. 에러 코드는 특별히 명시되어 있지 않습니다.

## CSS를 이용한 가장 간단한 방법

텍스트를 화면 가운데로 정렬하는 가장 간단한 방법은 CSS를 사용하는 것입니다. 여기에서는 `text-align: center;`과 `margin: auto;`를 활용할 수 있습니다.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .center-text {
      text-align: center;
      margin: auto;
    }
  </style>
</head>
<body>

<div class="center-text">
  이 텍스트는 가운데 정렬됩니다.
</div>

</body>
</html>
```

## JavaScript를 사용한 동적 중앙 정렬

JavaScript를 사용해 동적으로 텍스트를 중앙에 배치할 수도 있습니다. `getElementById` 함수를 사용하여 특정 요소를 선택한 후, `style` 속성을 변경하면 됩니다.

```javascript
document.getElementById("myText").style.textAlign = "center";
document.getElementById("myText").style.margin = "auto";
```

## Flexbox를 활용한 중앙 정렬

Flexbox는 레이아웃, 방향, 정렬 등을 한 번에 처리할 수 있는 편리한 방법입니다. Flexbox를 사용하면 아래와 같이 쉽게 중앙 정렬을 할 수 있습니다.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .center-flex {
      display: flex;
      justify-content: center;
      align-items: center;
    }
  </style>
</head>
<body>

<div class="center-flex">
  이 텍스트는 가운데 정렬됩니다.
</div>

</body>
</html>
```

## 정리

텍스트를 중앙에 정렬하는 방법은 여러 가지가 있습니다. 가장 간단한 방법은 CSS만을 사용하는 것이지만, JavaScript를 활용하거나 Flexbox를 이용할 수도 있습니다. 요구사항에 따라 가장 적합한 방법을 선택하면 됩니다.