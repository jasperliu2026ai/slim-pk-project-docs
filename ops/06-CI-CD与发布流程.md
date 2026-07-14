# 06 · CI/CD 与发布流程

> 版本：v1.0 | 2026-07-14

## 1. 流水线总览

```
代码提交（GitHub）
    │
    ▼
GitHub Actions 触发
    │
    ├── Lint + 单测（2 min）
    ├── 构建（npm build，< 3 min）
    └── 推送制品（打 Tag）
         │
         ├── dev 环境：feature/* 推送自动部署
         ├── staging：main 合并后手动触发
         └── prod：打 Tag（v*.*.*）+ 运维审批确认
```

## 2. GitHub Actions 工作流

### 2.1 CI（.github/workflows/ci.yml）

```yaml
name: CI
on:
  push:
    branches: ['**']
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm run test
      - run: npm run build
```

### 2.2 CD-生产（.github/workflows/deploy-prod.yml）

```yaml
name: Deploy to Production
on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: production   # GitHub Environment 审批保护
    steps:
      - uses: actions/checkout@v4

      - name: Setup SSH
        uses: webfactory/ssh-agent@v0.8.0
        with:
          ssh-private-key: ${{ secrets.PROD_SSH_KEY }}

      - name: Deploy CVM-01（50% 灰度）
        run: |
          ssh -o StrictHostKeyChecking=no ubuntu@${{ secrets.CVM01_IP }} \
            "bash /opt/slim-pk/scripts/deploy.sh ${{ github.ref_name }}"

      - name: Observe 5min（灰度观察）
        run: sleep 300

      - name: Deploy CVM-02（全量）
        run: |
          ssh ubuntu@${{ secrets.CVM02_IP }} \
            "bash /opt/slim-pk/scripts/deploy.sh ${{ github.ref_name }}"

      - name: Final Health Check
        run: curl -sf https://api.yourdomain.com/health
```

## 3. 发布策略

### 3.1 灰度节奏

```
Step 1: 部署 CVM-01（CLB 还有 CVM-02 兜底，50% 灰度）
        → 观察 5 分钟：错误率 < 0.1%，P99 < 500ms
Step 2: 无异常则部署 CVM-02（全量 100%）
        → 持续观察 30 分钟
Step 3: 任何阶段触发告警 → 立即回滚当前节点，不犹豫
```

### 3.2 发布禁止时间窗口

| 时间段 | 原因 |
|--------|------|
| 06:00 – 09:00 | 早晨打卡高峰 |
| 20:00 – 23:00 | 晚间打卡高峰 |
| PK 结算日 00:00 – 02:00 | 定时任务结算中 |
| 重大节假日、活动上线当天 | 流量突增期 |

**推荐发布窗口**：工作日 14:00 – 18:00 或凌晨 02:00 – 05:00

### 3.3 发布 Checklist

```
发布前（Pre-flight）：
□ 审批单已通过
□ 值班人员在线
□ 数据库已手动备份
□ 回滚脚本已准备并本地测试
□ 监控看板已打开
□ 已通知斯斯/睿睿

发布后（Post-check）：
□ /health 接口返回 200
□ 错误率 < 0.1%（观察 30 分钟）
□ 打卡接口 P99 延迟 < 500ms
□ MySQL 连接数正常
□ Redis 命中率 > 90%
□ 无新增告警
```

## 4. 回滚 SOP

### 触发条件（任意一条即启动）
- 错误率 > 1% 持续 2 分钟
- P99 延迟 > 2000ms 持续 3 分钟
- 健康检查连续失败
- 核心功能（打卡/支付）出现异常

### 回滚步骤（目标：3 分钟内完成）

```bash
# 两台 CVM 各执行
ssh ubuntu@CVM01_IP "bash /opt/slim-pk/scripts/rollback.sh"
ssh ubuntu@CVM02_IP "bash /opt/slim-pk/scripts/rollback.sh"

# 验证
curl -sf https://api.yourdomain.com/health

# 通知全员
# 示例：「已回滚到 vX.X.X，业务已恢复，正在排查原因」
```

## 5. 环境变量管理

| 变量 | 来源 | 禁止放在 |
|------|------|----------|
| DB_HOST / DB_PASS | 腾讯云 SSM | 代码库 / .env 入库 |
| REDIS_URL | 腾讯云 SSM | 代码库 |
| WX_APP_SECRET | 腾讯云 SSM | 代码库 |
| JWT_SECRET | 腾讯云 SSM | 代码库 |
| COS_SECRET_ID/KEY | 腾讯云 SSM + STS 临时密钥 | 代码库 |

> .env 文件由启动脚本从 SSM 动态生成，**不提交到 Git**，.gitignore 已排除。
