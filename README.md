# freefigure · 免费的科研插图网站

当前使用 **GitHub Pages 纯静态版**，不需要 Cloudflare、R2 或数据库，不需要因本方案绑定支付方式。

预期网址：https://mengfeiwangdmu.github.io/freefigure/

## 第一次启用（仓库所有者操作一次）

打开仓库 **Settings → Pages → Build and deployment**：

- Source：**Deploy from a branch**
- Branch：**main**
- Folder：**/docs**
- 点击 **Save**。

等待 Pages 构建部署完成，再打开上面网址；保存成功不等于部署已经成功。部署记录在 Actions 中查看。

以后提交 main 中 docs/ 下的文件，GitHub Pages 会自动更新。无需本地构建或输入部署命令。

如果你还连接着 Cloudflare Builds，可在 Cloudflare 关闭该项目自动构建或断开 Git 连接，避免继续尝试旧 R2 部署。不要开通 R2。

## 上传素材

1. 打开仓库 `docs/assets/`。
2. 点击 **Add file → Upload files**，上传素材和可选缩略图，提交。
3. 打开 `docs/assets.json`，点击铅笔，补充一条素材记录，再提交。
4. 等待 Pages 自动发布。浏览器可能需要刷新才能看到更新。

首张素材可以把 assets.json 的 `[]` 替换为（文件名要与实际上传的一致）：

```json
[
  {
    "id": "cell-001",
    "title": "B细胞",
    "title_en": "B cell",
    "category": "细胞",
    "description": "飞老师原创。非商业性学术使用。",
    "description_en": "Original by Teacher Fei. For non-commercial academic use.",
    "file": "assets/b-cell.svg",
    "preview": "assets/b-cell-preview.webp",
    "format": "SVG",
    "tags": ["B细胞", "免疫", "B cell"],
    "published": true
  }
]
```

没有单独预览图时，删掉 `preview` 字段，网站将显示原图。列表预览适用 SVG、PNG、JPG 或 WebP；其他格式原文件请另配可显示的预览图。需要隐藏时设置 `published:false`。但仓库是公开的，隐藏只是不显示在页面，仓库文件和 Git 历史仍可查看，不适合存放保密材料。

现有分类：细胞、细胞器、分子与受体、组织与器官、实验与仪器。

`id` 不可重复。路径必须相对于 docs/，以 `assets/` 开头。建议英文文件名，不使用空格；注意大小写。多条记录用逗号分隔，最后一条后不加逗号。英文名称和说明可选。

目前没有放入未经你上传的素材，首页为空是正常状态。

## 修改网页与记录

- **docs/index.html**：实际发布的首页，包含文案、CSS、分类和双语字典。
- **docs/assets.json**：实际发布的素材清单。
- **docs/assets/**：实际发布的素材及缩略图。
- **docs/fonts/**：备用毛笔字体及许可。

GitHub 打开文件 → 铅笔 → 编辑 → Commit changes。主页只发布 docs 文件夹，旧版的 content/、src/、wrangler.jsonc 等 Cloudflare 文件留在仓库中作迁移参考，不参与 Pages 发布，不需要去改。

留言使用仓库 Issues，用户需 GitHub 账号。如果留言入口不可用，请在仓库 Settings → General → Features 启用 Issues。

新增学习记录可直接编辑首页 journal 区块。尚未实现完整博客系统。

## 本地预览和验证

安装 Node.js 后，在仓库根目录运行：

```sh
node scripts/validate-pages.mjs
```

需要本地预览时，可在 docs 目录运行 Python 自带 HTTP 服务：

```sh
cd docs
python -m http.server 8000
```

然后打开 http://localhost:8000 。不要直接双击 HTML 测试素材清单，因为浏览器可能禁止 file:// 页面读取 JSON。

## 免费范围与容量

GitHub Free 支持公开仓库的 Pages。官方限制包括：已发布网站不超过 1GB，源仓库建议不超过 1GB，每月流量软限制 100GB。免费不是无限容量；超出可能受限，不应把 GitHub 当作大型网盘。

这是个人科研素材和学习分享网站，不使用付费 Actions、自托管服务或自定义付费域名。未来若引入交易、会员或付费服务，应重新核实 Pages 使用政策和托管方案。

官方限制：https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits
发布设置：https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

原创素材按网站非商业性许可使用；公开仓库并不自动授予全部代码和素材的无限制使用权。第三方字体许可见 docs/fonts/OFL.txt。
