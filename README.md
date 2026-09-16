# Dev Flow

一个 兼容 Agent 规范的 CLI skill：开发任务的规模路由器。用户报 bug 或提优化需求时，先判断任务规模，再路由到对应的流水线。

## 流水线

**小型 Bug / 小功能优化** —— 全自动闭环，一路到底：

```
Issue → Branch/Worktree → Code → Test → Merge → Release
```

**大型 Bug** —— 自动分析，两个人工门禁，门禁通过前不改生产代码：

```
Issue → Reproduce → Impact Analysis → Root Cause → Fix Plan → [人工确认①]
      → Branch/Worktree → Code → Test/Regression → Review → [人工确认②]
      → Canary Release → Monitor → Release
```

分类原则：小型需同时满足根因明显、低风险、不涉安全并发、测试好覆盖；大型命中任意一条即触发（根因不明、核心逻辑/数据/资金、安全/并发/迁移、跨服务、线上事故）。不确定时默认按大型处理。

## 安装

复制到用户级技能目录（所有项目生效）：

```bash
mkdir -p ~/.agents/skills
cp -r dev-flow ~/.agents/skills/
```

或安装到单个项目：把 `dev-flow/` 放到该仓库的 `.agents/skills/` 下。

## 结构

```
dev-flow/
└── SKILL.md    # skill 本体
```
