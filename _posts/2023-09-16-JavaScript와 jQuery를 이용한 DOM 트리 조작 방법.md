---
title: JavaScript와 jQuery를 이용한 DOM 트리 조작 방법
date: 2023-09-16 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트
  - JQUERY
---

## DOM 트리란 무엇인가?

DOM(Document Object Model) 트리는 웹 페이지의 구조를 나타내는 객체 모델입니다. HTML 문서가 웹 브라우저에 로드될 때, 브라우저는 이 문서를 DOM 트리로 변환합니다. 이 트리는 웹 페이지의 각 요소를 객체로 표현하며, 자바스크립트를 사용하여 이 객체를 조작할 수 있습니다.

## 화면에 표시되기 전에 DOM 조작하기

화면에 렌더링 되기 전에 DOM을 조작하는 것은 어렵지 않습니다. 여러 방법이 있지만, 가장 흔히 사용되는 두 가지 방법을 소개합니다.

### JavaScript를 사용한 방법

1. `DOMContentLoaded` 이벤트를 활용합니다. 이 이벤트는 HTML 문서가 완전히 로드되고 난 후에 발생합니다.
```javascript
document.addEventListener('DOMContentLoaded', function() {
    // 여기에 DOM을 조작하는 코드를 작성
});
```

### jQuery를 사용한 방법

1. jQuery의 `$(document).ready()` 함수를 사용합니다. 이 함수는 DOM이 준비되면 실행되는 코드 블록을 정의합니다.
```javascript
$(document).ready(function(){
    // 여기에 DOM을 조작하는 코드를 작성
});
```

## 주의사항: `DOMContentLoaded`와 `$(document).ready()`의 차이점

`DOMContentLoaded`는 순수 자바스크립트에서 사용되는 이벤트로, HTML과 스크립트 파일만 로드되면 실행됩니다. 반면, jQuery의 `$(document).ready()`는 이미지와 같은 다른 리소스까지 모두 로드된 후에 실행됩니다. 따라서 두 방법은 약간의 차이가 있으니 목적에 맞게 사용하세요.

## 실용적인 예시: 화면에 표시되기 전에 요소 추가하기

DOM이 완전히 로드되기 전에 요소를 추가하려면 다음과 같은 코드를 사용할 수 있습니다.
```javascript
document.addEventListener('DOMContentLoaded', function() {
    let newElement = document.createElement('div');
    newElement.innerHTML = '새로운 내용';
    document.body.appendChild(newElement);
});
```

이 글은 StackOverflow의 "How to manipulate a DOM tree before it is displayed on screen (JavaScript, jQuery)" 질문을 바탕으로 작성되었습니다. 원문에서는 `$(document).ready()`와 `window.onload`를 이용한 방법도 다루고 있지만, 여기에서는 두 가장 기본적인 방법을 중점으로 설명했습니다.