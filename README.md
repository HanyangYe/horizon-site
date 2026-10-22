# 地平线文化科技公司 · 官方网站

HORIZON 单页官网，纯静态实现（HTML + CSS + 原生 JavaScript），无构建步骤、无外部依赖。

## 线上地址

| 项目 | 值 |
|---|---|
| 站点 | https://hanyangye.github.io/horizon-site/ |
| 仓库 | https://github.com/HanyangYe/horizon-site |
| 可见性 | Public |
| 发布源 | `main` 分支、`/`（根目录） |
| 构建方式 | 分支部署（Legacy），**无 CI** |

## 目录结构

```
.
├── index.html              # 单页站点全部内容
├── css/style.css           # 样式（含响应式断点）
├── js/main.js              # 交互：滚动显现、导航状态、移动端菜单、数字滚动
├── assets/
│   ├── logo.png / favicon.png
│   ├── fonts/              # 品牌字体子集（woff2）
│   ├── cases/              # 代表作品配图
│   └── partners/           # 合作机构标识
└── .nojekyll               # 跳过 GitHub Pages 的 Jekyll 处理
```

全部资源均使用**相对路径**引用，因此既能部署在 `https://<user>.github.io/<repo>/` 这样的项目子路径下，也能在自有域名根目录下正常访问。

## 本地预览

站点无需构建，任选一种方式启动静态服务：

```bash
python -m http.server 8093
# 打开 http://localhost:8093
```

> 直接双击 `index.html` 也能打开，但建议用本地服务器，保证字体与图片加载行为与线上一致。

## 更新部署

### 方式一：git 提交（推荐，需能直连 github.com）

```bash
git add -A
git commit -m "更新内容"
git push
```

Pages 会自动重新发布，通常 1 分钟内生效。

### 方式二：REST API 脚本（代理拦截 github.com 时使用）

本机网络曾拦截 `github.com` 的 git 通道（`CONNECT tunnel failed, 502`），但 `api.github.com` 可正常访问，因此改用 Git Data API 提交。效果与 `git push` 等同，只是通道不同。

```bash
# 令牌通过环境变量传入，不写入任何文件
GITHUB_TOKEN=<你的 PAT> python ../deploy_pages.py
```

脚本行为：复用已有仓库 → 为每个文件创建 blob → 建 tree（整树替换）→ 提交（父提交为当前 `main`）→ 强制更新 `main` → 读取 Pages 构建状态。

> 注意：该脚本执行的是**整站覆盖**，本地目录被删除的文件在远端也会消失。适合一次性同步全站。

### 首次发布时的两个坑（已解决，供后续参考）

1. **空仓库无法走 Git Data API**：GitHub 会对空仓库返回 `409 Git Repository is empty`。脚本会先用 Contents API 提交一个最小文件作为引导提交，再批量写入其余文件。
2. **必须先创建提交再开 Pages**：`POST /repos/{owner}/{repo}/pages` 在仓库无任何提交时会失败。

## 维护提示

- 联系邮箱（`contact@horizon-culture.cn`）与页脚 ICP 备案号为**占位内容**，正式对外前请替换为真实信息。
- 图片为 webp 格式并启用懒加载；替换配图时建议保持同等宽高比，避免布局跳动。
- 合作机构标识统一为黑标白底 640×220 画布、内容高度 128px，替换时请沿用同一规格以保持视觉一致。
- 站点内容中不含任何个人身份信息；主理人按品牌资料展示为林楚杰。
