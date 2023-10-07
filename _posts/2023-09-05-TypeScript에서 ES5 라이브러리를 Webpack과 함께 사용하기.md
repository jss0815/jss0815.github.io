---
title: TypeScript에서 ES5 라이브러리를 Webpack과 함께 사용하기
date: 2023-09-05 20:00:00 +0900
categories:
  - JavaScript
tags:
  - TypeScript
  - ES5라이브러리
  - Webpack
---

## 문제 개요

StackOverflow의 질문에 따르면, TypeScript와 Webpack 기반의 프로젝트에서 기존 ES5(ES2015 이전 버전)로 작성된 JavaScript 라이브러리를 임포트하려고 시도할 때 발생하는 문제가 있습니다. 특히, "ReferenceError: exports is not defined"라는 오류 메시지가 출력됩니다.

## ReferenceError: exports is not defined 오류 이해하기

이 오류는 JavaScript 런타임에서 "exports" 객체를 찾을 수 없다는 것을 나타냅니다. ES5 라이브러리가 CommonJS 모듈 시스템을 사용하고 있을 때 주로 발생하는 문제입니다.

### 원인과 해결 방법

이러한 문제의 주된 원인은 Webpack 설정과 ES5 라이브러리 간의 호환성입니다. Webpack은 기본적으로 ES6+ 모듈 시스템을 사용하기 때문에, ES5 라이브러리와 충돌이 일어날 수 있습니다. 

1. **Webpack 설정 수정**: `webpack.config.js` 파일에서 `output` 섹션에 `libraryTarget: 'var'`를 추가하면 문제를 해결할 수 있습니다. 이렇게 하면 Webpack이 라이브러리를 전역 변수로 출력합니다.

    ```javascript
    output: {
        libraryTarget: 'var'
    }
    ```

2. **Externals 설정**: Webpack 설정에서 `externals` 옵션을 사용하여 ES5 라이브러리를 외부 의존성으로 표시할 수 있습니다.

    ```javascript
    externals: {
      'your-library-name': 'YourLibraryGlobalVariable'
    }
    ```

3. **TypeScript 설정 수정**: `tsconfig.json`에서 `"esModuleInterop": true`를 설정합니다. 이는 CommonJS와 ES 모듈 간의 호환성을 향상시킵니다.

    ```json
    {
      "compilerOptions": {
        "esModuleInterop": true
      }
    }
    ```

## 결론

TypeScript와 Webpack을 사용하는 프로젝트에서 ES5 라이브러리를 효과적으로 사용하기 위해서는 설정 파일을 적절하게 수정해야 합니다. 위에서 설명한 방법들은 이 문제를 해결하는 데 있어서 가장 효과적인 접근법입니다. 이를 통해 "ReferenceError: exports is not defined" 오류를 해결하고, 프로젝트의 다양한 라이브러리와의 호환성을 높일 수 있습니다.