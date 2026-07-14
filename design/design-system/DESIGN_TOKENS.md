# Design Tokens - 减肥 PK 小程序

> 版本：v0.1（初稿）  
> 方向：精密陪伴型（Apple Fitness+ × Whoop × Finch）  
> 更新：2026-07-14

---

## 一、色彩体系（Color System）

### 1.1 底色 / 中性色（Neutral - Deep Space）
用 **近黑而非纯黑**，避免屏幕死板；灰阶精细到 10 级，承担 90% 的视觉表达。

| Token | Hex | 用途 |
|---|---|---|
| `--bg-canvas` | `#0A0E1A` | App 最底层背景（深空底） |
| `--bg-elevated-1` | `#12172A` | 卡片背景（第一层浮起） |
| `--bg-elevated-2` | `#1B2138` | 悬浮/激活态（第二层） |
| `--bg-modal` | `#232A47` | 模态、Drawer（第三层） |
| `--line-hairline` | `rgba(255,255,255,0.06)` | 1px 分隔线，若隐若现 |
| `--text-primary` | `#F5F7FF` | 主文字（不用纯白，减眼疲劳） |
| `--text-secondary` | `#9AA3BF` | 次要文字 |
| `--text-tertiary` | `#5A6485` | 提示 / 时间戳 |
| `--text-disabled` | `#3A4160` | 禁用态 |

### 1.2 主色（Brand - Electric Lime）
**只用一个亮色**，承担所有正向反馈（进度、成功、成长）。绿而不俗，带电感。

| Token | Hex | 用途 |
|---|---|---|
| `--brand-primary` | `#C6FF3D` | 主品牌色 / CTA / 关键数据 |
| `--brand-primary-hover` | `#D5FF6B` | Hover 状态 |
| `--brand-primary-dim` | `rgba(198,255,61,0.16)` | 主色底纹 / 徽章底色 |
| `--brand-glow` | `rgba(198,255,61,0.35)` | 关键高光时刻的光晕（克制使用） |

### 1.3 情绪色（Emotion - 极少使用）
中性表达为主，避免"红色警告"式恐吓。

| Token | Hex | 用途 |
|---|---|---|
| `--accent-warm` | `#FF8A4C` | 陪伴色 / 温暖提示 / 勋章 |
| `--accent-info` | `#6BB4FF` | 信息类提示（非警告） |
| `--state-caution` | `#FFB84C` | 需注意（不用红） |
| `--state-danger` | `#FF6B7A` | 仅用于删除等破坏性操作确认 |

> ⚠️ 原则：主色 ≤ 1，情绪色 ≤ 1，其余全靠灰度层次。

---

## 二、字体体系（Typography）

### 2.1 字体族
- **中文**：HarmonyOS Sans SC / 苹方 / 系统默认 sans-serif fallback
- **数字（等宽）**：SF Mono / JetBrains Mono / "Roboto Mono" fallback
- **数字（展示大字号）**：DIN Alternate / Oswald（可选 web font）

### 2.2 尺寸阶（Type Scale）

| Token | Size / Line-height | Weight | 用途 |
|---|---|---|---|
| `--font-display-hero` | 72 / 76 | 700 | 打卡成功页大数字（掉了几斤） |
| `--font-display-l` | 48 / 52 | 600 | 周报、PK 结果数字 |
| `--font-display-m` | 32 / 36 | 600 | 卡片主数据（当前体重） |
| `--font-title-l` | 22 / 30 | 600 | 页面标题 |
| `--font-title-m` | 17 / 24 | 600 | 卡片标题 |
| `--font-body` | 15 / 22 | 400 | 正文 |
| `--font-caption` | 13 / 18 | 400 | 辅助说明 |
| `--font-mono-data` | 15 / 20 | 500 | 表格数据、时间戳（等宽） |
| `--font-tiny` | 11 / 14 | 500 | Tag / Chip |

> 🎯 大数字**必做戏剧化对比**：`72pt / 700` 的主数字 + `13pt / 400` 的单位说明，形成尊严感。

---

## 三、间距（Spacing）
采用 4pt 基准网格。

| Token | Value | 用途 |
|---|---|---|
| `--space-1` | 4px | 图标与文字贴合 |
| `--space-2` | 8px | 组件内元素间距 |
| `--space-3` | 12px | 卡片内 padding |
| `--space-4` | 16px | 卡片间距 / 页面 padding |
| `--space-5` | 24px | 模块分隔 |
| `--space-6` | 32px | 大模块之间 |
| `--space-8` | 48px | 页面顶部呼吸 |

---

## 四、圆角（Radius）

| Token | Value | 用途 |
|---|---|---|
| `--radius-xs` | 4px | Tag / Chip |
| `--radius-s` | 8px | 输入框 / 小按钮 |
| `--radius-m` | 12px | 常规按钮 |
| `--radius-l` | 16px | 卡片 |
| `--radius-xl` | 24px | 大卡片 / Sheet 顶部 |
| `--radius-full` | 999px | 胶囊按钮 / 头像 |

---

## 五、阴影 / Elevation（克制使用）

深色底下阴影效果弱，改用**边缘高光 + 背景色阶**表达层次。

| Token | 效果 |
|---|---|
| `--elev-1` | 卡片：background `#12172A` + 1px top highlight `rgba(255,255,255,0.04)` |
| `--elev-2` | 悬浮：background `#1B2138` + `box-shadow: 0 8px 24px rgba(0,0,0,0.4)` |
| `--elev-3` | 模态：background `#232A47` + `box-shadow: 0 16px 48px rgba(0,0,0,0.5)` |
| `--elev-glow` | 关键 CTA：`box-shadow: 0 0 32px var(--brand-glow)` — 仅用于"高光时刻" |

---

## 六、动效（Motion）

### 6.1 时长
| Token | Value | 用途 |
|---|---|---|
| `--duration-fast` | 150ms | 状态变化、Hover |
| `--duration-base` | 250ms | 页面过渡、卡片展开 |
| `--duration-slow` | 400ms | 数据滚动、进度条注入 |
| `--duration-celebration` | 800ms | 打卡成功、PK 胜利（唯一允许的长动效） |

### 6.2 曲线
| Token | Value | 用途 |
|---|---|---|
| `--ease-standard` | `cubic-bezier(0.2, 0.8, 0.2, 1)` | 默认过渡 |
| `--ease-spring` | `cubic-bezier(0.34, 1.56, 0.64, 1)` | 弹簧感（数字跳出） |
| `--ease-decel` | `cubic-bezier(0, 0, 0.2, 1)` | 进入 |
| `--ease-accel` | `cubic-bezier(0.4, 0, 1, 1)` | 退出 |

### 6.3 必做的动效模式
- **数字滚动**：体重、卡路里、天数 → `useCountUp` 400ms spring
- **进度条注入**：从 0 到目标值 400ms decel，不硬切
- **卡片进入**：从下方 8px + opacity 0→1，250ms decel（列表用 stagger 30ms）
- **CTA 按压**：scale 0.96 → 1，150ms spring
- **Haptic**：打卡成功 = `impact.medium`；错误 = `notification.warning`

---

## 七、图标（Icon）

- **线宽**：1.5px 统一（不混用 1px / 2px）
- **端点**：round cap
- **尺寸**：16 / 20 / 24 / 32
- **风格**：outline 为主，激活态转 filled（不做双色描边）
- **参考库**：Lucide Icons / Tabler / 自绘

---

## 八、组件状态清单（每个组件必须覆盖）

- Default / Hover / Pressed / Focused / Disabled / Loading / Error / Empty

