---
title: readme 新手搭建一个博客
date : 2021-6-25 19:40:49
tags: Hexo
---

本篇文章主要是为了记录一些基本的操作，我本人也会时常忘记，方便查阅。

搭建本博客，操作如下：

1. 安装 Node.js

2. 安装 Git 

3. 注册 GitHub ,  我的名字： yanrongdeng

4. 安装 Hexo
>
> ~ 打开终端，输入命令：`npm install hexo-cli -g`
>
> ~ 进入项目目录: `cd D:\Project\blog`
>
> ~ 初始化博客的模版文件: `hexo init yanrongdeng.github.io`
>
> ~ 进入博客文件夹: `cd yanrongdeng.github.io`
>
> ~ 安装依赖：`npm install`
>
> ~ 启动服务: `hexo server`
>  缩写成 hexo s (More info: [Server](https://hexo.io/docs/server.html))
>
> ~ 服务地址: `localhost:4000`
>

5. 使用 Hexo 主题
Hexo 默认提供的是 hexo-theme-landscape 主题 , 样式简单，功能较少。
> ~ 下载 yun 主题：`git clone https://github.com/YunYouJun/hexo-theme-yun themes/yun`
>
> ~ 引用 yun 主题：`theme: yun`
> 在 _config.yml 中找到 theme 这个字段，将其后的 landscape 修改为 yun。
> 
>~ 安装渲染器：`npm install hexo-render-pug hexo-renderer-stylus`
>
> pug 是一种模板引擎，可以渲染为 HTML 字符串。类似的还有 ejs，swig 等，语法和设计理念有所不同。
> stylus 是一种 CSS 预处理器，可以渲染为 CSS。类似的还有 scss，less，同样只是语法和设计理念有所差异。
<details>
  <summary>yun主题介绍</summary>
<p>最好的解决方案就是在博客根目录下（不是主题目录）新建 source/_data/yun.yml。（若 source/_data 目录不存在，请新建）</p>
<p>本主题将自定义配置与默认配置进行合并，因此你只需要在 yun.yml 文件中自定义你需要的配置即可，其余仍将自动采用默认配置。</p>
<p>譬如我们需要更换头像。在 yun.yml 中填写。</p>
<p>你可以在 source 文件夹下新建 images 文件夹，用来存储你的图片。</p>
<p>也可以使用 SM.MS 等图床工具配合 PicGo 上传你的图片文件，获取在线链接。</p>
  ``` yml
  avatar:
    url: /images/avatar.jpg # 你的头像图片地址
    rounded: true
    opacity: 1
  ```
  <p>更换主题色彩，比如换成黑色，黑色的十六进制颜色代码是 #000000。</p>
  ```yml
  colors:
    primary: "#000000"
  ```
  <p>这时你的主题色调就会变为黑色。</p>
  <p>这只是一个配置项的简单示例，更多配置你可以参考 Yun 主题文档 或直接在 theme/yun/_config.yml 中查看，并根据自己的需要进行配置。</p>
</details>

6. 生成静态文件
> ~ 清理缓存： ` hexo clean `
>
> ~ 生成静态文件：`hexo generate`
缩写为 hexo g (More info: [Generating](https://hexo.io/docs/generating.html))    

7. 与远程仓库建立关联
> ~ 初始化仓库：`git init`
> ~ 创建并切换分支：`git checkout -b hexo`
> ~ 关联远程仓库：`git remote add origin https://github.com/yanrongdeng/yanrongdeng.github.io`

8. 部署
> ~ 安装插件：`npm install hexo-deployer-git`
在 _config.yml 中配置。
```yml
deploy:
  type: git
  repo: git@github.com:yanrongdeng/yanrongdeng.github.io.git # 仓库名
  branch: master # 默认使用 master 分支
  message: Update Hexo Static Content # 你可以自定义此次部署更新的说明
```
> ~ 部署Hexo：` hexo deploy`
缩写 hexo d (More info: [Deployment](https://hexo.io/docs/one-command-deployment.html))
> ~ 清除缓存:  `hexo clean`  
> ~ 重新部署 Hexo: `hexo deploy -g`
<details>
<summary>https重定向</summary>
hexo deploy 
<p>等待完成后，打开网址 https://你的名字.github.io 就能看到你的线上网站了。</p>
<p>使用 https，http 可能无法正常打开。HTTPS 是多了安全加密的 HTTP，Chrome 浏览器已经默认会显示 http 链接为不安全。</p>
<p>为了安全，建议开启强制 https 跳转。项目地址页面 -> Settings -> Options -> GitHub Pages -> Enforce HTTPS。（翻到下面）</p>
<p>此时，http 网址会自动重定向到 https</p>
</details>

9. 备份与自动部署
```bash
# 添加到缓存区
git add -A
git commit -m "这次做了什么更改，简单描述下即可"
# 推送至远程仓库
git push
# 第一次提交，你可能需设置一下默认提交分支
# git push --set-upstream origin hexo
```
每次推送都要输入这三条命令，你可能觉得有些麻烦。
那么你可以编写 bash 脚本。
譬如，在根目录下新建 update.sh。
```bash
# 如果没有消息后缀，默认提交信息为 `:pencil: update content`
info=$1
if ["$info" = ""];
then info=":pencil: update content"
fi
git add -A
git commit -m "$info"
git push origin hexo
```
此后更新的话，只需要在终端执行 sh update.sh 即可。

10. 开始写作
新建 xxx.md 文件：`hexo new post xxx`
新建目录：`hexo new page xxx`

11. Markdown基本用法
```
标题
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

文本样式
*强调文本*    _强调文本_
**加粗文本** __加粗文本__
==标记文本==
~~删除文本~~
> 引用文本
H~2~O is是液体。
2^10^ 运算结果是 1024。

列表
- 项目
  * 项目
    + 项目
1. 项目1
2. 项目2
3. 项目3
- [ ] 计划任务
- [x] 完成任务

--- 水平分割线

链接
链接: [link](https://www.csdn.net/).
图片: ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hdmF0YXIuY3Nkbi5uZXQvNy83L0IvMV9yYWxmX2h4MTYzY29tLmpwZw)
带尺寸的图片: ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hdmF0YXIuY3Nkbi5uZXQvNy83L0IvMV9yYWxmX2h4MTYzY29tLmpwZw =30x30)
居中的图片: ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hdmF0YXIuY3Nkbi5uZXQvNy83L0IvMV9yYWxmX2h4MTYzY29tLmpwZw#pic_center)
居中并且带尺寸的图片: ![Alt](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9hdmF0YXIuY3Nkbi5uZXQvNy83L0IvMV9yYWxmX2h4MTYzY29tLmpwZw#pic_center =30x30)

<details>
  <summary>使用方式</summary>
</details>  

表格
有下滑线| ：用 &#124; 代替
有换行 ：   用 <br/>


yun主题 
各“引用”的使用方法

> Primary

<div class="success">

> Success

</div>

<div class="warning">

> Warning

</div>

<div class="danger">

> Danger

</div>

<div class="info">

> Info

</div>

```
``` yaml
head:
  css:
    material: https://fonts.googleapis.com/icon?family=Material+Icons
```