---
title: 타입스크립트에서의 overloading
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-05-30 00:00:00 +0900
categories: [TS]
description: 설명
tags: [TS, TypeScript, 개념]
---

# parameter 개수가 같고 타입이 다를경우

```tsx
// parameter 개수가 같고 타입이 다를 경우
type Config = {
  path: string;
  state: object;
};

type Push = {
  (path: string): void;
  (config: Config): void;
};

const push: Push = (config) => {
  // 조건이 다를 경우를 처리해줘야됨
  if (typeof config === "string") {
    console.log(config);
  } else {
    console.log(config.path);
  }
};
```

처리 부분에서 if ~ else 문을 통해 해당 타입이 어떤 형태별로 분류된 함수를 실행 시켜준다.

# parameter 개수가 다를 경우

```tsx
// parameter 개수가 다를 경우
type Add = {
  (a: number, b: number): number;
  (a: number, b: number, c: number): number;
};

const add: Add = (a, b, c?: number) => {
  // ?: 옵셔널을 통해 c가 있을 경우만 처리
  if (c) {
    return a + b + c;
  }
  return a + b;
};
```

파라미터가 여러개일 경우 ?: 를 통해 해당 파라미터의 존재여부를 없거나 존재하거나로 구분하여 함수를 실행 시켜준다.
