# 演示文稿模板

从 `1020/index.html` 抽取的通用模板，与 1020、0918 一样使用单个 HTML 保存页面、样式和交互。直接用浏览器打开 `index.html`，无需安装依赖或联网。

## 文件

- `index.html`：8 页版式示例，CSS 在顶部 `<style>`，JavaScript 在底部 `<script>`，示例图使用内联 SVG。
- `logo.png`：左下角 Logo，从 1020 复制。
- `README.md`：风格规范与使用说明。

## 配色与风格

浅色背景、蓝色主色、细边框、留白、简洁卡片。避免过多装饰和厚重阴影。颜色在 HTML 顶部 `:root` 中集中修改。

| 变量 | 色值 | 用途 |
| --- | --- | --- |
| `--blue` | #0067b1 | 章节、强调、箭头、进度条 |
| `--blue-soft` | #edf7fe | AI 回复、强调卡片 |
| `--ink` | #151719 | 正文 |
| `--muted` | #697177 | 次要说明、来源、页码 |
| `--line` | #d9dde0 | 边框、分隔线 |
| `--paper` | #fbfcfc | 页面背景 |
| `--white` | #ffffff | 卡片 |
| `--warm` | #fff9e6 | 设计者发言、待确认事项 |
| `--warm-line` | #ead28a | 黄色边框 |
| `--warm-ink` | #8a6500 | 黄色区域文字强调 |
| `--green` | #19734b | 确认规则、结果 |
| `--green-soft` | #eef7f1 | 结果背景 |

外部浏览器背景为 #e9ecee，蓝色边框为 #9fc9e6 / #b8d8ec。颜色配合文字标签使用。

## 字体与字号

默认字体 `Verdana, Arial, sans-serif`；中文由系统无衬线字体回退显示。所有字号按 1280 × 720 画布计算，随页面整体缩放。

| 元素 / 选择器 | 字号 | 字重与行高 |
| --- | --- | --- |
| 封面标题 `h1` | 46px | 默认粗体，1.08 |
| 封面副标题 `.opening-subtitle` | 25px | 常规，1.3 |
| 页面标题 `h2` | 22px | 默认粗体，1.4 |
| 卡片标题 `h3` | 22px | 默认粗体，1.2 |
| 正文 `p, li` | 16px | 常规，1.45 |
| 对话、总结条、术语 | 16px | 常规，约 1.4–1.45 |
| 章节 `.topline` | 16px | 800，大写，字距 .04em |
| 讲者日期 `.title-meta` | 16px | 常规 |
| 步骤 `.step` | 30px | 700 |
| 流程箭头 `.arrow` | 28px | 常规 |
| 来源 `.source-label` | 14px | 常规 |
| 页码 `.counter` | 11px | 常规 |
| 组织说明 `.logo-caption` | 10px | 粗体 |

标题过长时主动拆行，正文过多时精简或拆页，详细解释放入讲稿。

## 画布、布局与间距

16:9，固定 1280 × 720。浏览器按可用宽高整体缩放。普通页上边距 28px、左右 48px、下边距 66px；页眉高 26px，与正文间隔 16px；正文组件间隔 18px。卡片间距 24px、内边距 26px、圆角 10px、边框 1px。标题下有细分隔线。

示例包括封面、三列卡片、横向流程、设计对话、术语对照、大图缩放、配色展示和结尾。每个 `<section class="slide">` 是一页，复制后替换文字即可，页数自动计算。

- `.grid.two` / `.grid.three`：两列 / 三列。
- `.card` / `.card.accent`：普通 / 浅蓝卡片。
- `.flow` / `.arrow`：步骤与连接。
- `.bubble.designer`：靠右黄色设计者发言；`.bubble`：靠左蓝色 AI 回复。
- `.result`：绿色确认结论；`.band`：蓝色总结条。
- `.terms` / `.term-row`：两列术语表。
- `.source-label`：底部来源与边界说明。

## 左下角 Logo 与页脚

| 元素 | 参数 | 修改入口 |
| --- | --- | --- |
| Logo | 宽 64px，高度按比例；左 18px、下 6px；z-index 10 | `.deck-logo` |
| 组织说明 | 左 94px、下 15px；10px 粗体；蓝色 | `.logo-caption` |
| 页码 | 右 118px、下 28px；11px 灰色 | `.counter` |
| 按钮组 | 右 24px、下 18px；间距 8px | `.nav` |
| 翻页按钮 | 34 × 34px；16px；白底灰边框 | `.nav button` |
| 进度条 | 高 3px，紧贴底部，蓝色，宽度随页码变化 | `.progress` |

这些元素放在所有 section 之外，共享显示。替换 `logo.png` 即可更换 Logo，保持图片比例。组织说明在 HTML 的 `.logo-caption` 中修改。

```html
<img class="deck-logo" src="logo.png" alt="Your organization logo">
<div class="logo-caption">Your team / organization</div>
```

若沿用 1020 的组织名，可改为 `Research and Development China R&amp;D Centre`。

## 操作与复用

复制整个文件夹开始新演示，修改页面 title、封面、讲者日期、组织说明与 Logo。样式在 HTML 顶部修改，翻页逻辑在底部修改。

右方向键 / PageDown / 空格下一页；左方向键 / PageUp 上一页；F 请求全屏。右下角按钮可翻页。大图点击展开，+ / − 缩放，滚动查看，Close 或 Esc 关闭。

示例图在 HTML 中有两份内联 SVG：页面预览和弹窗原图，修改时保持一致。含 ID 的交互区域不要直接重复复制，新图需要独立 ID 与事件。模板不包含逐条 reveal，采用整页切换。

浏览器打印可导出 PDF，关闭浏览器页眉页脚并开启背景图形。打印会展开全部页面，隐藏交互控件及共享页脚；PDF 不包含弹窗内容。需要每页打印 Logo 时，应在各 section 内添加页脚并修改打印样式。导出前检查分页与溢出。

模板保留 1020 的视觉语言，合并了基础样式和通用组件，不是所有专用页面的逐像素复制。需要原页面专用布局时，直接查阅 `../1020/index.html`。已检查本地资源与结构，尚未做跨浏览器视觉验证。
