---
title: 데이터 정보를 저장하는 LocalStorage
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-04-06 00:00:00 +0900
categories: [JS]
description: 데이터 정보를 저장하는 LocalStorage
tags: [JS]
---

LocalStorage는 웹에서 파일을 저장할 수 있는 기능, 작은 DB라고 생각하면 된다.

## localStorage.setItem()

setItem의 경우 Key , Value 형식으로 값을 저장할 수 있다.

```jsx
localStorage.setItem("username" , "park");
```

## localStorage.getItem()

getItem은 localStorage에 저장된 값을 불러 온다.

```jsx
const name = localStorage.getItem("username");
```

## localStorage.removeItem()

removeItem은 localstorage 의 값을 삭제한다.

```jsx
localStorage.removeItem("username");
```