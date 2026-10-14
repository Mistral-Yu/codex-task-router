# codex-task-router

[English](../../README.md) · [日本語](../ja/README.md) · [简体中文](README.md)

一套用于集中接收 Codex 请求、将工作分配到合适项目和会话的规则。本仓库包含 `AGENTS.md` 委派规则，以及委派消息和结果报告的格式。

我曾误在另一个会话里开展工作，因此希望把请求集中到一个入口，再交给合适的会话处理。

入口会话直接回答简短的对话问题，将需要调查、分析、操作或制作成果的任务交给负责会话。请求原文、语言和资料会一并传递，结果以保存的报告链接提供。负责会话继续工作时，你仍可向入口提交下一个请求。

另提供[全局会话检查规则](../../session-scope-guard/README.md#简体中文)：请求看起来属于其他会话时先确认，并推荐中止。

## 开始使用

1. 选择所需语言，将该版本的 `AGENTS.md` 和 `doc/results.md` 复制到用于接收请求的项目根目录，保留 `doc/` 子目录。将该目录注册为名为 `codex-task-router` 的本地 Codex 项目并打开会话。
2. 发送目标项目或绝对路径、需要完成的工作、限制条件，以及相关文件或链接。可以自由表述，不必照搬下面的示例。
3. 入口优先选择合适的现有会话。需要新建时，会先说明目标项目、工作范围、模型和推理级别，并遵循 [AGENTS.md](AGENTS.md) 的审批规则。
4. 负责会话执行工作并保存简短报告。入口分别提供报告和负责会话的链接，随后继续接收新请求。

```text
项目：sample-app
请求：检查附件 CSV 中的缺失值和重复行。
限制：不更改原始数据，结果用中文。
资料1：待分析的原始 CSV。
```

## 操作要点

- 需要能使用 Codex 应用的 `list_threads`、`send_message_to_thread` 和文件操作工具。Codex 根据文档分配工作；本仓库不包含后台服务或可安装的技能包。
- 委派消息与结果使用你指定的语言，未指定时使用请求的语言。请求原文和附件会保留，并确认负责会话能访问和读取资料。
- 模型选择规则将最困难的任务和高精度电脑操作分配给 Astra，主要工作分配给 Sol，简单明确的任务分配给 Luna。同时核实负责会话的实际设置、工具和权限，不擅自更改现有设置。
- 委派消息和报告格式见 [doc/results.md](doc/results.md)。报告默认保存在 `local/reports/`，索引为 `local/reports/README.md`。目标会话和送达状态记录在 `local/routes.json`。
- 负责会话保存结果，不向入口发送完成消息。入口不会等待结果或自动收集报告；需要查看时，可让入口展示报告。仅明确要求时才进行独立复核。工具的权限审批在负责会话中操作。
- 希望在浏览器中查看报告时，可以请求 HTML 版本。无法打开时，入口会提供 Markdown 和成果链接，并注明显示效果尚未验证。

## 目录结构

```text
AGENTS.md                 英语委派规则
doc/results.md            英语委派与报告格式
README.md / LICENSE / .gitignore
session-scope-guard/       可选的全局规则（三种语言）
i18n/ja/                  日语版
  AGENTS.md
  doc/results.md
  README.md
i18n/zh-CN/               简体中文版
  AGENTS.md
  doc/results.md
  README.md
```

默认版本为英语。使用其他语言时，只需复制该版本的 `AGENTS.md` 和 `doc/results.md`，无需复制其他语言或 README。

## 参考配置

一种入口配置是通过 Codex 订阅使用 GPT-6 Luna（`gpt-6-luna`），推理级别为 `max`。模型需要单独设置，复制文档不会更改模型设置。负责会话的模型按任务选择。

## 许可证与本地文件

文档以 [MIT 许可证](../../LICENSE)提供。`.gitignore` 排除了附件、非公开报告与委派记录、备份、本地配置及验证脚本。关于 Codex 如何加载项目指令，参见 [AGENTS.md 官方指南](https://learn.chatgpt.com/docs/agent-configuration/agents-md)。

## 相关理念

[OpenAI dots](https://learn.chatgpt.com/docs/whats-new/dots-october-9-2026) 能判断是继续现有 Codex 会话还是新建会话，并发送追加指令，与本仓库的分配规则有部分相似之处。[Meta Muse](https://ai.meta.com/muse/) 也体现了通过对话接收请求、跨应用完成多步骤工作的更广泛理念。这些相似之处来自对公开行为的比较，不代表内部实现相同。本仓库专注于本地 Codex 会话之间的任务分配，尚未与这两个服务集成。

## 后续构想

参考 [Jev API 与可在本地运行的 Laya](https://unsloth.ai/docs/jp/moderu/decision-laya)，考虑通过决策模型选择“执行模型（本地／云端）→ 合适的现有会话或提议新建会话 → 委派”。结合任务难度、工具、权限和当前工作，保留现有审批规则。本地模型执行及这一分配流程仍处于构想阶段。

[OpenAI Decisions API](https://developers.openai.com/api/docs/guides/decisions) 也是潜在的集成方向。截至 2026 年 10 月 14 日，官方说明的 [ChatGPT 套餐使用流程](https://developers.openai.com/siwc/token-sharing-open-source/models-and-inference)采用 Responses API，尚未说明支持 Decisions API。本仓库尚未接入 Decisions API。
