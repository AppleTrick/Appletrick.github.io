---
title: npm? npx? yarn? 에 대한 내용
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-05-03 00:00:00 +0900
categories: [개념]
description: 설명
tags: [node, npm, npx, yarn]
---

# 😃 동기

node 를 사용할때마다 라이브러리를 불러와서 사용하는데, 가끔 상황에 따라 npm, npx, yarn 등으로 각각 실행 과 설치가 다를때 있다. 해당 이유가 궁금하기도 하고 알아보면 좋을거 같아 작성해본다.

# NPM?

npm 이란 Node Package Manager 의 약자로 node.js 의 패키지를 관리해주는 패키지 툴이다.

많은 개발자들이 npm 사이트에 많은 모듈들을 올려놓아 다운 하여 편한게 사용할 수 있다.

# yarn?

그럼 yarn은 어떤 존재일까? yarn 은 페이스북에서 만든 자바스크립트 패키지 매니저이다. npm과 같은 역할을 해준다. 같은 역할을 하지만 yarn 은 npm의 단점을 보완해서 나온 패키지 매니저이다.

## yarn이 npm보다 나은점

- 속도 : 흔히 패키지를 설치할때 yarn 은 병렬로 처리 npm 은 순차적를 하면서 설치할때 속도적 차이가 생긴다.
- 보안 : npm은 패키지들을 설치할때 자동으로 코드가 의존적으로 처리되게 만들었는데, 이 때문에 안전이 보장되지 않은 패키지가 설치될 경우 문제가 발생이 생길 수 있다.
- 안정성 : yarn은 yarn.lock 파일을 통해 버전 차이를 극복시켜준다. 물론 npm도 할수있지만, yarn은 기본세팅이기 때문

# yarn 이 그럼 무조건 npm 보다 좋은거 아닌가?

“❌”

yarn도 단점이 있다. yarn은 npm 보다 디스크 메모리를 더 잡아먹는것도 있을수도 있고, yarn.lock때문에 만약 기존 모듈이 최신으로 업데이트할 경우 하위호환을 지원 못할수도있다. 하지만 무엇보다 npm 이 yarn 보다 좋은점은 npm을 사용하고 있는 사람들과 현재까지 npm에 저장되어있는 다양한 package 들이다.

때문에 yarn이 npm보다 무조건 좋다고는 말은 못한다. 결국 취향차이와 자기의 상황에 맞게 쓰면 될거 같다.

# NPX?

위에 두개는 알겠다.npm, yarn은 는 자바스크립트 패키지 매니져이고 외부에서 패키지를 가지고 올 때 사용하는것인데 npx는 뭘까

npx는 Node Package eXecute 노드 패키지의 실행을 도구이다. npm 5.2.0 버젼에서 추가되었다.

```jsx
npm run my-package
npx my-package
```

보다 간단하게 프로젝트 실행가능, 또한 npx 로는 설치를 안하고 실행도 가능하다.
