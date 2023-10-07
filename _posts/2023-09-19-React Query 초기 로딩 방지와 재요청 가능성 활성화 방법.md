---
title: React Query 초기 로딩 방지와 재요청 가능성 활성화 방법
date: 2023-09-19 20:00:00 +0900
categories:
  - JavaScript
tags:
  - React
  - Query
---

## 개요

React Query는 클라이언트 상태 관리 라이브러리입니다. 주로 API와 같은 비동기 작업을 처리하는 데 사용되며, 초기 로딩을 어떻게 방지하고, 나중에 필요할 때 데이터를 재요청하는 것이 가능한지에 대한 문제가 있습니다.

## 초기 로딩 방지

React Query의 `useQuery`나 `useMutation` 훅은 초기 로딩을 자동으로 실행합니다. 하지만 이를 방지하려면 `enabled` 옵션을 `false`로 설정할 수 있습니다. 이렇게 하면 초기에 데이터를 불러오지 않고, 필요할 때만 데이터를 로딩합니다.

```javascript
useQuery('todos', fetchTodos, {
  enabled: false
});
```

## 재요청 활성화

`enabled: false`로 설정한 후에, 특정 조건이나 버튼 클릭 등에 따라 데이터를 재요청하고 싶다면, `refetch` 함수를 사용합니다. `useQuery` 훅에서 반환되는 `refetch` 함수를 호출하면 됩니다.

```javascript
const { refetch } = useQuery('todos', fetchTodos, {
  enabled: false
});

// 나중에 재요청하기
refetch();
```

## 주의사항

`enabled: false`로 설정하면 초기 로딩이 비활성화되므로, 수동으로 데이터를 불러와야 합니다. 그리고 `refetch` 함수를 사용하여 데이터를 갱신하면, 그 시점에서 새로운 데이터로 업데이트됩니다.

## 요약

React Query에서 초기 로딩을 방지하고 나중에 재요청을 가능하게 하려면 `enabled: false` 옵션을 사용해 초기 로딩을 비활성화하고, `refetch` 함수를 이용해 수동으로 데이터를 로딩하면 됩니다. 이렇게 하면 특정 조건에 따라 데이터를 불러올 수 있습니다.