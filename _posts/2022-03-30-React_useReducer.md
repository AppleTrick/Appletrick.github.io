---
title: useReducer란? 
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-03-30 00:00:00 +0900
categories: [React]
description: 블로그 포스팅 방법 분석
tags: [React, useReducer]
---

# state와 useReducer의 차이

state의 경우

```jsx
const [state , setState] = useState(0);
setState(state + 1)
```

useReducer의 경우

```jsx
function reducer (oldState, action){
	if(action == 'up'){
		return oldState + 1;
	}
}

[state , dispatch] = useReducer(reducer, 0);
dispatch('up')

```

# State의 코드

```jsx
import React , {useState} from 'react';

const App = () => {
    const [count, setCount] = useState(0);

    const down = () => {
        setCount(count - 1);
    }
    const reset = () => {
        setCount(0);
    }
    const up = () => {
        setCount(count + 1);
    }

    return(
        <>
            <input type="button" value="-" onClick={down} />
            <input type="button" value="0" onClick={reset}/>
            <input type="button" value="+" onClick={up}/>
            <span>{count}</span>
        </>
    )
}

export default App;
```

state의 값을 직접적으로 변경할 수 있다. 대부분은 state를 통해 값에대해 직접적으로 접근할 수 있다.

# 어디에서 문제인가?

만약에 count와 같은 변경되는 값이 한개가 아니라 여러개이면? 각각의 state의 값을 변경하게 할 것 인가?

# reducer

```jsx
count [값 , 처리하는 방식을 정해주는 함수명] = useReducer(처리 방법이 정해진 함수 , 초기값)
```

state와 reducer의 차이는 useReducer를 사용한다.

state를 직접 사용자가 변견하는것이 아니라 reducer가 직접적으로 해준다.

```jsx
import React , {useReducer} from 'react';

const App = () => {

    function countReducer (oldCount, action){
        if(action == 'UP'){
            return oldCount + 1
        }else if(action == 'RESET'){
            return 0
        }else if(action == 'DOWN'){
            return oldCount - 1;
        }
    }

    const [count, countDispatch] = useReducer( countReducer , 0);

    const down = () => {
        countDispatch('DOWN');
    }
    const reset = () => {
        countDispatch('RESEt');
    }
    const up = () => {
        countDispatch('UP');
    }

    return(
        <>
            <input type="button" value="-" onClick={down} />
            <input type="button" value="0" onClick={reset}/>
            <input type="button" value="+" onClick={up}/>
            <span>{count}</span>
        </>
    )
}

export default App;
```

만약 값을 직접적으로 설정하고 싶다면?

```jsx
import React , {useReducer, useState} from 'react';

const App = () => {

    const [number, setNumber] = useState(1);

    function countReducer (oldCount, action){
        if(action.type == 'UP'){
            return oldCount + action.number
        }else if(action.type == 'RESET'){
            return 0
        }else if(action.type == 'DOWN'){
            return oldCount + action.number;
        }
    }

    const [count, countDispatch] = useReducer( countReducer , 0);

    const down = () => {
        countDispatch({type : 'DOWN' , number : number});
    }
    const reset = () => {
        countDispatch({type : 'RESET', number : number});
    }
    const up = () => {
        countDispatch({type : 'UP', number : number});
    }
    const changeNumber = (event) => {
        setNumber(Number(event.target.value));
    }

    return(
        <>
            <input type="button" value="-" onClick={down} />
            <input type="button" value="0" onClick={reset}/>
            <input type="button" value="+" onClick={up}/>
            <br/>
            <input type="text" value={number} onChange={changeNumber}/>
            <span>{count}</span>
        </>
    )
}

export default App;
```

dispatch 쪽에 값을 객체 단위로 전달하여 함수에 직접적으로 값을 은닉하여 전달할 수 있다.