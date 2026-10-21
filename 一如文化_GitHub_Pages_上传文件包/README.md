# 一如文化 · 企业品牌宣传方案（网页版）

《一如文化 · 企业品牌宣传方案》PDF 的网页版。**单文件、零依赖**：整站只有一个 `index.html`，内联了全部 CSS 与 JavaScript，不加载任何外部字体、图片或 CDN 资源，也没有构建步骤。因此可以在 GitHub Pages 上直接托管，也可以丢到任意静态空间运行。

## 目录结构

```
.
├── index.html                          # 全部内容（结构与样式、交互均内联）
├── .nojekyll                           # 跳过 Jekyll 编译，避免静态资源被忽略
├── .gitignore
└── .github/
    └── workflows/
        └── deploy-pages.yml            # GitHub Actions：push 到 main 即自动发布到 Pages
```

## 方法一：GitHub Pages（推荐，带自动部署）

### 1. 新建仓库并上传

在 GitHub 新建一个空仓库（**不要**勾选 Add a README / .gitignore / license），例如命名为 `yiru-brand-plan`。然后在本机执行：

```bash
cd 一如文化品宣网页-部署包
git init
git add .
git commit -m "feat: 一如文化品宣方案网页版"
git branch -M main
git remote add origin https://github.com/<你的用户名>/yiru-brand-plan.git
git push -u origin main
```

也可以先在 GitHub 网页端建仓，再用 `git clone` 下来，把这几个文件拷进去提交。

### 2. 开启 Pages（只需做一次）

进入仓库 **Settings → Pages**，把 **Source** 改成 **GitHub Actions**（不是 "Deploy from a branch"），保存。

### 3. 触发部署

- 推送 `main` 分支会自动触发 `.github/workflows/deploy-pages.yml`；
- 若想立刻发布：进 **Actions** 标签页 → 选 `Deploy to GitHub Pages` → **Run workflow**。

跑完后，Actions 页面会显示访问地址，通常为：

```
https://<用户名>.github.io/yiru-brand-plan/
```

之后每次改 `index.html` 再 push，网页会自动更新，无需手工操作。

> 注意：分支名默认是 `main`。如果你的默认分支是 `master`，请把 workflow 里 `branches: ["main"]` 一并改掉，或修改默认分支名。

## 方法二：从分支直接发布（不用 Actions）

如果你不想用 GitHub Actions：

1. 新建一个 `gh-pages` 分支，只放 `index.html` 和 `.nojekyll`；
2. 在 **Settings → Pages** 里 Source 选 **Deploy from a branch**，分支选 `gh-pages`、目录选 `/ (root)`；
3. 保存，等 1–2 分钟即可访问。

改版时把新的 `index.html` 提交到 `gh-pages` 分支即可。

## 方法三：国内访问友好的替代托管

GitHub Pages 在国内部分地区访问较慢或不稳，可选：

| 平台 | 做法 | 特点 |
| --- | --- | --- |
| Gitee Pages | 新建同名仓库上传文件，服务里开启 Gitee Pages | 国内速度好，需实名认证；更新要手动点"更新" |
| Vercel | 导入 GitHub 仓库，Framework 选 Other，直接 Deploy | 自动 HTTPS、自动部署，国内部分地区可直连 |
| Netlify | 拖拽整个文件夹到 Netlify Drop | 零配置，适合快速上线 |

三个平台都不需要构建命令，纯静态托管即可。

## 绑定自定义域名（可选）

如果想用你们自己的域名（如 `brand.yiruculture.com`）：

1. 仓库根目录放一个 `CNAME` 文件，内容只写一行域名，例如 `brand.yiruculture.com`；
2. 到域名服务商处添加一条 **CNAME 记录**，指向 GitHub Pages 地址（`<用户名>.github.io`）；
3. 在 **Settings → Pages → Custom domain** 填入该域名，勾选 Enforce HTTPS。

## 本地预览

```bash
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

也可以直接双击 `index.html` 打开，效果完全一致。

## 页面说明

- 内容与原 PDF **逐字一致**，未做任何增删改。
- 视觉为宣纸米白 + 墨黑 + 朱砂红的禅意新中式排版，呼应方案中的「墨黑留白」调性红线。
- 长滚动浏览，桌面端左侧固定目录（滚动自动高亮当前章节），窄屏自动切换为顶部折叠菜单。
- 字体使用系统字体栈（思源宋体 / 宋体 / 苹方 / 微软雅黑），跨设备观感稳定，无需联网加载字体。
