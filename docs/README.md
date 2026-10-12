# WorkNotes 个人工作笔记

> 基于 [Docsify](https://docsify.js.org/#/) 搭建的静态个人知识库，用于记录工作问题、技术方案、踩坑笔记与项目总结。

- 仓库目录：`C:\Users\lwh\Documents\个人\WorkNotes`
- 站点目录：`C:\Users\lwh\Documents\个人\WorkNotes\docs`
- 版本：Docsify v5（`docsify@5`）

---

## 一、站点功能说明

本站已实现以下能力（对应 README 中列出的原始需求）：

| 需求 | 实现方式 |
| --- | --- |
| 暗黑主题 | 加载 `core.min.css`（亮色）+ `core-dark.min.css`，默认**跟随系统**深浅色；右上角悬浮按钮可手动切换 自动/暗色/亮色，选择保存在 `localStorage` |
| 访问不同目录、不同层级的 `.md` 文件 | 三层目录结构（机器视觉算法 / 上位机软件开发 / 项目总结），由 `_sidebar.md` 嵌套组织，可逐层展开 |
| 内容搜索 | 引入 `search` 插件，`paths: 'auto'` 按侧边栏自动建索引，支持跨文档全文搜索 |
| 发布到 GitHub + GitHub Pages | 见下文「四、发布到 GitHub 与 GitHub Pages」 |

其他增强：首页封面（`_coverpage.md`）、顶部导航（`_navbar.md`）、图片点击放大（zoom-image）、站外链接新窗口打开、代码块圆角与滚动条美化。

---

## 二、目录结构

```
WorkNotes/
├── docs/                      # 站点根目录（GitHub Pages 发布根）
│   ├── index.html             # docsify 入口（核心配置）
│   ├── README.md              # 站点首页（本文件）
│   ├── _sidebar.md            # 侧边导航
│   ├── _navbar.md             # 顶部导航
│   ├── _coverpage.md          # 首页封面
│   ├── .nojekyll              # 禁止 Jekyll，保证 GitHub Pages 正常解析
│   ├── guide.md               # docsify init 示例残留（未使用）
│   ├── MachineVisionAlgorithmDevelopment/   # 机器视觉算法开发
│   │   ├── 数字图像处理基础.md
│   │   ├── 工具Halcon.md / 工具OpenCV.md / 工具VisionPro.md
│   │   └── assets/            # 图片资源
│   ├── PCSoftwareDevelopment/ # 上位机软件开发
│   │   ├── 编程语言CSharp.md / 编程语言C++.md / 编程语言Python.md
│   │   ├── 组件Autofac.md / 组件Serilog.md / 组件Swagger.md
│   │   ├── 工具DBeaver.md / 工具Linux与Windows.md / 工具Nginx.md
│   │   ├── 工具Sqlsugar.md / 工具VS2026.md / 工具VSCode.md
│   │   ├── VS-WPF与MVVM.md / 前端知识.md / 常用通讯协议知识.md
│   └── ProjectSummary/        # 项目总结
│       ├── 上海-利德项目-细胞样本前处理设备.md
│       ├── 大连-海尔项目-液体样本前处理设备.md
│       └── 济南-凯晨项目-病毒样本浓度测定与效价测定自动化设备.md
```

> 命名说明：URL 中的 `#` 会被当作锚点导致链接失效，因此 C# 笔记的文件名直接使用 `编程语言CSharp.md`（避开 `#`），链接无需编码。

---

## 三、本地启动方式

1. 安装 Node.js（当前环境已装 `v22.23.2`），全局安装 docsify-cli：

   ```powershell
   npm i docsify-cli -g
   ```

2. 进入站点目录并启动本地服务：

   ```powershell
   cd "C:\Users\lwh\Documents\个人\WorkNotes\docs"
   docsify serve .
   ```

3. 浏览器打开：<http://localhost:3000/>

> 无需构建，Docsify 直接读取 `.md` 文件，改完刷新即可。

**CDN 网络备选**：`index.html` 使用 `cdn.jsdelivr.net`，国内网络有时访问缓慢或超时（浏览器会白屏）。若遇到，可把 `index.html` 中所有 `//cdn.jsdelivr.net` 全局替换为 `//fastly.jsdelivr.net` 或 `//unpkg.com` 再刷新。

---

## 四、发布到 GitHub 与 GitHub Pages

当前仓库已在本地初始化（`git init`），但**尚未配置远程仓库、也尚无提交**。首次发布步骤如下：

1. 在 GitHub 新建一个**空仓库**（例如 `WorkNotes`），**不要**勾选自动生成 README/.gitignore。

2. 本地关联远程并提交：

   ```powershell
   cd "C:\Users\lwh\Documents\个人\WorkNotes"
   git add .
   git commit -m "初始化 WorkNotes docsify 知识库"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/WorkNotes.git
   git push -u origin main
   ```

3. 在 GitHub 仓库页面打开 **Settings → Pages**，Source 选择：

   - Branch：`main`，目录选 **`/docs`**（因为站点文件放在 docs 子目录），保存。

4. 稍等片刻，站点即发布于：

   `https://<你的用户名>.github.io/WorkNotes/`

5. 发布后建议把 `index.html` 里的 `repo: ''` 填成仓库地址，侧边栏页脚会出现 GitHub 编辑链接。

> `.nojekyll` 文件已存在，GitHub Pages 会跳过 Jekyll 处理，确保 `_sidebar.md` 等以下划线开头的文件被正常当作资源提供。

---

## 五、维护规范

1. **新增笔记**：在对应分类目录下创建 `.md` 文件，并同步把链接加入 `_sidebar.md`（必要时补 `_navbar.md`）。
2. **修改配置/结构后**：同步更新本 README（目录结构、功能说明、版本信息等）。
3. **图片**：统一放在分类下的 `assets/` 目录，引用相对路径。
4. **文件名**：避免空格与 URL 特殊字符（如 `#`、`&`、`?`）；C# 笔记统一命名为 `编程语言CSharp.md`。
5. **提交**：每次变更后提交 git，并推送远端以更新 GitHub Pages。

---

## 六、相关链接

- Docsify 官方快速开始：<https://docsify.js.org/#/zh-cn/quickstart>
- Docsify 配置项：<https://docsify.js.org/#/configuration>
- 主题：Docsify v5 Themes（core / core-dark）
