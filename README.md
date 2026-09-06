# Togello Agent Plugin

![Togello logo](assets/togello-icon-512.png)

Togelloの公開MCPへ接続し、個人のTODO・予定参照・日別メモ・活動記録をAIから扱うためのPluginである。

[Agent Plugins 1.0.0](https://agent-plugins.org/)の共通形式を使用する。独自のSkillや実行スクリプトは含まない。

## 現在の状態

初期実装であり、Marketplaceには未申請である。クライアントでのインストールからOAuth認可、各操作までの一連の動作は未検証である。既存のTogello Appでの動作と、このPluginの互換性確認は別である。

## 接続先と認証

- MCP: `https://mcp.togello.com/mcp`
- Transport: Streamable HTTP
- OAuth issuer: `https://togello.api.toru-takagi.dev`
- 利用にはTogelloアカウントが必要である。
- Google Calendarの予定参照には、Togello側でのGoogle Calendar連携が必要である。

認証はクライアントが管理する。Agent Plugins 1.0.0には共通のOAuth設定フィールドがないため、このPluginには接続先のみを記載する。クライアントが提示するTogelloの認可画面で権限を確認して接続する。認可画面が出ない場合は、クライアントのリモートMCP・OAuth対応を確認する。

トークン、クライアントシークレット、個人のタスクやメモを、このリポジトリのファイルに保存しない。

## Cursorでのローカル検証手順

以下は[Cursor公式ドキュメント](https://cursor.com/docs/plugins)に基づく検証手順であり、このPluginでの検証完了を示すものではない。

1. このリポジトリをローカルに取得する。
2. `~/.cursor/plugins/local/togello/`に、`plugin.json`と`mcp.json`が直下になるよう配置する。
3. Cursorを再起動するか、`Developer: Reload Window`を実行する。
4. CustomizeでTogelloが認識されていることを確認する。
5. Togello MCPへ接続し、クライアントの案内に従ってOAuth認可する。
6. まず「Togelloで日本の現在日時を確認して」で接続を確認する。

組織設定でローカルPluginの読み込みが禁止されている場合は、その設定に従う。他のクライアントでは、Agent Plugins、Streamable HTTP、OAuthへの対応と導入手順を個別に確認する。

## できること

| 領域 | 操作 |
| --- | --- |
| TODO | 一覧取得、作成、更新、完了などの状態変更 |
| カテゴリ | 一覧取得 |
| 予定 | 連携Google Calendarの予定と、予定日時を持つTODOの参照 |
| 日別メモ | 指定日の取得、更新、クリア |
| 活動記録 | 活動項目・ログの取得、開始、完了 |
| 時刻 | 日本の現在日時の取得 |

Gatherの作成、複数人の日程調整、Google Calendarへの予定作成は提供しない。カレンダー取得ツールには任意期間を指定する入力がない。

## 依頼例

以下は公開MCPの機能に基づく依頼例であり、このPluginでの実行検証は未完了である。

- 「Togelloの未完了タスクを一覧にして」
- 「Togelloの予定と未完了タスクを確認し、今日の作業順を提案して。データは変更しないで」
- 「Togelloに『リリース手順を確認する』というTODOを作って」
- 「Togelloの2026-09-06のカレンダーメモを表示して」
- 「Togelloの活動項目と、現在進行中の活動ログを確認して」

TODOの作成・更新、日別メモの更新、活動ログの開始・完了は、Togello内のデータを変更する。日別メモの更新は本文の置換であり、空の内容を指定するとクリアされる。活動ログを開始するには既存の活動項目が必要である。

## データとサポート

Pluginは既存のリモートMCPに接続する設定を配布する。実際に利用可能なツールや入力項目は、接続先とクライアントから取得される定義に従う。

- [Togello](https://togello.com)
- [プライバシーポリシー](https://togello.com/privacy-policy.html)
- [MCPサーバーのソース](https://github.com/Toru-Takagi/togello-mcp-server)
- サポート: support@togello.com

このPluginの設定と文書は[ISC License](LICENSE)で提供する。`assets/togello-icon-512.png`はISC Licenseの対象外である。Togelloサービス本体のコードやTogelloの名称・ロゴの権利を許諾するものではない。
