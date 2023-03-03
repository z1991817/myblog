---
title: "GithubAction报错"
date: 2023-03-03T11:10:49+08:00
draft: true
---

### gitAction突然报错，不会自动构建发布了
原因是我的脚本把``` hugo ```的版本放成最近版本

``` javascript
- name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.92.2'
          extended: true
```
目前换成本地版本，本地版能可以打包成功
