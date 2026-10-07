# kuige.me — 魁歌 KuiGe 主页

独立开发者 [魁歌 KuiGe](https://kuige.me/)（GitHub：[Tliens](https://github.com/Tliens)）的官方主页，展示所有免费在线工具与作品。

**线上地址：** https://kuige.me/

## 收录的作品

| 作品 | 地址 | 仓库 |
|---|---|---|
| AI Rank · 大模型排行榜 + AI 热榜资讯 | https://ai-model-rank.kuige.me/ | ai-model-rank |
| TokenLens · Token 计数器 | https://tokenlens.kuige.me/ | TokenLens |
| JSON Lens · JSON 工具箱 | https://jsonlens.kuige.me/ | jsonlens |
| SSE Inspector · SSE 调试器 | https://sse-inspector.kuige.me/ | sse-inspector |
| Stream Inspector · 流媒体调试工具箱（拉流 + 音频分析） | https://stream-inspector.kuige.me/ | stream-inspector |
| 魁歌建站指南 · 零基础 9 步建站教程 | https://fast-site.kuige.me/ | fast-site |
| PicSqueeze · 图片压缩 | https://picsqueeze.kuige.me/ | picsqueeze |
| ShareForge · 分享图生成器 | https://shareforge.kuige.me/ | shareforge |
| Rednote Formatter · 文案排版 | https://rednote-formatter.kuige.me/ | rednote-formatter |
| X热榜 · X/Twitter 博主人气排行 | https://xhot.kuige.me/ | xhot |
| Indie Gems · 独立开发者作品收录 | https://indie-gems.kuige.me/ | indie-gems |
| GitHub Gems · 宝藏开源项目导航 | https://github-gems.kuige.me/ | github-gems |
| 群星闪耀 · 影响世界的人 | https://world-shapers.kuige.me/ | world-shapers |
| SongGems · 免费 CC 音乐播放器 | https://songgems.kuige.me/ | songgems |
| MarkGone · 图片在线去水印 | https://markgone.kuige.me/ | markgone |
| VidGone · 视频在线去水印 | https://vidgone.kuige.me/ | vidgone |
| CastLens · 免费在线录屏 | https://castlens.kuige.me/ | castlens |
| PhotoGems · 免费图片画廊 | https://photogems.kuige.me/ | photogems |
| 明史 · 明代历史知识站 | https://ming-history.kuige.me/ | ming-history |
| IconGems · 图标插画宝库 | https://icongems.kuige.me/ | icongems |
| SkillGems · AI 智能体技能精选目录 | https://skillgems.kuige.me/ | skillgems |

> 2026-09-28 合并：AI Hot Board（AI 热榜）并入 [AI Rank](https://ai-model-rank.kuige.me/) 的热榜资讯板块；Audio Inspector（在线音频分析）并入 [Stream Inspector](https://stream-inspector.kuige.me/) 的音频分析工具页（`/audio.html`）。原域名保留为跳转页，不再单列。

## 说明

- 单文件纯静态页面（`index.html`），无构建、无依赖，直接部署到任意静态托管即可。
- 卡片缩略图直接引用各作品站点的 `og-image.png`，新增作品时在 `index.html` 的 `.grid` 里复制一张卡片并改链接即可。
- 旧 Hexo 博客内容备份在 `hexo-blog-2023` 分支。

## 主站 2.0 结构（2026-10 改版）

页面顺序：Hero（主句「把想法变成产品，把产品变成资产」+ X 关注主按钮 + 最近上线横条）→ 01 Now 构建日志 → 02 Latest Thoughts 近期思考（私藏文章 + FEATURED_URL 指定的 X 代表作）→ 03 Featured Products 精选八品 → 04 Archive 作品档案（其余工具 + Apps + 开源）→ 05 About → FAQ 品牌问答 → Contact → 数据带。

### 如何更新 X 长文（Latest Thoughts）

1. 编辑 [`articles.json`](articles.json)：封面图存入 `covers/`，在 `articles` 数组最前面加一条 `{ "date", "url", "title", "excerpt", "cover" }`（可附 `title_en` / `excerpt_en`）。
2. 页面加载时会 `fetch('articles.json')` 渲染；读取失败时回退到 `index.html` 内置的 `THOUGHTS_FALLBACK`（两处保持同步，或至少保证 json 可访问）。
3. 标题与封面的免登录抓取法：直接打开 `x.com` 的文章 status 页，`og:description` 即完整标题，`og:image` 即封面（`pbs.twimg.com` 链接可另存）；文章发布时间可从 status ID 反推：`(id >> 22) + 1288834974657` 得到毫秒时间戳。

### 如何发布私藏文章（src: "mine"）

不发在 X 上的个人长文走这条路径：

1. 封面图存入 `covers/`（`cwebp -q 82 输入图 -o covers/article-N.webp`）。
2. 全文页建在 `articles/` 下（如 `articles/zhongyong.html`，单文件静态页，风格与 `/articles/` 二级页一致：同一套主题变量、星空背景、页头页脚 + Cloudflare 统计）。
3. `articles.json` 最前面加一条，加字段 `"src": "mine"`，`url` 填站内绝对路径（如 `/articles/zhongyong.html`），二级页会归到「私藏文章」分类；`articles/index.html` 的 `FALLBACK` 同步加一条。
4. 新页面加进 `sitemap.xml`。私藏文章会自动出现在主页 Latest Thoughts（并同步 `index.html` 的 `THOUGHTS_FALLBACK`）；X 长文仍只展示 `FEATURED_URL` 指定的代表作。
