# codex-task-router

[English](README.md) · [日本語](i18n/ja/README.md) · [简体中文](i18n/zh-CN/README.md)

A set of instructions for receiving requests in one Codex chat and routing work to the right project and chat. This repository contains an `AGENTS.md` routing policy and a format for handoffs and result reports.

I created it after accidentally working in the wrong session, to give requests a single starting point and keep project work in the right chat.

The intake chat answers brief conversational questions directly and delegates tasks that require investigation, analysis, actions, or deliverables. It passes along the original request, language, and references, and links to reports saved by the destination chat. You can send the next request while delegated work continues.

For a lighter alternative, the [global session scope guard](session-scope-guard/README.md) asks before acting on requests that appear to belong to another session, with stopping as the recommended choice.

## Getting started

1. Choose a language and copy its `AGENTS.md` and `doc/results.md` into the root of the project you will use for intake. Keep the `doc/` subfolder. Register that directory as a local Codex project named `codex-task-router` and open a chat there.
2. Send a request with the target project or absolute path, any constraints, and relevant files or links. You can use your own wording; the example below is optional.
3. The intake chat selects a suitable existing chat where possible. Before creating a new chat, it presents the project, scope, model, and reasoning effort and follows the approval rules in [AGENTS.md](AGENTS.md).
4. The destination chat performs the work and saves a short report. The intake gives you separate links to the report and that chat, then remains available for new requests.

```text
Project: sample-app
Request: Check the attached CSV for missing values and duplicate rows.
Constraints: Do not change the source data. Report in English.
Reference 1: The original CSV to analyze.
```

## Operating principles

- Requires access to the Codex app's `list_threads`, `send_message_to_thread`, and file tools. Codex follows the documents to route work; this repository does not include a background service or an installable skill.
- Handoffs and reports use your requested language, or the language of your request. Original requests and attachments are preserved, and references are checked for readability and access from the destination chat.
- The model-selection policy assigns the hardest tasks and high-precision computer operations to Astra, most work to Sol, and simple, clearly specified tasks to Luna. Selection also depends on the chat's actual settings, tools, and permissions; existing settings are not changed silently.
- [doc/results.md](doc/results.md) defines the handoff and report format. Reports are saved under `local/reports/` by default, with an index at `local/reports/README.md`. Destinations and delivery status are recorded in `local/routes.json`.
- Destination chats save results without sending completion messages back to the intake. The intake does not wait for results or collect them automatically; ask it to show a report when needed. Independent revalidation requires an explicit request. Approve native permission prompts in the destination chat.
- Request browser viewing if you want an HTML version of a report. If it cannot be opened, the intake provides Markdown and deliverable links and states that visual verification is incomplete.

## Files

```text
AGENTS.md                 English routing policy
doc/results.md            English handoff and report format
README.md / LICENSE / .gitignore
session-scope-guard/       Optional global instructions in three languages
i18n/ja/                  Japanese edition
  AGENTS.md
  doc/results.md
  README.md
i18n/zh-CN/               Simplified Chinese edition
  AGENTS.md
  doc/results.md
  README.md
```

English is the default. To use another language, copy that edition's `AGENTS.md` and `doc/results.md`; you do not need the other translations or README files.

## Reference setup

One intake configuration is GPT-6 Luna (`gpt-6-luna`) with reasoning effort `max` through a Codex subscription. Configure the model separately; copying the documents does not change model settings. Destination models are selected for each task.

## License and local files

The documents are available under the [MIT License](LICENSE). `.gitignore` excludes attachments, private reports and routing records, backups, local configuration, and validation scripts. For how Codex loads project instructions, see the [official AGENTS.md guide](https://learn.chatgpt.com/docs/agent-configuration/agents-md).

## Related ideas

There is some conceptual overlap with [OpenAI dots](https://learn.chatgpt.com/docs/whats-new/dots-october-9-2026), which can choose between existing and new Codex threads and send follow-up instructions. [Meta Muse](https://ai.meta.com/muse/) shares the broader idea of taking conversational requests and carrying out multistep work across apps. These are similarities in the documented behavior, not evidence of a shared implementation. This repository focuses on routing between local Codex chats and has no integration with either service.

## Future notes

A possible extension is decision-model routing inspired by [Jev API and locally hosted Laya](https://unsloth.ai/docs/jp/moderu/decision-laya): execution model (local or cloud) → suitable existing session or proposed new session → delegation, considering task difficulty, tools, permissions, and ongoing work within the current approval rules. Local-model execution and this routing flow remain ideas for exploration.

[OpenAI Decisions API](https://developers.openai.com/api/docs/guides/decisions) integration is another possibility. As of October 14, 2026, the documented [ChatGPT plan usage flow](https://developers.openai.com/siwc/token-sharing-open-source/models-and-inference) uses the Responses API and does not document Decisions API support. No Decisions API integration is implemented here.
