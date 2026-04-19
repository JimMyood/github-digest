# github-digest

自动化的 GitHub 项目摘要归档仓库。

## 内容

| 文件名模式 | 内容 | 生成频率 |
|---|---|---|
| `YYYY-MM-DD.md` | GitHub Trending 日榜 Top 50(详细版) | 每日 09:00 (Asia/Shanghai) |
| `YYYY-Www-recap.md` | 过去 7 天日榜精读综述 | 每周六 20:00 |
| `YYYY-Www-star-top50.md` | Star 总榜 Top 50 详细 | 每周日 10:00 |

## 工作流

```
Anthropic 远程 agent (schedule trigger)
  → 生成 markdown + git push 到本仓库
  → 本地 launchd 每小时 git pull
  → copy 到 Obsidian vault
```

- **生成端**:claude.ai 的 scheduled trigger,跑在 Anthropic 云
- **同步端**:本地 Mac 的 launchd agent (`~/Library/LaunchAgents/com.jim.github-digest-sync.plist`),执行 `~/github-digest-sync.sh`
- **消费端**:Obsidian vault `03-Resources/GitHub-Trending/`

## 字段规范(每条项目)

- **功能**:项目做什么(1 句)
- **适用场景**:谁在什么场景下会用(1 句)
- **同类/对比**:2-3 个对标项目或替代品
- **可借鉴**:给目标用户(中文创作者)的启发(1 句)

## 手动触发

```bash
# 本地同步(拉取 + 推到 vault)
bash ~/github-digest-sync.sh

# 远程 agent 跑一次(不等定时),在 https://claude.ai/code/scheduled 点按钮
```
