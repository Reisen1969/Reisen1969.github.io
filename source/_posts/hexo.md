---
title: 使用hexo
categories: note
tags: [hexo]
---

使用hexo的一些记录


## 建站
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```
这个文件夹/主目录 作为 `main` 分支的文件夹, 我打算将`gh-pages`作为我的主页面.


## 一些快捷命令

```
$ hexo server
```
生成网站并本地预览


```
$ hexo deploy
```
可以一件部署到github
需要事先 在 `_config.yml`添加
```
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  # example, https://github.com/hexojs/hexojs.github.io
  branch: gh-pages
```

在 主目录执行 
```
 npm install hexo-deployer-git --save
```
安装git插件.

## github自动化处理

使用 node --version 指令检查你电脑上的 Node.js 版本，并记下该版本
在储存库中建立 .github/workflows/pages.yml，并填入以下内容 (将 16 替换为上个步骤中记下的版本)：

```
.github/workflows/pages.yml
name: Pages

on:
  push:
    branches:
      - main # default branch

jobs:
  pages:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 16.x
        uses: actions/setup-node@v2
        with:
          node-version: "16"
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

## 主题
在 blog/_config.yml 文件中找到并修改：

`theme: volantis`

在主目录执行 `npm i hexo-theme-volantis`

更新主题:
更新时，把 `package.json` 中的版本号改为 `*` 再执行 `npm i` 就可以了。

[自定义设置](https://volantis.js.org/v6/theme-settings/#%E7%BD%91%E7%AB%99%E4%B8%8E%E6%96%87%E7%AB%A0%E5%B0%81%E9%9D%A2)
