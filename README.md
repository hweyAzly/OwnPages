# 个人主页

一个纯静态的个人主页项目。零依赖、零构建，改一个文件就能变成你自己的站点，直接部署到 GitHub Pages。

## 特性

- **零构建**：没有 npm、没有打包，`index.html` 双击就能看
- **单文件配置**：所有文字、链接、项目都写在 `assets/js/content.js` 一个文件里
- **跟随系统主题**：默认深色，右上角可切换，选择会记住
- **响应式**：手机、平板、桌面都适配
- **自带 SEO**：标题、描述、分享卡片、结构化数据都齐了
- **细节**：滚动渐入、打字机、鼠标跟随柔光、平滑锚点、`prefers-reduced-motion` 支持

## 目录结构

```
P/
├── index.html              页面骨架（一般不用改）
├── 404.html                404 页面
├── favicon.svg             网站图标
├── robots.txt              搜索引擎规则（需改域名）
├── sitemap.xml             站点地图（需改域名）
├── .nojekyll               让 GitHub Pages 跳过 Jekyll 处理
├── assets/
│   ├── css/style.css       样式
│   ├── js/content.js       ★ 内容配置，改这里
│   ├── js/main.js          渲染与交互逻辑
│   └── img/                图片放这里（头像、项目截图）
└── README.md
```

## 第一步：改成你自己的内容

打开 `assets/js/content.js`，从上往下改：

| 字段 | 改什么 |
|---|---|
| `meta.title` | 浏览器标签页标题，建议「你的名字 · 关键词」 |
| `meta.description` | 一句话介绍，会出现在搜索结果和分享卡片里 |
| `meta.url` | 部署后的完整网址，如 `https://yourname.github.io` |
| `profile.name` | 你的名字（也会作为头像占位的首字母） |
| `profile.avatar` | 头像路径，如 `assets/img/avatar.jpg`；留空则显示首字母 |
| `profile.role` | 一句话身份，如「全栈开发者 · 独立创作者」 |
| `profile.tagline` | 打字机循环播放的几句话，建议 2–4 句 |
| `profile.email` | 你的邮箱（决定所有「联系我」按钮的跳转） |
| `profile.socials` | 社交链接，按需增删 |
| `about` | 关于我的段落、数字统计、技能标签 |
| `work.projects` | 作品列表，建议 3–6 个 |
| `path.items` | 经历时间线 |
| `footer.icp` | 备案号（没有就留空，留空不显示） |

改完保存，刷新浏览器即可看到效果。

> 提示：可以用记事本改，但推荐用 [VS Code](https://code.visualstudio.com/)，改错了能一眼看出语法问题。

## 第二步：本地预览

**最简单**：双击 `index.html`，浏览器直接打开。

**更接近线上**（推荐，路径行为一致）：

```bash
# 在项目目录下执行
python -m http.server 8000
```

然后浏览器访问 <http://localhost:8000>。

## 第三步：部署到 GitHub Pages

### 方式 A：`用户名.github.io` 仓库（推荐，网址最短）

1. 登录 [GitHub](https://github.com)，右上角 **+** → **New repository**
2. 仓库名必须填 **`你的用户名.github.io`**（例如 `zhangsan.github.io`），选 **Public**，不要勾选任何初始化文件，点 **Create repository**
3. 把项目文件传上去，两种方法任选：

   **网页上传（不用装任何软件）**
   - 在仓库页点 **uploading an existing file**
   - 把 `P` 目录里的**所有文件和文件夹**拖进去
   - 注意：要拖内容，不要拖 `P` 文件夹本身
   - 底部点 **Commit changes**

   **命令行**
   ```bash
   cd "D:/Desktop/教程/个人/P"
   git init
   git add .
   git commit -m "init: personal site"
   git branch -M main
   git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
   git push -u origin main
   ```

4. 回到仓库 → **Settings** → 左侧 **Pages**
5. **Source** 选 `Deploy from a branch`，Branch 选 **main**，目录选 **/(root)**，点 **Save**
6. 等 1–3 分钟，刷新页面，顶部会出现你的网址：`https://你的用户名.github.io`

### 方式 B：普通仓库名

如果仓库叫 `mysite`，站点地址就是 `https://你的用户名.github.io/mysite/`。
配置步骤同上，只是访问时多一层路径。

本项目所有资源都用**相对路径**，放在子目录下也能正常工作。

### 以后怎么更新

改完文件后重新上传或 `git push`，Pages 会在 1 分钟左右自动重新发布。

## 第四步（可选）：绑定自己的域名

1. 在域名商（阿里云、腾讯云、Cloudflare 等）添加一条 CNAME 记录：
   - 主机记录：`www`，记录值：`你的用户名.github.io`
   - 如果想用裸域名（`example.com`），添加 4 条 A 记录指向 GitHub 的 IP（见官方文档）
2. 仓库 **Settings → Pages → Custom domain** 填入你的域名，点 Save
3. 勾选 **Enforce HTTPS**，证书会自动签发（通常几分钟到几小时）

绑定后记得把 `meta.url`、`robots.txt`、`sitemap.xml` 里的网址一起改掉。

## 常见问题

**打开是空白页？**
按 `F12` 看 Console 有没有红色报错。多数情况是 `content.js` 里少了个逗号或引号。

**样式没生效？**
检查 `assets/css/style.css` 路径大小写。GitHub Pages 跑在 Linux 上，**大小写敏感**，`Style.css` 和 `style.css` 是两个文件。

**改了内容但线上没变？**
浏览器缓存，强制刷新（`Ctrl + F5`）；或者去仓库 **Actions** 看部署是否还在进行。

**部署后图片不显示？**
图片要放进 `assets/img/`，路径写相对路径，如 `assets/img/avatar.jpg`。

**GitHub 访问慢？**
可以换 Cloudflare Pages 或 Vercel，流程类似：连上 GitHub 仓库，构建命令留空，输出目录填 `/`。

## 想加点什么

| 想要 | 怎么做 |
|---|---|
| 博客 | 加一个 `blog/` 目录，用 Markdown 生成静态页，或直接用 Jekyll/Hugo |
| 访问统计 | 接 [Umami](https://umami.is/) 或 [Plausible](https://plausible.io/)，加一段 script |
| 评论 | [Giscus](https://giscus.app/)，基于 GitHub Discussions，纯静态可用 |
| 暗色/亮色跟随时间 | 在 `content.js` 里加个时间判断，调 `initTheme` 的默认值 |

---

祝你上线顺利。
