---
title: React-Router 사용하고 활용하기 
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-03-16 00:00:00 +0900
categories: [Blogging]
description: 블로그 포스팅 방법 분석
tags: [블로그, 글쓰기]
---

# 라우팅이란?

라우팅이란 유저가 요청한 URL 에 따라 원하는 페이지를 보여주는것을 의미한다.

리액트에서 라우팅은 페이지별로 나눠져 있는 컴포넌트를 관리하기 위한 시스템이다.

리액트에서 라우팅시스템을 구현하는 방법은 두가지가 있는데 

1. **리액트 라우터(React Router) :** 리액트 라우터는 기존의 시스템에서 가장 많이 사용되는 시스템이다.
2. **Next.js :** 리액트 프로젝트의 프레임워크로 다양한 기능을 제공하는데 그중 하나가 리액트 라우팅 시스템이다.

# React-Router 사용하기

현재 이글에서는 기초적인 리액트 라우터만 써보기로 하자

## React-Router 설치

```bash
npm i react-router-dom
```

## index.js 에서 라우팅 시스템을 적용

프로젝트 전체에 리액트 라우터를 적용하기 위해서는 메인 루트가 되는 index.js에 react-router를 적용시켜준다.

```jsx
import React from 'react';
import ReactDom from 'react-dom';
import App from './src/App';
import {BrowserRouter} from 'react-router-dom';

ReactDom.render(
    <BrowserRouter>
        <App />
    </BrowserRouter>, 
    document.getElementById('root')
);
```

## 라우팅시킬 페이지 생성

**`Home.jsx`**

```jsx
import React from 'react';

const Home = () => {
    return(
        <div>
            <h1>홈</h1>
            <p>가장 먼저 보여지는 홈 페이지 입니다.</p>
        </div>
    )
}

export default Home;
```

**`About.jsx`**

```jsx
import React from 'react';

const About = () => {
    return(
        <>
            <h1>about</h1>
            <p>about 페이지 입니다.</p>
        </>
    )
}

export default About;
```

## 메인 실행 페이지

**`App.jsx`**

```jsx
import React from 'react';

import { Route, Routes } from "react-router-dom";
import Home from "./skillFolder/Routing/pages/home"
import About from "./skillFolder/Routing/pages/about"

const App = () => {
  return(
      <>
        <Routes>
            <Route path="/" element={<Home/>}/>
            <Route path="/about" element={<About/>}/>
        </Routes>
      </>
  );
};

export default App;
```

---

### <Route> 의 규칙

```jsx
<Route path="주소규칙" element={보여 줄 컴포넌트 JSX} />
```

위 의 규칙은 꼭 지켜주자

---

### 결과페이지

정상적으로 햇을 경우 아래와 같은 이미지의 결과 페이지가 나오게 된다.

![1](https://user-images.githubusercontent.com/31761527/158533496-48867538-0eba-40fc-8186-bda642b70003.png)

---

## <Link> 를 이용하여 다른 컴포넌트로 가는법

Link를 이용하면 다른 컴포넌트로 이동할 수 있는 수단이 생긴다. 

- <a> 태그는 브라우저의 새로운 페이지를 불러오기 때문에 리액트에서는 사용 하면안된다.
- <Link> 태그는 역할을 같지만 브라우저의 새로운 페이지는 부르지 않고 History API 에 브라우저 경로 변경만 해준다.

```jsx
<Link to="경로">링크 이름</Link>
```

`home.jsx`

```jsx
import React from 'react';
import {Link} from 'react-router-dom';

const Home = () => {
    return(
        <div>
            <h1>홈</h1>
            <p>가장 먼저 보여지는 홈 페이지 입니다.</p>
            <Link to="./about">소개</Link>
        </div>
    )
}

export default Home;
```

# URL 파라미터와 URL 쿼리스트링을 이용한 페이지 정보

URL 파라미터 : 주소의 경로에 유동적인 값을 넣는 형태, 주로 **특정 데이터**를 조회할 때 사용

쿼리 스트링은 주소의 뒷부분에 ? 문자열 이후에 key=value 로 값을 정의하며 & 로 구분을 하는 형태 주로 **정렬 방식의 데이터 조회에 필요한 옵션을 전달** 할때 사용

- ***URL파라미터*** : /profile/Appletrick
- ***URL쿼리스트링 :*** /main?**page=1&keyword=name

## URL 파라미터 이용해보기

`App.jsx`

```jsx
const App = () => {
  return(
      <>
        <Routes>
            <Route path="/" element={<Home/>}/>
            <Route path="/about" element={<About/>}/>
            <Route path='/profile/:username' element={<Profile/>}/>
        </Routes>
      </>
  );
};
```

라우팅을 해줄때 profile로 가면 :username을 매개변수로 파라미터로 받아준다.

`Home.jsx`

```jsx
const Home = () => {
    return(
        <div>
            <h1>홈</h1>
            <p>가장 먼저 보여지는 홈 페이지 입니다.</p>
            <ul>
                <li>
                    <Link to="/about">소개</Link>
                </li>
                <li>
                    <Link to="/profile/appletrick">Appletrick</Link>
                </li>
                <li>
                    <Link to="/profile/steve">스티브잡스</Link>
                </li>
                <li>
                    <Link to="/profile/who">누구?</Link>
                </li>
            </ul>
        </div>
    )
}
```

profile에서 매개변수로 appletrick, steve, who 3개로 나뉘게 된다.

`**profile.jsx**` 를 만들어주자

```jsx
import React from 'react'
import { useParams } from 'react-router-dom'

const data = {
    appletrick : {
        name : 'Appletrick',
        about : '멋진 개발자',
    },
    steve : {
        name : '스티브잡스',
        about : '애플의 창시자',
    }
}

const Profile = () => {

    const params = useParams();
    const profile = data[params.username];

    return(
        <>
            <h1>사용자 프로필</h1>
            {profile ? (
                <div>
                    <h2>{profile.name}</h2>
                    <h3>{profile.about}</h3>
                </div>
            ) : (
                <p>존재하지 않는 사람 입니다.</p> 
            )}
        </>
    )
}

export default Profile
```

- 임시적인 data 오브젝트를 생성해준다.
- useParams()를 통해 URL 파라미터값을 가지고온다.
- profile 변수에 data 파라미터 값과 일치한 내용을 가지고와서 화면에 띄어준다.

<aside>
☝🏻 URL 파라미터는 `/profiles/:usernam`과 같이 경로에 `:`를 사용하여 설정
만약 URL 파라미터가 여러개인 경우엔 `/profiles/:username/:field`와 같은 형태로 설정

</aside>

## 쿼리 스트링 사용해보기

쿼리스트링을 `**about.jsx**` 에서 띄어보기

useLocation을 통해 쿼리스트링의 경로를 나타내준다.

```jsx
import React from 'react';
import { useLocation } from 'react-router-dom';

const About = () => {

    const location = useLocation();
    console.log(location);

    return(
        <>
            <h1>about</h1>
            <p>리액트 라우터사용하는 페이지</p>
            <p>현재의 쿼리 스트링 {location.search}</p>
        </>
    )
}

export default About;
```

주소값을 http://localhost:3000/about?detail=true&mode=1 해줄경우

화면에 useLocation() 훅을 이용하여 쿼리스트링을 화면에 띄울수 있다.

**location 객체 안의 값**

![2](https://user-images.githubusercontent.com/31761527/158533495-8c09671b-787b-4117-83e2-3314a41136fd.png)

- **pathname** : 현재주소
- **hash :** 주소의 # 문자열 뒤의 값
- **state**: 페이지로 이동할때 임의로 넣을 수 있는 상태 값
- **key**: location 객체의 고유 값, 초기에는 default 이며 페이지가 변경될때마다 고유의 값이 생성됨
- **search**: 맨 앞의 ? 문자 포함한 쿼리스트링 값

현재의 쿼리 스트링은 ?detail=true&mode=1 값인데 이 값을 key 와 value로 분류하는 작업은 npm에 `qs` 또는 `querystring`을 통해 가능하다.

(원래는 npm의 qs, querystring을 통해 해야 했지만 v6버전 부터 리액트로 할것)

리액트 라우터에서는 v6 버젼부터 useSearchParam을 통해 쉽게 쿼리스트링을 다룰 수 있다.

```jsx
import React from 'react';
import { useSearchParams } from 'react-router-dom';

const About = () => {

    const [searchParams, setSearchParams] = useSearchParams();
    const detail = searchParams.get('detail');
    const mode = searchParams.get('mode');

    console.log(typeof(mode), typeof(detail));

    const onToggleDetail = () => {
        setSearchParams({mode, detail : detail === true ? false : true });
    }

    const onIncreaseMode = () => {
        const nextMode = mode == 'null' ?  1 : parseInt(mode) + 1;
        setSearchParams({mode : nextMode , detail});
    }

    return(
        <div>
            <h1>소개</h1>
            <p>리액트 라우터를 사용해 보는 프로젝트입니다.</p>
            <p>detail: {detail}</p>
            <p>mode: {mode}</p>
            <button onClick={onToggleDetail}>Toggle detail</button>
            <button onClick={onIncreaseMode}>mode + 1</button>
        </div>
    )
}

export default About;
```

### 핵심

- useSearchParams() 는 배열값으로 값을 반환한다.
    - 첫번째 값은 쿼리파라미터의 값을 조회하는것 (searchParams이부분 )
    - 두번째 값은 쿼리파라미터의 값을 수정하거나 업데이트 (setSearchParams 부분) 을가지고 온다..

조회하여 값을 가지고 올때는 모두 string 문자열 값을 취하기 때문에 값을 더 하거나 뺄때는 parseInt() 를 통해 값을 조정한다.

# 중첩된 라우팅

중첩된 라우팅을 사용하는 방법

`article.jsx`

```jsx
import React from 'react';
import { Link, Outlet } from 'react-router-dom';

const Article = () => {
    return(
        <>
            <Outlet/>
            <ul>
                <li>
                    <Link to="/articles/1">게시글 1</Link>
                </li>
                <li>
                    <Link to="/articles/2">게시글 2</Link>
                </li>
                <li>
                    <Link to="/articles/3">게시글 3</Link>
                </li>
            </ul>
        
        </>

    )
}

export default Article
```

`article.jsx`

```jsx
import React from 'react';
import { useParams } from 'react-router-dom';

const Article = () => {
    const { id } = useParams();
    return(
        <>
            <h2>게시글 {id}</h2>
        </>
    )

}

export default Article
```

`home.jsx`

```jsx
<li>
	<Link to="/articles">게시글 목록</Link>
</li>

```

`app.jsx`

```jsx
<>
        <Routes>
            <Route path="/" element={<Home/>}/>
            <Route path="/about" element={<About/>}/>
            <Route path='/profile/:username' element={<Profile/>}/>
            <Route path='/articles' element={<Articles/>}>
              <Route path=':id' element={<Article/>}/>  
            </Route>
        </Routes>
</>
```

<OutLet/> 컴포넌트를 사용할것

![3](https://user-images.githubusercontent.com/31761527/158533493-0ba27915-4f3b-4244-921f-a3d4de7709d9.png)

![4](https://user-images.githubusercontent.com/31761527/158533490-a449f9fd-f07a-4912-9155-41679ad35573.png)

<OutLet/> 컴포넌트는 Route에서 자식요소로 들어가는 부분을 보여줄수 있다

## 좀더 나은 중첩방식 Outlet

OutLet 은 공통적인 부분을 보여줄때 효율적으로 사용할수 있다.

기존에 Header는 헤더부분을 따로 만들고 컴포넌트화 시키고 따로 페이지를 보여주는 방법도 있지만 Outlet은 조금더 효율적으로 화면을 보여줄 수 있다.

`Layout.jsx`

```jsx
import React from "react";
import { Outlet , useNavigate} from "react-router-dom";

const Layout = () => {

    const navigate = useNavigate();

    const goBack = () => {
        navigate(-1);
    }

    const goArticle = () => {
        navigate('/articles' , {replace : true});
    }/

    const goAbout = () => {
        navigate('/about');
    }

    return(
        <>
            <header style={ {background : "royalblue" , padding : 16 , fontSize : 24}}>
                <button onClick={goBack}>뒤로가기</button>
                <button onClick={goArticle}>게시글목록</button>
                <button onClick={goAbout}>소개로</button>
            </header>
            <main>
                <Outlet/>
            </main>
        </>
    )
}

export default Layout;
```

- useNavigate 는 Link component를 사용하지 않고 페이지를 이동시키는 훅이다.

`App.jsx`

```jsx
import { Route, Routes } from 'react-router-dom';
import Layout from './Layout';
import About from './pages/About';
import Article from './pages/Article';
import Articles from './pages/Articles';
import Home from './pages/Home';
import Profile from './pages/Profile';

const App = () => {
  return (
    <Routes>
      <Route path="/" element={<Layout />}>
        <Route index element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/profiles/:username" element={<Profile />} />
      </Route>
      <Route path="/articles" element={<Articles />}>
        <Route path=":id" element={<Article />} />
      </Route>
    </Routes>
  );
};

export default App;
```

layout을 기본 페이지로 하여 하위 요소를 Outlet을 통해 나타낼수 있다.

![5](https://user-images.githubusercontent.com/31761527/158533479-3c8143ef-ba9c-45a7-98b8-00c9643f5bb3.png)

Layout의Route의 path는 “/” 루트로 된고 Home component의 index props 는 `path = “/”` 와 같은 의미 이다.

```jsx
const navigate = useNavigate();

navigate()
```

- navigate (?)
    
    파라미터 값이 숫자면 해당 숫자만큼 앞으로 가거나 뒤로감, 주소를 입력할경우 해당 주소로 가게됨,
    
    replace라는 옵션은 해당 페이지 기록을 남기않게됨
    

## NavLink를 사용해보자

현재 라우트의 경로와 일치하는 경우 특정 스타일 또는 CSS 클래스를 적용하는 컴포넌트

`artcles.jsx`

```jsx
import React from 'react';
import { NavLink, Outlet } from 'react-router-dom';

const Article = () => {
    const activeStyle = {
        color : 'green',
        fontsize : 21,
    }

    return(
        <>
            <Outlet/>
            <ul>
                <li>
                    <NavLink to="/articles/1" style={({isActive}) => (isActive ? activeStyle : undefined)} >게시글 1</NavLink>
                </li>
                <li>
                    <NavLink to="/articles/2" style={({isActive}) => (isActive ? activeStyle : undefined)}>게시글 2</NavLink>
                </li>
                <li>
                    <NavLink to="/articles/3" style={({isActive}) => (isActive ? activeStyle : undefined)}>게시글 3</NavLink>
                </li> 
            </ul>
        
        </>

    )
}

export default Article
```

중복된 코드를 최소화하고 같이 묶어서 쓰는법

```jsx
import React from 'react';
import { NavLink, Outlet } from 'react-router-dom';

const Articles = () => {
    return (
      <div>
        <Outlet />
        <ul>
          <ArticleItem id={1} />
          <ArticleItem id={2} />
          <ArticleItem id={3} />
        </ul>
      </div>
    );
  };
  
  const ArticleItem = ({ id }) => {
    const activeStyle = {
      color: 'green',
      fontSize: 21,
    };
    return (
      <li>
        <NavLink
          to={`/articles/${id}`}
          style={({ isActive }) => (isActive ? activeStyle : undefined)}
        >
          게시글 {id}
        </NavLink>
      </li>
    );
  };

export default Articles
```

## NotFound Page만들기

NotFound페이지는 경로가 지정되지 않은 페이지로 주소가 갈 때 이를 해결해주는 페이지 이다.

`NotFound.jsx`

```jsx
import React from 'react';

const NotFound = () => {
    return(
        <div
            style={% raw %}{{
            display: 'flex',
            alignItems: 'center',
            justifyContent: 'center',
            fontSize: 64,
            position: 'absolute',
            width: '100%',
            height: '100%',
            }}{% endraw %}
         >
        404
        </div>
    )
}

export default NotFound;
```

App.jsx 에 NotFound를 축가

```jsx
<Route path="*" element={<NotFound/>}/>
```

## Navigate 컴포넌트를 이용한 loginpage

`MyPage.jsx`

```jsx
import React from 'react';
import { Navigate } from 'react-router-dom';

const MyPage = () => {
    const isLogIn = false;
    
    if(!isLogIn){
        return <Navigate to="/login" replace={true}/>
    }

    return (
        <>My Page</>
    )
}

export default MyPage;
```

Navigate 컴포넌트를 통해 로그인이 되지 않으면 login page로 가게 설정

`Login.jsx`

```jsx
import React from 'react'

const Login = () => {
    return <>로그인 페이지</>;
  };
  
export default Login;
```

`App.jsx`

```jsx
<Route path="/login" element={<Login/>}/>
<Route path="/mypage" element={<MyPage/>}/>
```

두개 항목 추가해줄것

내용 

> [https://velog.io/@velopert/react-router-v6-tutorial#64-navigate-컴포넌트](https://velog.io/@velopert/react-router-v6-tutorial#64-navigate-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8)
>