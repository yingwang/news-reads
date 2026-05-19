# news-reads

每天早上把过去 24 小时全球新闻整理成一份结构化中文 brief，五个板块覆盖地缘政治、经济与市场、科技与 AI、科学与气候、社会与文化，发布为 GitHub Pages 静态站点。

Live site: https://yingwang.github.io/news-reads/

## 结构

每天一篇，固定五段：

- **地缘政治与国际关系** - 战争、外交、制裁、领导人会晤
- **经济与市场** - 主要股指、汇率、利率、央行、关税政策、显著经济数据
- **科技与 AI** - 模型发布、产品发布、并购、关键论文、半导体动态
- **科学与气候** - 科研突破、太空、气候事件
- **社会与文化** - 重大社会事件、艺术、体育（仅当有真正全球影响时）

每条新闻 2-4 句，第一句陈述事实，第二句给上下文，第三句视情况给意义。整篇控制在 1200-2000 中文字之间。

风格遵循 `feedback_writing_style_chinese.md` 与 `feedback_writing_no_compression.md`：展开写，不缩略，书面体，不口语化，不用中文破折号，不用 emoji，不用 LLM 收尾。让事实自己说话，不替读者评价新闻好坏。

## 仓库布局

```
news-reads/
├── docs/
│   ├── index.md                          # 落地页（最新一篇全文）
│   └── news/
│       ├── YYYY-MM-DD.md                 # 每日 brief
│       └── ...
├── mkdocs.yml                            # MkDocs Material 配置
└── .github/workflows/deploy-docs.yml     # 构建与部署管线
```

## 自动化

笔记由 [yingwang/claude-skills](https://github.com/yingwang/claude-skills) 里的 `news-daily` skill 生成。每天早上 07:43 cron 自动调用 `/news-daily`：抓取当日全球新闻，写成中文 brief，发到 Telegram，再把 md 写进本仓库 `docs/news/YYYY-MM-DD.md`，覆盖 `docs/index.md` 为最新一篇，更新 `mkdocs.yml` 导航，提交并推送。GitHub Actions 随后构建静态站点并部署到 GitHub Pages。

## 本地构建

```bash
pip install \
    "mkdocs-material>=9.5" \
    "mkdocs-awesome-pages-plugin>=2.10" \
    "pymdown-extensions>=10.7" \
    "mkdocs>=1.6" \
    "mdx-truly-sane-lists>=1.3"

mkdocs serve
```

本地站点服务于 `http://localhost:8000/news-reads/`。

## License

本仓库的中文 brief 采用 Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International 协议发布。详见 [LICENSE](LICENSE)。引用的新闻事实归各原始来源所有，本站只做摘要与上下文整理。
