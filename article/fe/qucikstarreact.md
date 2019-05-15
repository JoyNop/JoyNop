t> 前几天给准备了一些简单的简单的`React`教程，之前在做团队项目的时候，用了大佬们的框架，直接刷刷写就OK，可是当自己去配置一些东西的时候，发现事情并没有那么简单，用了两天的时间反复折腾一些UI，配置TypeScript，每一步都十分艰辛

## 创建React项目 

> 这里我们首先采用`FaceBook`制作的[Create-React—App](https://github.com/facebook/create-react-app) 这个`Cli`，用脚手架的原因就是，比较方便嘛，先配制出一个架子来，以后慢慢深入，自己造轮子？当然，造轮子是对个人技术的检验和学习，也并非会用于正式生产


### 通过`creat-react-app` 创建一个React项目

**Quick Overview**

  - 创建React项目

   1. npx
   ```bash
   npx create-react-app my-app
   ```
     
   (npx comes with npm 5.2+ and higher, see instructions for older npm versions)

   2. npm
   ```bash
   npm init react-app my-app
   ```
   npm init <initializer> is available in npm 6+

   3. Yarn
   ```bash
   yarn create react-app my-app
   ```
   (npx comes with npm 5.2+ and higher, [see instructions for older npm versions](https://gist.github.com/gaearon/4064d3c23a77c74a3614c498a8bb1c5f)  )

Then open `http://localhost:3000/` to see your app.
When you’re ready to deploy to production, create a minified bundle with `npm run build`.

![demo](https://camo.githubusercontent.com/29765c4a32f03bd01d44edef1cd674225e3c906b/68747470733a2f2f63646e2e7261776769742e636f6d2f66616365626f6f6b2f6372656174652d72656163742d6170702f323762343261632f73637265656e636173742e737667)

**通过creat-react-app创建TypeScript项目**

```bash
create-react-app my-app --scripts-version=react-scripts-ts
```

在这里我们采用这个，并且使用`yarn`安装，为后续TypeScript项目提供支持

### 安装对Stylus的支持

创建完项目后，要执行`yarn eject` (npm 安装执行`npm eject`) 也就是打开全部配置项。 

安装依赖：`yarn stylus stylus-loader`

找到`config`里面的两个配置文档。

配置的内容都是一样的。

关于`stylus`不多解释，网上太多了。文档后缀是 `.styl `

#### 修改webpack.config.prod.js

- 找到`oneOf:[]`

在里面按照模板内容添加

```json
{ 
  test: /\.styl$/, 
  loaders: ['style-loader', 'css-loader', 'stylus-loader'], 
},

```
- 找到`file-loader`

对照修改为以下内容

```json
{
  loader: require.resolve('file-loader'),
  // Exclude `js` files to keep "css" loader working as it injects
  // it's runtime that would otherwise processed through "file" loader.
  // Also exclude `html` and `json` extensions so they get processed
  // by webpacks internal loaders.
  exclude: [/\.(js|jsx|mjs)$/, /\.html$/, /\.json$/ ,/\.styl$/],
  options: {
              name: 'static/media/[name].[hash:8].[ext]',
            },
},
```

#### 修改webpack.config.dev.js

与修改`webpack.config.dev.js`相同

