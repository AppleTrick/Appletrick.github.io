---
title: gitblog 구글 서칭하게 만들기
author:
  name: Changhee Park
  link: https://github.com/Appletrick
date: 2022-05-21 01:00:00 +0900
categories: [Blogging]
description: 설명
tags: [블로그, blog, Google Search, Google]
---

# Google Search Console로 접속하기

[https://search.google.com/search-console/about](https://search.google.com/search-console/about) 에 접속한다.

<img width="754" alt="스크린샷 2022-05-21 오후 4 50 44" src="https://user-images.githubusercontent.com/31761527/169642548-6439eb3d-675a-492d-9ca3-e93059bbd32f.png">

gitblog가 존재할 경우 URL 접두어 부분에 gitblog 사이트 입력을 해준다.

<img width="645" alt="스크린샷 2022-05-21 오후 4 29 18" src="https://user-images.githubusercontent.com/31761527/169642566-223fd624-116c-4173-bb41-5e979774b8f9.png">

html 파일을 다운로드 후에 root의 동일한 위치에 파일을 위치해준다.

# sitemap.xml 생성하기

```
---
layout: null
---

<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
        xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    {% for post in site.posts %}
    <url>
        <loc>{{ site.url }}{{ post.url }}</loc>
        {% if post.lastmod == null %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
        {% else %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
        {% endif %}

        {% if post.sitemap.changefreq == null %}
        <changefreq>weekly</changefreq>
        {% else %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
        {% endif %}

        {% if post.sitemap.priority == null %}
        <priority>0.5</priority>
        {% else %}
        <priority>{{ post.sitemap.priority }}</priority>
        {% endif %}

    </url>
    {% endfor %}
</urlset>
```

sitemap.xml 을 생성후에 아까와 동일하게 root의 위치와 동일하게 위치해준다.

# robots.txt 생성하기

```jsx
User-agent: *
Allow: /

Sitemap: URL/sitemap.xml
```

URL 에 자신의 URL을 입력해주고 robots.txt root의 위치와 동일하게 위치해준다.

# Google Search에 sitemap 설정해주기

<img width="1368" alt="스크린샷 2022-05-21 오후 5 04 33" src="https://user-images.githubusercontent.com/31761527/169642572-2457369c-1457-4e60-849a-77d249efa039.png">

새 사이트 맵에 sitemap.xml 을 추가해준다.

현재 사진과 같이 가져올수 없음이라고 뜨는데.. 오래걸릴수도 있다고한다. 결과가 나오면 다시 포스팅 수정할것임

# 참고

[https://ip99202.github.io/posts/깃허브-블로그-구글-검색-가능하게-하기/](https://ip99202.github.io/posts/%EA%B9%83%ED%97%88%EB%B8%8C-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EA%B5%AC%EA%B8%80-%EA%B2%80%EC%83%89-%EA%B0%80%EB%8A%A5%ED%95%98%EA%B2%8C-%ED%95%98%EA%B8%B0/)

[https://velog.io/@eona1301/Github-Blog-검색창-노출시키기](https://velog.io/@eona1301/Github-Blog-%EA%B2%80%EC%83%89%EC%B0%BD-%EB%85%B8%EC%B6%9C%EC%8B%9C%ED%82%A4%EA%B8%B0)
