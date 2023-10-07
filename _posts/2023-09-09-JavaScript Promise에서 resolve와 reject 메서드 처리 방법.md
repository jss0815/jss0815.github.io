---
title: JavaScript Promise에서 resolve와 reject 메서드 처리 방법
date: 2023-09-09 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트
  - promise
---

## 문제 상황 설명

문제의 원인은 StackOverflow의 질문에서 제기되었습니다. 사용자는 JavaScript에서 `Promise` 객체의 `resolve`와 `reject` 메서드를 제대로 다루지 못하고 있습니다. 코드에서 발생하는 오류는 `TypeError` 입니다.

## Promise의 기본 구조

먼저, `Promise` 객체는 JavaScript에서 비동기 작업을 수행하고 그 결과를 나중에 받아올 수 있도록 하는 객체입니다. 비동기란 여러 작업이 동시에 수행되는 것을 말합니다. `Promise` 객체는 보통 `resolve`와 `reject`라는 두 가지 메서드를 사용해 완료 또는 실패를 처리합니다.

## resolve와 reject 메서드의 역할

`resolve` 메서드는 `Promise`가 성공적으로 완료되었을 때 호출되며, `reject` 메서드는 `Promise`가 실패했을 때 호출됩니다. 이 두 메서드를 통해 이후에 `.then()`과 `.catch()`로 처리할 결과나 오류를 정의합니다.

## TypeError의 발생 원인과 해결법

질문에서 제시된 `TypeError`는 대부분 잘못된 메서드 호출 또는 객체 참조로 인해 발생합니다. 가장 먼저 확인해야 할 것은 `resolve`와 `reject` 메서드가 올바르게 호출되고 있는지입니다. 다음은 올바른 예시입니다.

```javascript
new Promise((resolve, reject) => {
  if (true) {
    resolve("성공");
  } else {
    reject("실패");
  }
});
```

만약 `resolve`와 `reject`가 올바르지 않은 문맥에서 호출되면 `TypeError`가 발생할 수 있습니다. 예를 들어, 함수의 스코프 밖에서 이 메서드들을 호출하면 문제가 발생할 것입니다.

## 마무리

`Promise`에서 `resolve`와 `reject` 메서드를 올바르게 사용하려면 먼저 메서드가 호출되는 문맥을 이해해야 합니다. 그리고 나서 올바른 구문과 로직을 적용해야 `TypeError`와 같은 오류를 피할 수 있습니다. 이러한 방법을 통해 비동기 프로그래밍에서 발생하는 다양한 문제를 더욱 효과적으로 해결할 수 있습니다.