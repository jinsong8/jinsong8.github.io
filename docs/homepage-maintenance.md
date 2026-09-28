# 主页维护

主页直接基于 [Zhihao Zhang 的主页源码](https://github.com/alanzhangcs/alanzhangcs.github.io)改编，上游版本为 `063fd8cbbb2e2e3ac925828d3b3d260be983772c`。保留原版布局、Lato 字体、布局尺寸、颜色、响应式样式、主题切换、滚动导航高亮、新闻展开和论文图片灯箱。`assets/css/homepage.css` 基于上游 `stylesheet.css`，保留原作者文件注释，并增加本地字体和 SVG 图标样式。交互脚本保留在页面布局中，主题图标改由 CSS 随主题切换。

本项目继续使用 Jekyll / GitHub Pages，以 Liquid 模板渲染个人资料：

- `_data/homepage.yml`：新闻、论文、教育、实习、奖项和学术服务。带日期的内容按时间倒序排列，`academic_services` 记录服务角色及会议名称。
- `_pages/about.md`：个人简介、研究方向及各版块模板。
- `_layouts/homepage.html`：由原版 `index.html` 改编的页面框架及交互脚本。
- `assets/css/homepage.css`：原版样式及本地字体、SVG 图标样式。
- `_includes/homepage-icon.html`：Font Awesome Free 6.5.1 的 6 个原版 SVG 图标，内嵌到 HTML，避免下载整套图标字体。保留各 SVG 的版权注释，完整许可证见 `assets/fontawesome-LICENSE.txt`。
- `assets/fonts/lato/`：与原 Google Fonts CSS 相同的 Lato v25 WOFF2 文件，包含 400/700、正体/斜体及 Latin/Latin Extended 子集；保留 `font-display: swap` 和 Unicode 范围，浏览器按需下载。许可证见同目录 `OFL.txt`。
- `_data/navigation.yml`：顶部导航。链接使用 `#about` 格式，与原版滚动高亮脚本一致。
- `_config.yml`：姓名、头像、邮箱、Scholar 和 GitHub 等资料。`avatar_webp_200` / `avatar_webp_400` 配置响应式 WebP 头像，`avatar` 保留原头像回退。邮箱使用 `author.email_display`，当前以 `[at]` 替代 `@`；`author.email` 留空，避免旧模板输出明文 `mailto:` 链接。
- `images/portrait-200.webp`、`images/portrait-400.webp`：200/400px、质量 80 的头像，浏览器根据显示尺寸和像素密度选其一；头像在首屏正常加载。
- `images/publications/thumbnails/`：最长边 320px 的 WebP（质量 85）和 JPEG（质量 80）缩略图，保留懒加载和异步解码。
- `images/publications/full/`：从论文原始页面重新下载的完整分辨率 PNG，保持文件原样，只在点击对应缩略图时请求。原 `images/publications/` 下的 640px JPEG/WebP 保留旧链接，但不再参与当前页面的加载。
- `images/favicon-photo-32.png`、`images/favicon-photo-16.png`：由个人头像降采样得到的浏览器标签页图标。

新闻不超过 12 条时全部显示，隐藏展开按钮；超过 12 条时显示最新 12 条，其余由 Show earlier news 按钮展开。`date` 使用 `2026.08` 格式，`datetime` 使用 `2026-08` 格式。

研究方向放在个人介绍中，紧接合作交流邀请之前，不设独立 Research 栏目。Email 按钮定位到联系方式。邮箱的 `[at]` 写法仅减少简单地址抓取，无法保证防止垃圾邮件，也不会移除历史版本或其他网站已公开的地址。

论文的 `first_author: true` 在会议信息旁显示 First author；作者列表中的 Song Jin 自动加粗。`paper` 和 `image` 必填，`code` 可选。`thumbnail` / `thumbnail_webp` 是列表缩略图，`image` 是点击后显示的原始 PNG。缺少 thumbnail 时回退到 image；缺少 thumbnail_webp 时使用 JPEG 缩略图。RecInter 的完整论文标题为 Beyond Static Testbeds: An Interaction-Centric Agent Simulation Platform for Dynamic Recommender Systems。TagPR 的 EMNLP 2026 Main 录用信息由主页作者提供。

## 插图来源

所有插图来自本人论文的 arXiv HTML 版本；列表缩略图保留完整内容与宽高比，降低分辨率以加快加载，放大图保持原始文件：

| 论文 | 图号 | 来源 |
| --- | --- | --- |
| AllocEmbed | Figure 3 | https://arxiv.org/html/2609.01778v1/picture2_cropped.png |
| TagPR | Figure 3 | https://arxiv.org/html/2509.23140v1/pic_main_v1.png |
| DiningBench | Figure 1 | https://arxiv.org/html/2604.10425v1/main_pic1.png |
| ViPER | Figure 1 | https://arxiv.org/html/2510.24285v1/pics/main1.png |
| FinRpt | Figure 1 | https://arxiv.org/html/2511.07322v1/pipeline3.png |
| RecInter | Figure 1 | https://arxiv.org/html/2505.16429v1/fig1.2.png |

2026-09-28 从上述链接重新下载放大图，原始像素尺寸分别为 AllocEmbed 1410×760、TagPR 1388×681、DiningBench 3146×1646、ViPER 3428×1932、FinRpt 1581×689、RecInter 1589×855。`full/` 中 PNG 与下载文件逐字节一致；只有列表缩略图经过缩放和压缩。

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

首页仍为 `/`，保留 `/about/` 和 `/about.html` 跳转以及原有版块锚点。仅在配置了 Google Analytics ID 时加载对应统计脚本。

## 加载优化

首页不再请求 Google Fonts CSS 或 cdnjs 的 Font Awesome CSS/字体。Lato 字体从本站加载，首屏使用的 Latin 正体 400/700 通过 preload 提前请求。CSS 链接带版本参数，修改样式时同步更新参数，避免部署后短时间内混用新 HTML 与旧 CSS。

访客地图及其脚本、样式已删除，不再向该地图服务发起请求。论文图片继续懒加载，并使用异步解码。

论文图片由上表中的原始 PNG 生成：以白色背景合成透明通道，使用 Pillow 的 Lanczos 等比例缩放，WebP 使用 method=6 编码。六张 320px WebP 缩略图合计 82,104 字节，相比此前六张 640px WebP 的 253,674 字节减少约 67.6%。头像的 200/400px WebP 分别为 3,650 / 9,818 字节，原 512px 头像为 13,251 字节。

原图地址仅出现在论文缩略图链接中，没有 img/source/preload 引用；初始化和滚动都不会请求原图。点击时灯箱先显示缓存中的缩略图，再请求该论文的完整分辨率 PNG 并替换，灯箱仅显示图片和关闭按钮。加载失败保留缩略图；关闭或切换论文后，过期请求不会覆盖当前灯箱。支持 WebP 的浏览器不会同时下载 JPEG 缩略图回退。传输量下降不等于首屏渲染时间同比下降，实际耗时需结合网络测试判断。

Lato 文件来源为原 Google Fonts 返回的 `fonts.gstatic.com/s/lato/v25/` URL；许可证来自 `google/fonts` 仓库的 `ofl/lato/OFL.txt`。SVG 和图标许可证来自 `FortAwesome/Font-Awesome` 仓库的 `6.5.1` 标签。
