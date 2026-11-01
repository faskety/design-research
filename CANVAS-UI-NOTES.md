# Canvas UI 设计美学

*快照：2026 年 11 月 1 日 · 来源：[canvasui.dev](https://canvasui.dev/) 线上页面，视口 1024px，数值取自 computed style*

**一句话：画廊式克制。界面是白墙，色彩和动效全部留给展品。**

## 核心思想

1. **色彩是奖励，不是装饰。** 首页的界面本身全是中性灰，彩色只出现在 hero 面板和被悬停的那张卡片上。灰度卡片一悬停才变彩色，色彩因此有了"被唤醒"的戏剧性。
2. **独特感来自用法，不是 token。** 色值与 `study/shadcn-ui_ui` 的 neutral 默认值一致，也没有品牌色。辨识度来自边框透明度、虚线、嵌套和字距。
3. **用线不用影。** 首页只有 1 个元素带阴影（5% 黑）。层级靠 1px 细线和极淡的底色区分，虚线又给页面一种"工程图纸"的气质。
4. **展示即证明。** 演示不是截图而是真组件在运行；"How it works" 用 UI 自己演示流程（光标移动、选中、进度条）。
5. **只有一处高潮。** 页面主体克制到近乎冷淡，收尾突然切到深色 CTA 面板，配蓝色粒子。这是首页末尾唯一一次明显的情绪释放。

## 色彩

| Token | Light | Dark |
|---|---|---|
| background | `#fff` | `#0a0a0a` |
| foreground | `#0a0a0a` | `#fafafa` |
| card | `#fff` | `#171717` |
| muted | `#f5f5f5` | `#262626` |
| muted-foreground | `#737373` | `#a1a1a1` |
| border | `#e5e5e5` | `#ffffff1a` |

关键在透明度叠加：`border/60`、`border/70`、`border/40`，`muted/30`、`background/60`。同一个 token 分几档，不新增颜色。

文档侧栏用小蓝点标记部分组件，是浏览过程中见到的唯一彩色 UI 元素。

## 排版

字体：Geist Sans + Geist Mono。**首页字重只用 400 和 500**，没有 bold。

| 层级 | 字号 / 行高 | 字重 | 字距 | 备注 |
|---|---|---|---|---|
| H1 | `clamp(2.25rem, 5.5vw, 3.75rem)` / 1.04 | 500 | -0.05em | `text-wrap: balance` |
| H2 | 36 / 40px | 500 | -0.05em | `text-wrap: balance` |
| 卡片标题 | 15 / 22.5px | 500 | -0.025em | |
| 正文 | 16 / 28px | 400 | normal | muted 色，`text-wrap: pretty` |
| 小节标签 | 12px | 400 | 0.1em | Mono，全大写，muted |
| 按钮 | 15px | 500 | -0.01em | |

记忆点：**大字极紧、行高极贴，小字松弛、行高宽裕**，靠这种反差出气质，而不是靠字重。Mono 标签 + 紧缩大标题是每个区块的固定开场。

## 版式

- 容器 `max-w-6xl`（1152px），两侧 32px，区块上下 128px，大量留白。
- 容器左右各一条 1px 虚线导轨：`repeating-linear-gradient` 画 4px 实 / 5px 空，底部 288px 用 mask 渐隐。
- 区块之间用虚线分隔（`border-t border-dashed border-border/60`），与导轨相交处有小刻度。整页像一张标注过的图纸。
- 区块节奏交替：居中 hero → 跑马灯画廊 → 左右分栏 → 反向分栏 → 深色收尾。

## 组件配方

**同心嵌套卡片（标志性做法）**

外层圆角 18px + 内边距 8px → 内层圆角 10px。正好满足 `外圆角 = 内圆角 + 内边距`，所以弧线同心。对应 [界面设计技巧](DESIGN-CRAFT.md) 第 11 条。

```css
.card  { border-radius: 18px; padding: 8px;
         border: 1px solid color-mix(in oklab, var(--border) 60%, transparent);
         background: color-mix(in oklab, var(--muted) 30%, transparent); }
.inner { border-radius: 10px;
         border: 1px dashed color-mix(in oklab, var(--border) 70%, transparent);
         background: color-mix(in oklab, var(--background) 60%, transparent); }
```

画廊卡片用的是这组数值。代码块、Agent 对话框、Newsletter 表单和浏览器窗口演示也是同一种双层外壳，一种容器走天下。

**灰度画廊卡片**

```css
video { filter: grayscale(1); transition: filter .3s ease-out; }
.card:hover video { filter: grayscale(0); }
/* 亮色模式下反相，让深色素材融入白底 */
:root:not(.dark) video { filter: grayscale(1) invert(1) hue-rotate(180deg); }
```

一份素材同时适配两套主题，不用录两遍。悬停时底部浮出 `from-black/75` 渐变和标题描述，平时卡片上没有任何文字。

**毛玻璃**：只用在悬浮层上。导航 `bg/70 + blur(24px) saturate(1.5)`，saturate 让透过来的颜色不发灰。hero 上的数据卡压在彩色噪点图上，是首页主要的大面积玻璃。

**其他**

- 主按钮：44px 高的黑色胶囊，配箭头，`active: scale(.98)`。次按钮常常只是文字加箭头。
- 滑块：把整行做成填充条（32px 高，圆角 10px），标签和数值都在条内，不用细轨道加圆点。
- 数字卡：大号数字 + Mono 小字说明（`35 / AND COUNTING`）。

## 动效

主要缓动是 `cubic-bezier(0.23, 1, 0.32, 1)`（快起慢停），入场与展开都不用回弹。

| 场景 | 参数 |
|---|---|
| Hero 文字入场 | 600ms，`translateY(12px)` + fade，每项错开 60ms（`--enter-index`） |
| Hero 面板入场 | 1s，`clip-path: inset(0 0 98% round 1rem)` → `inset(0 round 1rem)`，像幕布拉开 |
| 按压反馈 | 150ms，`scale(.98)` / 小按钮 `.95` |
| 悬停 | 色彩 300ms，覆盖层 200ms |
| 步骤进度 | 5.2s 线性 `scaleX(0→1)`，当前步骤下方走一条细线 |
| 跑马灯 | `translate(-50%)` 循环，两端 8% mask 渐隐 |

组件上写了 `motion-reduce:transition-none`，尊重减弱动效设置。

## 文案

短句、陈述、有节奏：*Copy, paste, ship.* / *Every component, alive on canvas.* / *One component, six flavors.* 不用感叹号，不堆形容词。

## 适用边界

- 这套打法**依赖展品本身足够好看**。如果内容是数据或文字，白墙就只是空，要换成让数据当展品。
- 平铺 shadcn 默认值不等于这个效果，要照搬的是虚线、同心嵌套、灰度转彩色这些用法。
- 虚线和 Mono 标签用多了会变成"开发者网站"模板感，适合技术产品，不适合情绪化的内容。

## 未验证

- WebGL 组件的实际光标交互没有逐个试，只看了静态画面和悬停态。
- 没有测手机宽度。
- 暗色模式是手动切 class 查看的，只看了 hero 和画廊。
- `/components` 和组件详情页截图时还在加载或过渡中，只确认了双栏布局与悬浮侧栏，卡片和内容细节未评估。
