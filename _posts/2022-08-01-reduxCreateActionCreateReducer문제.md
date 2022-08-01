---
title: redux immutable 문제 해결하기 (createAction, createReducer)
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-08-01 00:00:00 +0900
categories: [TS, React, Redux]
description: 설명
tags: [개념, Redux, TypeScript, React]
---

# redux immutable 문제 해결하기

redux 사용하다 보니 문제가 생겼다.

```tsx
const initialState: ScheduleData = {
  Expedition: {
    Weekly: {
      ChallengeAbyss: {
        IsDone: false,
        Visible: true,
      },
      EffonaReward: {
        IsDone: false,
        Visible: true,
      },
      CrackPieceReward: {
        IsDone: false,
        Visible: true,
      },
      ChallengeGuardian: {
        IsDone: false,
        Visible: true,
      },
    },
  },
  Characters: [
    {
      CharacterInform: {
        CharacterName: "하얀눈송이아래",
        Job: "건슬링어",
        Level: 1591,
      },
      Daily: {
        ChaosDungeon: {
          isDone: false,
          RestGage: 0,
          Visible: true,
        },
        Gaurdian: {
          isDone: false,
          RestGage: 0,
          Visible: true,
        },
        DailyEffona: {
          isDone: false,
          Visible: true,
        },
        GuildCheck: {
          isDone: false,
          Visible: true,
        },
      },
      Weekly: {
        Argos: {
          isDone: false,
          Visible: true,
        },
        Valtan: {
          IsDone: false,
          GateNumber: 0,
          Visible: true,
        },
        Viakiss: {
          IsDone: false,
          GateNumber: 0,
          Visible: true,
        },
        Kukusaiton: {
          IsDone: false,
          GateNumber: 0,
          Visible: true,
        },
        Abrelshood: {
          IsDone: false,
          GateNumber: 0,
          Visible: true,
        },
        Kayangal: {
          IsDone: false,
          GateNumber: 0,
          Visible: true,
        },
      },
    },
  ],
};
```

이렇게 큰값의 데이터를 어떻게 변화 시킬것인가에 대해 문제가 생겼다.

react에서 redux를 사용할 때 상태는 불변성을 유지시켜줘야된다.

즉 값을 유지 시켜줘야되는데 문제는 이렇게 큰 값의 경우 코드의 양이 많아지고 데이터를 변경하기 까다로워져 버린다.

# 문제 해결의 방안

- immer.js
- ReduxToolkit 사용 (createAction, createReducer )

처음 해결방안으로는 immer을 이용하여서 문제를 해결하려고 했으나 Redux Toolkit을 통해 immer와 같은 불변성 문제를 해결방법이 있는걸 보고 ReduxToolkit을 이용하여 문제 방안 해결

# 새로운 문제 : createAction과 createReducer는 TypeScript에서 어떻게 사용하나?

핵심은 createReducer 이지만 action을 좀 더 편하게 사용하기 위해 createAction 사용하는법

## createAction 사용하기

**구 액션정의**

```tsx
// 액션 이름을 타입화
const actionNameType = "actionName" as const;

// 액션 생성
const action = (value) => ({
  type: actionNameType,
  payload: { value },
});
```

액션을 정의를 이렇게 했다면

**createAction으로 actiont 생성**

```tsx
// 액션 이름을 타입화
const actionNameType = "actionName" as const

// 1 - 1 전달 값이 없을 경우 액션 생성
const action = createAction(actionNameType);
---------------------------------------------------------------------
// 1 - 2 payload와 같이 전달할 값이 있을 경우

// payload의 타입 정의
type Profile = {
	name : string
	adress : string
}
// Generic을 이용하여 타입 전달
const action = createAction<Profile, typeof actionNameType>(actionNameType);
```

핵심은 payload 타입 정의하고 Generic 에 넣어주는것

## createReducer

```tsx
const createReducerName = createReducer(initialState, {
  actionName: (state, action) => state + action.payload,
});
```

reducer를 만들때와 큰 차이는 없다. initialState에는 생성값이 되고 이후의 Map(K,V)의 Key값에 createAction에 정의했던 actionName을 쓰고 Value 값에는 함수로 (state , action) ⇒ 형태로 state 값에는 initialState 가 들어가고 action에는 정의한 action이 들어와 action.payload를 사용하면 인자로 받아온 값을 사용 가능하다.

# 후기

사실 정확한 해결책인지는 모르겠지만, 일단 기록하고 보자..
