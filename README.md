# Open Source Scout

An agent skill for researching open-source solutions before development, validating candidates, and comparing reuse with building from scratch.

开发前先调研现成方案：明确需求，寻找成熟依赖、SDK、模板或完整项目，验证重点候选，再交付推荐和改造计划。

## 安装

安装环境：Node.js 22.20.0 或更高版本（Skills CLI 1.7.2 的要求）。

通过 [Skills CLI](https://github.com/vercel-labs/skills) 安装到当前项目：

```bash
npx skills add original4422/open-source-scout --skill open-source-scout
```

指定安装到 Codex 和 Claude Code：

```bash
npx skills add original4422/open-source-scout --skill open-source-scout -a codex claude-code -y
```

需要在多个项目中使用时，添加 `-g`：

```bash
npx skills add original4422/open-source-scout --skill open-source-scout -a codex claude-code -g -y
```

查看仓库中可安装的技能：

```bash
npx skills add original4422/open-source-scout --list
```

## 使用

在支持技能的助手中描述需求，例如：

> 使用 open-source-scout。我想做一个离线运行的文档检索工具，支持 PDF 和 Markdown。先调研现成方案，比较复用与自行实现的成本，验证重点候选，给出推荐和改造计划。

已有项目也可以手动调用：

> 使用 open-source-scout，检查当前项目的技术栈，为新增的文件解析功能寻找成熟依赖，说明接入成本和仍需开发的部分。

Codex 可显式调用 `$open-source-scout`；其他工具使用各自的技能调用方式。支持自动选择技能的宿主会根据描述匹配新项目请求，实际触发由宿主决定。

## 工作流程

1. 读取需求、项目约定和已有技术栈，只追问影响选型的关键问题。
2. 以 GitHub 为主搜索，结合官方 SDK、库、插件与模板，通常深入比较约 3 个候选。
3. 优先判断需求匹配度、接入与改造成本、可维护性和许可证条件，Star 与更新时间作为辅助信号。
4. 对最有希望的 1–2 个候选做最小验证，分别记录文档声明、源码检查和实际运行结果。
5. 与自行实现相同核心需求的成本比较，推荐依赖、整仓改造、组合方案、局部复用或自行实现。
6. 保存 Markdown 报告及改造计划，供后续开发使用。

常规验证在独立临时目录和项目局部环境中执行。需要改变系统配置、使用账号或付费资源、明显增加耗时时，先说明具体操作和成本。完成选型报告后，由用户决定是否继续开发。

## 交付内容

- 推荐结论与主要取舍。
- 需求对应表：直接支持、需要改造、缺失或未确认。
- 候选比较与淘汰原因。
- 与自行实现的成本比较及估计依据。
- 来源、检查日期、版本、验证命令、结果与未验证项。
- 复用范围、改造顺序、完成标准和工作量估计。

已有项目按仓库约定保存报告；没有约定时使用 `docs/research/open-source-scout-<主题>.md`。新项目尚无目录时使用 `open-source-research/<主题>/report.md`。

## 文件

```text
skills/open-source-scout/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── report-template.md
    └── tool-adapters.md
```

- [核心指令](skills/open-source-scout/SKILL.md)
- [报告模板](skills/open-source-scout/references/report-template.md)
- [工具适配](skills/open-source-scout/references/tool-adapters.md)

核心流程独立可用，使用宿主已有的联网、文件读取和命令执行能力。技能目录可以整体迁移到其他支持 `SKILL.md` 的工具。

## 许可证

[MIT](LICENSE) · Copyright (c) 2026 original4422
