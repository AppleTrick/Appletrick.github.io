---
title: interface에관하여
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-06-03 00:00:00 +0900
categories: [TS]
description: 설명
tags: [TS, TypeScript, 타입스크립트, interface, 개념]
---

interface는 type과 유사하다. 똑같이 해당 구조를 사전에 설정해 주는 역할을 한다.

# interface와 type

## type에서의 코드

```tsx
type NickName1 = string;
type HealthBar1 = number;
type Hamberg = Array<string>;
type Team = "red" | "blue" | "yellow"; // 1️⃣ 타입에서 특정 값만을 가지게 할 수 있음

type Player3 = {
  nickname: NickName1;
  healthBar: HealthBar1;
  team: Team;
};

const LeeP: Player3 = {
  nickname: "LeeP",
  healthBar: 12,
  team: "red", // 1️⃣ red , blue, yellow 3가지중 하나만 가능
};

type Coffee = string;

const ediya: Coffee = "이디야";
```

타입으로 값을 제한 할 수 있다. 위의 코드에서는 type에서 Team 은 red, blue, yellow 중 하나만 가능하다.

이처럼 타입은 코드에서 type은 다재다능한 키워드이다.object를 정의 할 수 있고 특정 타입을 제한 할 수 있다.

또한 alias 기능을 사용하여 디테일하게 사용이 가능하다. 타입은 모든 것이 될 수 있다!

## interface는 ?

interface는 type과는 다르게 object 모양을 알려주는데만 사용한다. 코드를 보면 다음과 같다.

```tsx
type NickName1 = string;
type HealthBar1 = number;
type Hamberg = Array<string>;
type Team = "red" | "blue" | "yellow"; // 타입에서 특정 값만을 가지게 할 수 있음

interface Player3 {
  nickname: NickName1;
  healthBar: HealthBar1;
  team: Team;
}
```

interface는 object를 정의하는 이유 하나로 사용한다.

# type 과 interface에서 다른점들

type과 interface에서는 다른점들이 여러가지가 있다.

## 상속

type과 interface에서는 상속에서 차이가 난다.

### interface에서의 상속 코드

```tsx
interface User {
  name: string;
}

interface Player extends User {}

const park: Player = {
  name: "park;",
};
```

인터페이스의 경우 상속은 extends 키워드를 통해 하는 반면

### type에서의 상속 코드

```tsx
type User = {
  name: string;
};

type Player = User & {};

const park: Player = {
  name: "park;",
};
```

type 에서는 쿠체적인 적용 없이 & 연산자를 통해 상속해준다.

# interface는 property의 축적이 가능하다.

property의 축적이 가능하다는 말은 코드를 보면 이해하기 쉽다.

```tsx
interface User {
  name: string;
}

interface User {
  address: string;
}

interface User {
  addressNum: number;
}

const park: User = {
  name: "park",
  address: "seoul",
  addressNum: 125,
};
```

User interface를 만들고 여러개를 중첩해서 만들어도 typescript에서 하나로 합쳐준다.
