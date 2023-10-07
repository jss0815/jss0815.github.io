---
title: TypeError 해결 Cannot read properties of undefined (reading passport)
date: 2023-08-17 20:00:00 +0900
categories:
  - JavaScript
tags:
  - NodeJS
  - TypeError
---

## 문제 개요

개발자들이 Node.js와 Passport를 사용하여 웹 애플리케이션을 만들 때 자주 마주치는 문제 중 하나는 `TypeError: Cannot read properties of undefined (reading 'passport')`라는 에러 메시지입니다. 이 문제는 Passport 라이브러리를 사용해 인증을 구현할 때 특히 자주 발생합니다. 

## 원인 파악

이 에러 메시지가 뜨는 주된 원인은 서버의 `req` (요청) 객체가 정의되지 않았거나 `passport` 정보를 정확하게 읽지 못한 것입니다. 다시 말해, 서버가 클라이언트로부터 정보를 받을 때 `req` 객체의 내부 정보가 비어 있거나 잘못되어 있어서 발생합니다.

## 해결 방안

### 초기 설정 확인

먼저, Passport를 설정할 때 필요한 초기 설정이 올바르게 되어 있는지 확인하세요. `passport.initialize()`와 `passport.session()` 미들웨어가 적용되어 있는지 점검하면 좋습니다.

```javascript
app.use(passport.initialize());
app.use(passport.session());
```

### 미들웨어 순서

Express 미들웨어가 실행되는 순서도 중요합니다. `app.use()`를 이용하여 미들웨어를 설정할 때, `passport.initialize()`와 `passport.session()`은 세션 설정 미들웨어 다음에 위치해야 합니다.

```javascript
app.use(session({ /* 세션 설정 */ }));
app.use(passport.initialize());
app.use(passport.session());
```

### 세션 설정

`express-session`을 사용한다면, 세션 설정이 올바르게 이루어졌는지 확인하세요. 특히 `secret`, `resave`, `saveUninitialized` 옵션을 주의깊게 살펴보세요.

```javascript
app.use(session({
  secret: 'your-secret-key',
  resave: false,
  saveUninitialized: true,
}));
```

## 정리

`TypeError: Cannot read properties of undefined (reading 'passport')` 에러는 주로 설정 오류나 미들웨어 순서 문제로 발생합니다. 초기 설정을 철저하게 확인하고, 필요한 미들웨어가 올바른 순서로 적용되었는지 확인하면 대부분의 문제를 해결할 수 있습니다.