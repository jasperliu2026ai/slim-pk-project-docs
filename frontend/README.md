# 减肥 PK 小程序 — 前端开发文档

> 作者：睿睿【前端】  
> 版本：v1.0 | 日期：2026-07-14  
> 项目：减肥 PK 小程序（L1 自用版，Deadline：2026-08-01）

---

## 文档目录

| 文件 | 内容 |
|------|------|
| [README.md](./README.md) | 本文件，文档索引 |
| [01-技术选型与架构.md](./01-技术选型与架构.md) | 技术栈选型、分包架构、目录结构 |
| [02-页面与路由设计.md](./02-页面与路由设计.md) | 完整页面清单、路由规则、TabBar 设计 |
| [03-核心组件设计.md](./03-核心组件设计.md) | 关键业务组件的实现方案与接口设计 |
| [04-接口约定.md](./04-接口约定.md) | 前后端接口清单、数据结构、错误码 |
| [05-状态管理.md](./05-状态管理.md) | MobX store 设计，跨页面数据流 |
| [06-微信能力对接.md](./06-微信能力对接.md) | 微信登录、分享、订阅消息、云存储对接 |
| [07-性能与工程规范.md](./07-性能与工程规范.md) | setData 优化、分包策略、编码规范 |
| [08-开发排期.md](./08-开发排期.md) | 18 天倒排排期、前端任务清单 |
| [09-风险与预案.md](./09-风险与预案.md) | 技术风险清单、预案、待拍板事项 |
| [10-合规与安全.md](./10-合规与安全.md) | 健康数据合规、隐私授权、安全红线 |

---

## 快速开始

### 环境要求

- 微信开发者工具 ≥ 1.06.2307（Stable）
- Node.js ≥ 18.x
- TypeScript ≥ 5.x

### 项目初始化

```bash
# 克隆前端仓库
git clone https://github.com/jasperliu2026ai/slim-pk-miniapp.git
cd slim-pk-miniapp

# 安装依赖
npm install

# 构建 npm 包（Vant Weapp 等）
# 在微信开发者工具菜单：工具 → 构建 npm
```

### 开发阶段注意事项

1. **AppID**：必须使用真实注册的微信小程序 AppID（COS 上传、分享等能力都依赖）
2. **不校验合法域名**：开发阶段在开发者工具「详情 → 本地设置」勾选「不校验合法域名」和「不校验 HTTPS」，联调地址使用后端 CVM 内网 IP
3. **图片上传**：前端通过 `wx.uploadFile` 将水印图推后端接口，后端负责存 COS，前端不接 COS SDK

---

## 技术栈一览

| 分类 | 选型 | 备注 |
|------|------|------|
| 框架 | 微信小程序原生（WXML / WXSS / TypeScript） | 零跨端冗余 |
| 组件库 | Vant Weapp | 按需引入，CSS 变量主题定制 |
| 状态管理 | MobX-miniprogram | 跨页共享排行榜/打卡状态 |
| 图表 | ECharts for 小程序 | 体重趋势折线图 |
| 动效 | lottie-miniprogram | 打卡成功/PK 胜利动效 |
| 图片存储 | 腾讯云 COS（后端中转） | 前端 wx.uploadFile 到后端接口 |
| 代码规范 | ESLint + Prettier + stylelint | Conventional Commits |

---

## 关联仓库 & 文档

- 前端代码：https://github.com/jasperliu2026ai/slim-pk-miniapp
- 项目文档：https://github.com/jasperliu2026ai/slim-pk-project-docs
