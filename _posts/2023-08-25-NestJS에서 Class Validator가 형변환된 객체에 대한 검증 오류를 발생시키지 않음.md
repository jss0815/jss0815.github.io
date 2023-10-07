---
title: NestJS에서 Class Validator가 형변환된 객체에 대한 검증 오류를 발생시키지 않음
date: 2023-08-25 20:00:00 +0900
categories:
  - JavaScript
tags:
  - NestJS
---

## 문제 개요

NestJS에서는 Class Validator를 이용해 객체의 유효성을 검사할 수 있습니다. 그러나, 때로는 형변환된 객체에 대한 검증 오류가 발생하지 않는 경우가 있습니다. 본 글에서는 이러한 문제점을 자세히 살펴보고 해결 방안을 제시하겠습니다.

## Class Validator란?

Class Validator는 TypeScript와 JavaScript에서 클래스 기반으로 객체를 검증하기 위한 라이브러리입니다. 이 라이브러리를 사용하면 객체의 필드나 속성에 다양한 검증 조건을 적용할 수 있습니다. 예를 들어, 이메일 형식이 올바른지, 문자열의 길이가 특정 범위 내에 있는지 등을 검증할 수 있습니다.

## 형변환과 검증 오류

문제는 자동 형변환(캐스팅)된 객체에서 발생합니다. Class Validator는 원래의 객체 유형을 기반으로 검증을 수행하기 때문에, 형변환이 이루어진 객체에 대한 검증이 제대로 이루어지지 않을 수 있습니다.

### 예시: `ValidationError`

아래와 같이 `string`으로 형변환된 객체를 검증할 때 `ValidationError`가 발생하지 않는 경우를 살펴보겠습니다.

```typescript
class CreateUserDto {
  @IsString()
  name: string;
}

const user = {
  name: 1234,
};

validateOrReject(user as CreateUserDto).catch(errors => {
  // ValidationError가 발생하지 않음
});
```

## 해결 방안

1. **형변환 전에 검증**: 객체를 형변환하기 전에 먼저 검증을 수행합니다.
2. **Whitelist 사용**: Class Validator에서 제공하는 `whitelist` 옵션을 활용해, 허용된 필드만을 검증합니다.

```typescript
const options = { whitelist: true, forbidNonWhitelisted: true };
validateOrReject(user as CreateUserDto, options).catch(errors => {
  // 이제 ValidationError가 발생
});
```

3. **트랜스포머 사용**: `class-transformer` 라이브러리를 이용해 객체를 올바른 형태로 변환한 후 검증을 수행합니다.

## 결론

NestJS의 Class Validator는 매우 유용하지만, 형변환된 객체에 대한 검증에서는 주의가 필요합니다. 이를 해결하기 위해 몇 가지 방법이 있으며, 이 중에서 가장 적합한 방법을 선택하여 사용하면 됩니다.