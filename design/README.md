# 设计稿目录 — 轻减 PK 小程序

## 目录结构

```
design/
├── README.md                   # 本文件
├── design-system/
│   ├── DESIGN_TOKENS.md        # 设计 Token（色彩/字体/间距/圆角/阴影）
│   └── INFO_ARCHITECTURE.md    # 信息架构 & 页面结构
└── logo-assets/
    ├── qingjian-logo-v1.svg    # 轻减 Logo SVG 矢量稿（可缩放）
    ├── qingjian-logo-v1.png    # Logo PNG 导出稿
    └── fit-pk-logo-v0.svg      # 早期 Logo 草案（存档）
```

## 设计资产说明

### Design Tokens（`design-system/DESIGN_TOKENS.md`）
定义全局视觉变量，包含：
- **主色板**：品牌主色 #4CAF82（薄荷绿）、强调色 #FF6B35（活力橙）
- **字体规范**：HarmonyOS Sans 优先，系统字体回退链
- **字号/行高**：9 个层级（10px ~ 28px）
- **间距系统**：4px 基础栅格
- **圆角 & 阴影**：3 个层级

### 信息架构（`design-system/INFO_ARCHITECTURE.md`）
- 完整页面树（主包 + 两个分包）
- 导航结构 & Tab 设计
- 核心交互流程（创建PK / 加入PK / 每日打卡 / 结算 & 海报分享）

### Logo 资产（`logo-assets/`）
- SVG 矢量稿可直接用于小程序 Icon 导出（建议 81×81px）
- PNG 为 1024×1024 高清导出，适配各平台上传要求

## 交互原型

> ⚠️ Figma 完整交互稿待 AppID 确认后正式输出，当前提供文档描述版。

关键交互流程见 `design-system/INFO_ARCHITECTURE.md` 中「交互流程」章节。

## 版本历史

| 版本 | 日期 | 说明 |
|------|------|------|
| v0.1 | 2026-07-14 | 首版 Design Token + 信息架构 + Logo |

## 待输出

- [ ] Figma 完整交互稿（等 AppID 确认，预计 D+3）
- [ ] 各页面高保真效果图
- [ ] 组件库 Storybook
- [ ] 切图规范导出说明
