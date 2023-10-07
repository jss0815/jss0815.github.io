---
title: React에서 querySelector가 첫 호출에서 null을 반환하는 문제 해결하기
date: 2023-08-22 20:00:00 +0900
categories:
  - JavaScript
tags:
  - React
  - querySelector
---

## 문제 상황 요약

React에서 자바스크립트의 `querySelector` 메서드를 사용할 때, 처음 호출하는 경우 `null`을 반환한다는 문제가 있습니다. 이후에는 정상적으로 작동한다는 것이 특이한 점입니다.

## 원인 분석

### DOM 렌더링 타이밍 이해하기

React에서 `querySelector` 메서드를 호출하는 시점이 중요합니다. React 컴포넌트의 라이프 사이클에서, 처음 렌더링이 이루어진 후에 DOM 요소가 실제로 존재합니다. 그 이전에 `querySelector`를 호출하면, 찾고자 하는 요소가 아직 DOM에 존재하지 않기 때문에 `null`을 반환합니다.

### useEffect를 활용하기

이 문제를 해결하기 위해서는 `useEffect` 훅을 사용해야 합니다. `useEffect`는 컴포넌트가 렌더링된 후에 실행되는 코드를 작성할 수 있게 해줍니다. 따라서 `useEffect` 안에서 `querySelector`를 호출하면, 첫 호출에서도 원하는 요소를 정확히 선택할 수 있습니다.

## 해결 방안

React에서 이 문제를 해결하는 가장 적절한 방법은 `useEffect` 훅을 사용하는 것입니다. 다음은 예시 코드입니다.

```javascript
import React, { useEffect } from 'react';

function MyComponent() {
  useEffect(() => {
    const element = document.querySelector('#my-element');
    if (element) {
      // 원하는 작업 수행
    }
  }, []);

  return (
    <div id="my-element">
      Hello, World!
    </div>
  );
}
```

위의 코드에서 `useEffect`는 컴포넌트가 렌더링된 이후에 실행되므로, `querySelector`로 `#my-element`를 찾을 수 있습니다.

## 정리

React에서 `querySelector`를 사용할 때에는 컴포넌트의 라이프 사이클과 DOM 렌더링 타이밍을 잘 이해해야 합니다. `useEffect` 훅을 적절히 활용하면, 이러한 문제를 쉽게 해결할 수 있습니다. 이를 통해 더욱 견고한 웹 애플리케이션을 구축할 수 있습니다.