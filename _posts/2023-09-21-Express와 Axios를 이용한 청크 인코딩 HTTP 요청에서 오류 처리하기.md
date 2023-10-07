---
title: Express와 Axios를 이용한 청크 인코딩 HTTP 요청에서 오류 처리하기
date: 2023-09-21 20:00:00 +0900
categories:
  - JavaScript
tags:
  - HTTP프로토콜
  - Axios
  - Express
---

## 들어가며: 청크 인코딩 HTTP 요청이란?

HTTP 프로토콜을 이용해 서버와 클라이언트가 데이터를 주고받을 때, 전체 데이터를 한 번에 보내지 않고 여러 개의 "청크(조각)"로 나눠서 보내는 방식을 청크 인코딩(HTTP Chunked Transfer Encoding)이라고 합니다. 이 방식은 대용량 데이터를 효율적으로 처리할 수 있습니다.

## 오류 상황: `Transfer-Encoding: chunked`와 관련된 문제점

StackOverflow에 올라온 질문에서는 Express와 Axios를 이용하여 청크 인코딩 방식으로 HTTP 요청을 처리하면서 오류가 발생했습니다. 구체적으로는 `Transfer-Encoding: chunked` 헤더를 사용하면서, 서버나 클라이언트 측에서 어떻게 오류를 처리해야 하는지에 대한 문제였습니다.

## 오류명: `ERR_HTTP_HEADERS_SENT`

오류가 발생할 때 나타나는 오류 코드는 `ERR_HTTP_HEADERS_SENT`입니다. 이 오류는 HTTP 헤더가 이미 전송된 후에 다시 헤더를 수정하거나 추가하려고 할 때 발생합니다.

## 해결 방법: Express와 Axios에서의 오류 처리

### Express에서의 오류 처리

1. **미들웨어 활용**: Express에서는 `next()` 함수를 이용해 미들웨어를 통과시키고, 오류를 다음 미들웨어로 넘길 수 있습니다.
2. **에러 핸들링 미들웨어**: 특별한 형태의 미들웨어로서 4개의 인수를 받습니다. 이를 통해 오류를 캐치하고 처리할 수 있습니다.

```javascript
app.use((err, req, res, next) => {
  if (res.headersSent) {
    return next(err);
  }
  res.status(500).send('Internal Server Error');
});
```

### Axios에서의 오류 처리

1. **`catch` 블록 사용**: Promise 기반의 Axios에서는 `.catch()` 를 이용해 오류를 잡을 수 있습니다.
2. **응답 상태 코드 확인**: Axios 요청에서 반환되는 `response` 객체에는 HTTP 상태 코드가 포함되어 있습니다. 이를 통해 오류를 판별할 수 있습니다.

```javascript
axios.post('/some-api-endpoint', payload)
  .then(response => {
    // 성공 시의 처리
  })
  .catch(error => {
    if (error.response) {
      // 서버에서 반환한 상태 코드와 문제점을 확인
      console.error(`Error: ${error.response.status}`);
    } else {
      // 그 외의 오류 처리
      console.error('An unknown error occurred');
    }
  });
```

## 결론: 철저한 오류 처리가 필요하다

청크 인코딩 방식으로 HTTP 요청을 처리할 때는 주의가 필요합니다. Express와 Axios 모두 강력한 오류 처리 메커니즘이 있지만, 이를 올바르게 활용하지 않으면 `ERR_HTTP_HEADERS_SENT`와 같은 문제가 발생할 수 있습니다. 따라서, 신중한 오류 처리 로직을 구현해야 합니다.