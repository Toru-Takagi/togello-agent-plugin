# Anthropic Community Marketplace申請資料

このリポジトリは、Cursor向けのAgent Plugins形式とClaude Code向けのPlugin形式を同じルートで提供する。既存の`plugin.json`と`mcp.json`はCursor向けに維持し、Claude Code向けには`.claude-plugin/plugin.json`と`.mcp.json`を使用する。

## 申請先

Anthropicが管理する公式Marketplaceではなく、第三者Plugin向けのCommunity Marketplaceを対象とする。

- 申請フォーム: https://platform.claude.com/plugins/submit
- Community Marketplace: https://github.com/anthropics/claude-plugins-community

## 申請前の検証

リポジトリの親ディレクトリをカレントディレクトリにして以下を実行する。

```bash
claude plugin validate ./togello-agent-plugin
claude plugin validate ./togello-agent-plugin --strict
claude --plugin-dir ./togello-agent-plugin
```

Claude Codeのセッション内では、`/mcp`でPlugin由来のスコープ名`plugin:togello:togello`を確認し、必要に応じてOAuth認証を完了する。Pluginリポジトリのルートをカレントディレクトリにすると、ルートの`.mcp.json`がプロジェクトMCPとしても読み込まれる可能性があるため、親ディレクトリから起動する。

## 公開後の導入確認

Community Marketplaceへの反映後、以下でMarketplace経由の導入を確認する。

```bash
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install togello@claude-community
```

審査承認とMarketplaceへの反映は別であり、承認直後にカタログへ表示されない場合がある。
