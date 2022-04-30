---
title: JS로 새로고침 막기
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-04-05 00:00:00 +0900
categories: [JS]
description: JS로 새로고침 막기
tags: [javascript]
---

# 새로고침을 막는 preventDefault

**HTML**

```jsx
<form id="login-form">
  <input
    required
    maxlength="15"
    type="text"
    placeholder="what is your name? "
  />
  <input type="submit" value="log in" />
</form>
```

**Javascript**

```jsx
const loginForm = document.querySelector("#login-form");
const loginInput = document.querySelector("#login-form input");

const onLoginSubmit = (event) => {
  event.preventDefault();
  console.log(event);
};

loginForm.addEventListener("submit", onLoginSubmit);
```

form 을 통해서 값을 전달 할 때 submit 이벤트가 실행되면 onLoginSubmit 함수가 실행된다.

실행된 함수의 매개변수의 값은 기본적으로 방금 실행된 이벤트에 대한 정보를 담고 있다.

그 중 preventDefault는 페이지의 새로고침을 막는다.
