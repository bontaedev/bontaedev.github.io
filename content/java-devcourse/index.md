---
emoji: ๐งข
title: ๋ธ๋ก๊ทธ ํฌ์คํ ์์
date: '2021-01-22 23:00:00'
author: ์ค์ฝ๋ฉ
tags: blog gatsby theme ๊ฐ์ธ ๋น ํ๋ง
categories: ๋ธ๋ก๊ทธ
---

# ๐ ์ ๋ชฉ์ ์ต์ ์์ ๋ถ์ฌ์!

์ผ๋ฐ์ ์ธ ๋ด์ฉ์ ์ด๋ ๊ฒ ์ ์ผ๋ฉด ๋ฉ๋๋ค.

> ์ฌ๊ธฐ๋ quote๋ฅผ ์ ๋ ๋ถ๋ถ! [๋งํฌ](https://github.com/zoomKoding/zoomkoding-gatsby-blog/issues/new) > [์คํ](https://github.com/zoomKoding/zoomkoding.com)๋ ๋ธ๋ก๊ทธ ํ๋ง!โญ๏ธ

# ๐ง ์ฝ๋๋ธ๋ญ์ ์ด๋ ๊ฒ ์๋ ฅ

single quotation์ ์ฐ๋ฉด `code block`

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/zoomkoding/zoomkoding-gatsby-blog)

## ๐โโ๏ธ ์คํํ๊ธฐ

์๋์ฒ๋ผ ์๋ ฅํ๋ฉด ์ฌ๋ฌ์ค์ ์ฝ๋๋ธ๋ญ๋ ์๋ ฅ๊ฐ๋ฅ!

```bash
# Install dependencies
$ npm install

# Start development server
$ npm start
```

```java
System.out.println("hello java");
```

<br/>

์ ๋ช๋ น์ด๊ฐ ๋ฌธ์  ์์ด ์คํ๋๋ค๋ฉด [http://localhost:8000](http://localhost:8000)์์ ๋ธ๋ก๊ทธ๋ฅผ ํ์ธํ์ค ์ ์์ต๋๋ค.

### 1. ๋ธ๋ก๊ทธ ๊ธฐ๋ณธ ์ ๋ณด

```js
title: '' // zoomkoding.com
description: '' // ์ค์ฝ๋ฉ์ ๊ฐ๋ฐ์ผ๊ธฐ
language: 'ko', // 'ko', 'en' (์์ด ๋ฒ์ ๋ ์ง์ํ๊ณ  ์์ต๋๋ค.)
siteUrl: '' // https://www.zoomkoding.com
ogImage: '/og-image.png', // ๊ณต์ ํ  ๋ ๋ณด์ด๋ ๋ฏธ๋ฆฌ๋ณด๊ธฐ ์ด๋ฏธ์ง๋ก '/static' ํ์์ ๋ฃ๊ณ  ์ถ์ ์ด๋ฏธ์ง๋ฅผ ์ถ๊ฐํ์๋ฉด ๋ฉ๋๋ค.
```

### 2. ๋๊ธ ์ค์ 

๋ธ๋ก๊ทธ ๊ธ๋ค์ ๋๊ธ์ ๋ฌ ์ ์๊ธธ ์ํ์ ๋ค๋ฉด utterances๋ฅผ ํตํด์ ์ด๋ฅผ ์ค์ ํ์ค ์ ์์ต๋๋ค.

> ๐ฆ utterances ์ฌ์ฉ๋ฐฉ๋ฒ์ [๋งํฌ](https://utteranc.es/)๋ฅผ ์ฐธ๊ณ ํด์ฃผ์ธ์!

```js
comments: {
    utterances: {
        repo: '' // zoomkoding/zoomkoding-gatsby-blog
    },
}

```

### 3. ๊ธ์ด์ด ์ ๋ณด

๊ธ์ด์ด(author)์ ์๋ ฅํ์  ์ ๋ณด๋ ํํ์ด์ง์ about ํ์ด์ง ์๋จ์ ์๋ ๊ธ์ด์ด๋ฅผ ์๊ฐํ๋ ์น์์ธ bio์์ ์ฌ์ฉ๋ฉ๋๋ค. **description**์ ์์ ์ ์ค๋ชํ๋ ๋ฌธ๊ตฌ๋ค์ ๋ฃ์ผ๋ฉด ์ ๋๋ฉ์ด์์ผ๋ก ๋ณด์ฌ์ง๊ฒ ๋ฉ๋๋ค. bio์ ๋ค์ด๊ฐ๋ ์ด๋ฏธ์ง๋ฅผ ๋ฐ๊พธ์๋ ค๋ฉด `assets`์ ์ํ์๋ ํ์ผ์ ์ถ๊ฐํ์๊ณ  ํ์ผ์ ์ด๋ฆ์ **thumbnail**์ ๋ฃ์ด์ฃผ์๋ฉด ๋ฉ๋๋ค.(gif๋ ์ง์ํฉ๋๋ค!)

์์ดํฐ ๋ฏธ๋ชจํฐ์ฝ์ผ๋ก thumbnail์ ๋ง๋๋ ๋ฐฉ๋ฒ์ด ๊ถ๊ธํ์๋ฉด [์ด ๊ธ](https://www.zoomkoding.com/memoji-to-gif/)์ ์ฐธ๊ณ ํด์ฃผ์ธ์!

> ๐ค ์์์ ์ค์ ํ ์ธ์ด์ ๋ฐ๋ผ description์ ํฌ๋งท์ด ๋ฌ๋ผ์ง๋๋ค.

```js
author: {
    name: '์ ์งํ',
    bio: {
      role: '๊ฐ๋ฐ์',
      description: ['์ฌ๋์ ๊ฐ์น๋ฅผ ๋๋', '๋ฅ๋์ ์ผ๋ก ์ผํ๋', '์ด๋ก์ด ๊ฒ์ ๋ง๋๋'],
      thumbnail: 'zoomkoding.gif',
    },
    social: {
      github: 'https://github.com/zoomKoding',
      linkedIn: 'https://www.linkedin.com/in/jinhyeok-jeong-800871192',
      email: 'zoomkoding@gmail.com',
    },
},
```

## ๐โโ๏ธ about page ๋ง๋ค๊ธฐ

about ํ์ด์ง ๋ํ gatsby-meta-config.js๋ฅผ ํตํด ์์ฑ๋ฉ๋๋ค. about ํ์์ ์๋ timestamps์ projects์ ๊ฐ๊ฐ ์ ๋ณด๋ฅผ ์๋ ฅํ์๋ฉด about ํ์ด์ง๊ฐ ์๋ ์์ฑ๋ฉ๋๋ค.

### 1. timestamps

์๋์ ๊ฐ์ด ๊ฐ timestamp ์ ๋ณด๋ฅผ ๋ฐฐ์ด๋ก ์ ๊ณตํด์ฃผ์๋ฉด ์๋ ฅํ์  ์์์ ๋ง์ถฐ์ timestamps section์ ๋ณด์ฌ์ง๊ฒ ๋ฉ๋๋ค.

> links์ ํด๋น ์ ๋ณด๊ฐ ์๋ค๋ฉด ์๋ตํด๋ ๋ฉ๋๋ค.

```js
{
    date: '2021.02 ~',
    activity: '๊ฐ์ธ ๋ธ๋ก๊ทธ ๊ฐ๋ฐ ๋ฐ ์ด์',
    links: {
        post: '/gatsby-starter-zoomkoding-introduction',
        github: 'https://github.com/zoomkoding/zoomkoding-gatsby-blog',
        demo: 'https://www.zoomkoding.com',
    },
},
```

### 2. projects

๋ง์ฐฌ๊ฐ์ง๋ก ๊ฐ project ์ ๋ณด๋ฅผ ๋ฐฐ์ด๋ก ์ ๊ณตํด์ฃผ์๋ฉด ์๋ ฅํ์  ์์์ ๋ง์ถฐ์ projects section์ ๋ณด์ฌ์ง๊ฒ ๋ฉ๋๋ค.

```js
{
  title: '๊ฐ๋ฐ ๋ธ๋ก๊ทธ ํ๋ง ๊ฐ๋ฐ',
  description:
    '๊ฐ๋ฐ ๋ธ๋ก๊ทธ๋ฅผ ์ด์ํ๋ ๊ธฐ๊ฐ์ด ์กฐ๊ธ์ฉ ๋์ด๋๊ณ  ์ ์  ๋ง์ ์๊ฐ๊ณผ ๊ฒฝํ์ด ๋ธ๋ก๊ทธ์ ์์๊ฐ๋ฉด์ ์  ์ด์ผ๊ธฐ๋ฅผ ๋ด๊ณ  ์๋ ๋ธ๋ก๊ทธ๋ฅผ ์ง์  ๋ง๋ค์ด๋ณด๊ณ  ์ถ๊ฒ ๋์์ต๋๋ค. ๊ทธ๋์ ์ฌ๋ฌ ๊ฐ๋ฐ ๋ธ๋ก๊ทธ๋ฅผ ๋ณด๋ฉด์ ์ข์๋ ๋ถ๋ถ๊ณผ ๋ถํธํ๋ ๋ถ๋ถ๋ค์ ๋ฐํ์ผ๋ก ๋ ํผ๋ฐ์ค๋ฅผ ์ฐธ๊ณ ํ์ฌ ์ง์  ๋ธ๋ก๊ทธ ํ๋ง๋ฅผ ๋ง๋ค๊ฒ ๋์์ต๋๋ค.',
  techStack: ['gatsby', 'react'],
  thumbnailUrl: 'blog.png',
  links: {
    post: '/gatsby-starter-zoomkoding-introduction',
    github: 'https://github.com/zoomkoding/zoomkoding-gatsby-blog',
    demo: 'https://www.zoomkoding.com',
  }
}
```

<br/>

๊ทธ๋ ๊ฒ ๋ด์ฉ์ ๋ฌธ์  ์์ด ์๋ ฅํ์จ๋ค๋ฉด ๋๋ง์ ๋ธ๋ก๊ทธ๊ฐ ํ์ํ ๊ฒ์ ํ์ธํ์ค ์ ์์ต๋๋ค.๐

> ๋ณ๋์ฌํญ์ ์คํ ์ค์ธ ๋ธ๋ก๊ทธ์์ ํ์ธํ์๋ ค๋ฉด `npm start`๋ฅผ ํตํด ์ฌ์คํํด์ฃผ์ธ์!

## โ๏ธ ๊ธ ์ฐ๊ธฐ

๋ณธ๊ฒฉ์ ์ผ๋ก ๋ธ๋ก๊ทธ์ ๊ธ์ ์ฐ๋ ค๋ฉด `/content` ์๋์ ๋๋ ํ ๋ฆฌ๋ฅผ ์์ฑํ๊ณ  `index.md`์ markdown์ผ๋ก ์์ฑํ์๋ฉด ๋ฉ๋๋ค.

> ์ด ๋, ํด๋์ ์ด๋ฆ์ ๊ฒฝ๋ก๋ฅผ ์์ฑํ๋๋ฐ ๋ฉ๋๋ค.

### ๐ ๋ฉํ ์ ๋ณด

index.md ํ์ผ์ ์๋จ์๋ ์๋์ ๊ฐ์ด emoji, title, date, author, tags, categories ์ ๋ณด๋ฅผ ์ ๊ณตํด์ผ ํฉ๋๋ค.

> emoji๋ ๊ธ๋จธ๋ฆฌ์ ๋ณด์ฌ์ง๊ฒ ๋๋ฉฐ, categories๋ ๋์ด์ฐ๊ธฐ๋ก ๋๋์ด ์ฌ๋ฌ๊ฐ๋ฅผ ์๋ ฅํ  ์ ์์ต๋๋ค.

```
---
emoji: ๐งข
title: Getting Started
date: '2021-03-22 23:00:00'
author: ์ค์ฝ๋ฉ
tags: tutorial
categories: tutorial
---
```

### ๐ผ ์ด๋ฏธ์ง ๊ฒฝ๋ก

๊ธ์ ์ด๋ฏธ์ง๋ฅผ ์ฒจ๋ถํ๊ณ  ์ถ์ผ์๋ค๋ฉด ๊ฐ์ ๋๋ ํ ๋ฆฌ์ ์ด๋ฏธ์ง ํ์ผ์ ์ถ๊ฐํ์์ ์๋์ ๊ฐ์ด ์ฌ์ฉํ์๋ฉด ๋ฉ๋๋ค.

```
![์ฌ์ง](./[์ด๋ฏธ์ง ํ์ผ๋ช])
```

### ๐ ๋ชฉ์ฐจ ์์ฑ

๊ธ์ ์ฐ์ธก์ ๋ชฉ์ฐจ๊ฐ ๋ณด์ด๊ธฐ๋ฅผ ์ํ์ ๋ค๋ฉด `index.md` ํ์ผ ๋งจ ์๋์ ๋ค์ ๋ด์ฉ์ ์ถ๊ฐํ์๋ฉด ์๋์ผ๋ก ๋ชฉ์ฐจ๊ฐ ์์ฑ๋ฉ๋๋ค.

    ```toc
    ```

### ๐ก ๋ฒ๊ทธ ๋ฆฌํฌํธ & ๋ฌธ์

๊ถ๊ธํ์  ์ ์ด ์์ผ์๋ค๋ฉด [์ด์](https://github.com/zoomKoding/zoomkoding-gatsby-blog/issues/new)๋ก ๋จ๊ฒจ์ฃผ์๋ฉด ์ต๋ํ ๋น ๋ฅด๊ฒ ๋ต๋ณ ๋๋ฆฌ๋๋ก ํ๊ฒ ์ต๋๋ค!๐โโ๏ธ

> ๐ค ํน์ ํน์  ๊ธฐ๋ฅ์ด ์์ด์ ํ๋ง ์ฌ์ฉ์ ๋ง์ค์ด์๊ฑฐ๋ ์ ์ํ๊ณ  ์ถ์ผ์  ๊ธฐ๋ฅ์ด ์์ผ์๋ค๋ฉด,  
> ๐ [์ฌ๊ธฐ](https://github.com/zoomKoding/zoomkoding-gatsby-blog/issues/40)์ ๋๊ธ ๋จ๊ฒจ์ฃผ์ธ์! ์ ๊ทน์ ์ผ๋ก ๋ฐ์ํ๊ฒ ์ต๋๋ค :)

```toc

```
