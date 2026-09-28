# 主页维护

主页直接基于 [Zhihao Zhang 的主页源码](https://github.com/alanzhangcs/alanzhangcs.github.io)改编，上游版本为 `063fd8cbbb2e2e3ac925828d3b3d260be983772c`。保留原版 HTML 结构、Lato 字体、布局尺寸、颜色、响应式样式、主题切换、滚动导航高亮、新闻展开和论文图片灯箱。`assets/css/homepage.css` 是上游 `stylesheet.css` 的逐字节副本，保留原作者文件注释。原版内联交互脚本保留在页面布局中。

本项目继续使用 Jekyll / GitHub Pages，以 Liquid 模板渲染个人资料：

- `_data/homepage.yml`：新闻、论文、教育、实习、奖项和学术服务。带日期的内容按时间倒序排列，`academic_services` 记录服务角色及会议名称。
- `_pages/about.md`：个人简介、研究方向及各版块模板。
- `_layouts/homepage.html`：由原版 `index.html` 改编的页面框架及交互脚本。
- `assets/css/homepage.css`：原版样式表。
- `_data/navigation.yml`：顶部导航。链接使用 `#about` 格式，与原版滚动高亮脚本一致。
- `_config.yml`：姓名、头像、邮箱、Scholar 和 GitHub 等资料。邮箱使用 `author.email_display`，当前以 `[at]` 替代 `@`；`author.email` 留空，避免旧模板输出明文 `mailto:` 链接。
- `images/publications/`：各篇论文的真实框架插图，压缩为最长边 640px、质量 75 的 JPEG；缩略图和灯箱均使用该轻量版本，保留懒加载。
- `images/favicon-photo-32.png`、`images/favicon-photo-16.png`：由个人头像降采样得到的浏览器标签页图标。

新闻不超过 12 条时全部显示，隐藏展开按钮；超过 12 条时显示最新 12 条，其余由 Show earlier news 按钮展开。`date` 使用 `2026.08` 格式，`datetime` 使用 `2026-08` 格式。

研究方向放在个人介绍中，紧接合作交流邀请之前，不设独立 Research 栏目。Email 按钮定位到联系方式。邮箱的 `[at]` 写法仅减少简单地址抓取，无法保证防止垃圾邮件，也不会移除历史版本或其他网站已公开的地址。

论文的 `first_author: true` 在会议信息旁显示 First author；作者列表中的 Song Jin 自动加粗。`paper` 和 `image` 必填，`code` 可选。RecInter 的完整论文标题为 Beyond Static Testbeds: An Interaction-Centric Agent Simulation Platform for Dynamic Recommender Systems。TagPR 的 EMNLP 2026 Main 录用信息由主页作者提供。

## 插图来源

所有插图来自本人论文的 arXiv HTML 版本，保留完整内容与宽高比，降低分辨率以加快加载：

| 论文 | 图号 | 来源 |
| --- | --- | --- |
| AllocEmbed | Figure 3 | https://arxiv.org/html/2609.01778v1/picture2_cropped.png |
| TagPR | Figure 3 | https://arxiv.org/html/2509.23140v1/pic_main_v1.png |
| DiningBench | Figure 1 | https://arxiv.org/html/2604.10425v1/main_pic1.png |
| ViPER | Figure 1 | https://arxiv.org/html/2510.24285v1/pics/main1.png |
| FinRpt | Figure 1 | https://arxiv.org/html/2511.07322v1/pipeline3.png |
| RecInter | Figure 1 | https://arxiv.org/html/2505.16429v1/fig1.2.png |

## 本地运行

安装 Ruby 和 Bundler 后，在项目目录运行：

```sh
bundle install
bundle exec jekyll serve
```

构建静态页面：

```sh
bundle exec jekyll build
```

首页仍为 `/`，保留 `/about/` 和 `/about.html` 跳转以及原有版块锚点。原有访客地图和已配置时的 Google Analytics 也保留。
