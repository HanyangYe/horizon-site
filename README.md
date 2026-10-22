# 地平线文化科技公司 · 官方网站

HORIZON 单页官网，纯静态实现（HTML + CSS + 原生 JavaScript），无构建步骤、无外部依赖。

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

## 部署（GitHub Pages）

当前采用「分支部署」：`main` 分支根目录即发布源，无需任何 CI 配置。

- 发布地址：`https://<user>.github.io/<repo>/`
- 资源路径：全部相对路径，子路径部署无需改动
- `.nojekyll` 已包含：跳过 Jekyll 构建，避免下划线开头文件被忽略、并加快发布

### 更新流程

修改本地文件后提交并推送即可，Pages 会自动重新发布（通常 1 分钟内生效）：

```bash
git add -A
git commit -m "更新内容"
git push
```

## 维护提示

- 联系邮箱与备案号目前为占位内容，正式上线前请替换为真实信息。
- 图片为 webp 格式并启用懒加载；替换配图时建议保持同等宽高比，避免布局跳动。
