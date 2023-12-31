---
title: 자바스크립트 Promise에서 resolve와 reject 메소드 다루기
date: 2023-09-24 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트
---

## `resolve`와 `reject`의 기본 원리

자바스크립트에서 `Promise`는 비동기 작업을 쉽게 다루기 위해 사용됩니다. `resolve` 메소드는 작업이 성공적으로 완료되었을 때 호출되며, `reject`는 작업이 실패했을 때 호출됩니다. 이 두 메소드는 Promise 객체 내부에서 정의되어 있으며, `.then()` 또는 `.catch()` 메소드로 결과를 받을 수 있습니다.

## 주의사항

이 두 메소드는 Promise 객체 내부에서만 사용되어야 합니다. 외부에서 이 메소드를 직접 호출하면 예기치 않은 동작이 발생할 수 있습니다.

## 해결 방법

1. **함수 스코프 확인**: `resolve`와 `reject`를 호출하는 위치가 Promise 생성자 내부인지 확인하세요.
  
2. **비동기 작업 상태 체크**: 비동기 작업이 완료되었는지, 아니면 에러가 발생했는지 확인 후에 `resolve` 또는 `reject`를 호출하세요.

3. **메소드 철자와 대소문자 확인**: 자바스크립트는 대소문자를 구분합니다. `Resolve`나 `Reject`와 같이 철자나 대소문자를 잘못 입력하면 `TypeError`가 발생할 수 있습니다.

4. **함수 호출 형식 확인**: `resolve`와 `reject`는 함수이므로 괄호(`()`)를 이용해 호출해야 합니다.

5. **에러 추적**: 콘솔에 출력되는 에러 메시지를 자세히 분석하여 문제를 해결하세요.

이러한 방법을 통해 `resolve`와 `reject` 메소드를 올바르게 다루어 문제를 해결할 수 있습니다.