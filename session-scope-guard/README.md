# Session scope guard

A small alternative to the task router: ask before acting when a request appears to belong to another session. It recommends stopping that request and does not route work automatically.

## English

Merge [AGENTS.md](AGENTS.md) into your global `~/.codex/AGENTS.md`, keeping existing instructions. If you use `AGENTS.override.md`, merge it there instead. Use one language edition. This fragment is intended for ordinary project sessions; it does not replace the task router's delegation policy.

To enable the built-in question UI in Default mode, add this key under `[features]` in `~/.codex/config.toml`. If that table already exists, add only the key:

```toml
[features]
default_mode_request_user_input = true
```

The flag is under development; check your build with `codex features list` and open a new session after changing the setting. Enabling it does not guarantee question UI access; follow the active mode, client, and tool rules. Copying this folder does not change global files. See the official [configuration guide](https://learn.chatgpt.com/docs/config-file/config-basic) and [AGENTS.md guide](https://learn.chatgpt.com/docs/agent-configuration/agents-md).

## 日本語

依頼が別セッション向けに見える場合、作業前に質問して「中断」を推奨する短い別案です。[日本語の追記文](AGENTS.ja.md) をグローバルの `~/.codex/AGENTS.md` に追記し、既存の指示は残してください。`AGENTS.override.md` を使っている場合は、そちらに追記します。通常のプロジェクトセッション向けで、受付ルーターの委託方針を置き換えるものではありません。

通常モードで質問UIを使うには、`~/.codex/config.toml` の `[features]` に上の設定を加え、新しいセッションを開きます。既存の `[features]` は重複させず、キーだけ追加してください。この機能は開発中なので `codex features list` で対応を確認します。有効化だけで質問UIが使えるとは限らず、実際のモード・クライアント・ツールの制約に従います。フォルダーのコピーだけではグローバル設定は変わりません。

## 简体中文

这是一个简短的替代方案：请求看起来属于其他会话时，先提问并推荐中止。将[中文追加规则](AGENTS.zh-CN.md) 合并到全局 `~/.codex/AGENTS.md`，保留已有指令。如果使用 `AGENTS.override.md`，则合并到该文件。它适用于普通项目会话，不替代入口 Router 的委派规则。

要在默认模式下使用提问界面，将上面的设置加入 `~/.codex/config.toml` 的 `[features]`，再打开新会话。已有该表时只添加键，不要重复建表。此功能仍在开发中，请用 `codex features list` 检查当前版本是否支持。启用该选项不保证提问界面可用，仍须遵守实际模式、客户端和工具的限制。复制文件夹不会修改全局设置。
