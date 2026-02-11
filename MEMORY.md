# 长期记忆

## 重要资源

- **ClawHub 技能仓库**: https://github.com/VoltAgent/awesome-openclaw-skills
  - 包含 2,999 个社区构建的 OpenClaw 技能
  - 按 28 个类别组织（AI & LLMs, Search & Research, DevOps, Coding 等）
  - 遇到未知任务时，优先在此搜索合适的技能

## 工作准则

- 遇到未知任务 → 先在 ClawHub 搜索相关技能
- 找到合适的技能 → 自动安装并使用
- 技能安装命令: `clawhub install <skill-slug>`
- 技能搜索命令: `clawhub search "关键词"`

## 技能管理

### 核心技能策略
- **已安装技能**：当前 8 个技能标记为核心（永不被清理）
- **新安装技能**：默认不加入核心列表（可被清理）
- **配置文件**: `~/.openclaw/core-skills.json`

### 定期清理规则
- **执行频率**: 每周日凌晨 3:00
- **清理对象**: 仅限未来新安装的技能（超过 10 天未使用）
- **核心技能**: 仅限配置文件中的技能受保护
- **日志位置**: `~/.openclaw/logs/skill-cleanup.log`
- **脚本位置**: `~/.openclaw/scripts/skill-cleanup.sh`

### 紧急清理（防止崩溃）
- **触发条件**: 技能总数 ≥ 50 个
- **清理规则**: 自动删除最旧的 10 个非核心技能
- **预防**: 保持技能库精简

### 管理核心技能
```bash
# 查看核心技能列表
cat ~/.openclaw/core-skills.json

# 添加核心技能（手动）
jq '.core_skills += ["新技能名"]' ~/.openclaw/core-skills.json > /tmp/temp.json && mv /tmp/temp.json ~/.openclaw/core-skills.json
```

## 航母位置追踪

### 核心方法
AIS 船舶追踪 + 卫星遥感 + 权威军事情报交叉验证

### 常用航母 MMSI
- USS Theodore Roosevelt (CVN-71): 369078000
- USS George H.W. Bush (CVN-77): 369985000
- USS Ronald Reagan (CVN-76): 369970000
- USS Nimitz (CVN-68): 369924000

### 查询平台
- **AIS**: MarineTraffic, VesselFinder, ShipFinder
- **军事情报**: USNI News (https://news.usni.org)
- **卫星遥感**: Sentinel-1 SAR, Sentinel-2 (https://scihub.copernicus.eu)

### 自动化脚本
- **脚本**: `~/.openclaw/scripts/carrier-tracker.sh`
- **报告**: `~/.openclaw/carrier-tracker/latest_report.md`
- **定时任务**: 每天 8:00 自动追踪

### 重要限制
- 军舰常关闭 AIS 信号
- 卫星有过顶周期（非实时）
- 军事行动中严格保密

---

## 📝 反思日志

### 记录规则
- 每日 20:00 自动记录反思
- 内容：今日工作复盘、改进点、新的认知

### 2026年

#### 02月

**2026-02-11**
- 任务调度优化：发现 quiet-hours 导致凌晨任务被跳过，调整执行时间
- 推送格式改进：应用户要求，从摘要改为原文+翻译对照
- 模型配置：添加 Kimi 2.5 API Key
- 长期任务简化：航母追踪改为每日 18:00 一次
- 新增任务：原油市场日报（每日 12:00）
