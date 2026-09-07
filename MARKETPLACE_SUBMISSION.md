# Cursor Marketplace申請資料

準備日: 2026-09-07。申請・公開は未実施である。この文書は申請入力用の原稿であり、実際のフォーム項目名・必須項目はログイン後に確認する。

## 申請情報

| 項目 | 内容 |
| --- | --- |
| 表示名 | Togello |
| Plugin識別名 | `togello` |
| バージョン | `0.1.0` |
| 公開者 | Toru-Takagi |
| Repository | https://github.com/Toru-Takagi/togello-agent-plugin |
| 形式 | Agent Plugins 1.0.0（ルートの`plugin.json`と`mcp.json`） |
| Webサイト | https://togello.com |
| サポート | support@togello.com |
| プライバシーポリシー | https://togello.com/privacy-policy.html |
| ライセンス | ISC（設定・文書。名称・ロゴは対象外） |
| ロゴ | `assets/togello-icon-512.png`（公式favicon由来の512×512 PNG） |
| キーワード | togello, tasks, calendar, activity, mcp |

Agent Plugins 1.0.0のルートmanifestにはlogoフィールドがないため、独自フィールドは追加しない。申請画面にロゴ指定欄があれば上記ファイルを使用する。Marketplaceでの名前の利用可否とロゴ表示は審査・掲載時に確認する。

## 説明文案

### 短い説明（英語）

Manage personal tasks, calendar memos, and activity logs with Togello.

### 詳細説明（英語）

Connect Cursor to Togello through its hosted MCP server. Review personal tasks and connected calendar information, create and update TODOs, manage daily calendar memos, and start or complete activity logs from your AI assistant.

A Togello account and OAuth authorization are required. Viewing Google Calendar events requires linking Google Calendar in Togello first. This plugin provides connection configuration for the existing Togello MCP service; it does not install a local server or include executable scripts.

Task updates, memo updates, and activity logging change data in Togello. Calendar memo updates replace the existing text. The plugin does not create Google Calendar events or provide multi-person scheduling.

### 日本語説明

Togelloの公開MCPへ接続し、個人のTODO、連携カレンダーの予定参照、日別メモ、活動記録をCursorから扱うPluginである。TogelloアカウントとOAuth認可が必要であり、Google Calendarの予定参照にはTogello側での連携が必要である。

## 審査用の確認手順

1. READMEの手順でPluginを導入する。
2. CustomizeでTogelloを開き、Plugin由来のMCPをAuthenticateする。
3. 新しく開いた認可画面でログインして権限を確認し、認可後にCursorへ戻る。
4. Configure togelloでLocalがConnected、12ツールが認識されていることを確認する。
5. Agentモードの新規チャットで次の指示を入力する。

> Togello Pluginのget-japan-current-timeだけを1回呼び出し、結果を表示してください。その他のデータの取得・変更はしないでください。

期待結果は`timeZone: Asia/Tokyo`と実行時の`currentTime`である。固定日時を期待値にしない。既存の直接登録MCPがある場合は、Plugin由来の接続と区別する。

## 検証結果と範囲

- 2026-09-07、macOSのCursorでローカルPluginのOAuth認可を完了した。
- Cursorログで認証コールバック交換完了とStreamable HTTP接続成功を確認した。
- UIでConnectedと12ツールの認識を確認した。
- 検証チャットで日本時刻`2026/9/7 21:24:45`（Asia/Tokyo）が返った。同時刻のCursorログでもget-japan-current-time呼び出しを確認した。
- 同日のOpenAI側Togello Appでも日本時刻の取得に成功した。既存接続での確認であり、OpenAIでの新規認可・トークン更新の実機検証を意味しない。

未検証: Marketplace経由の導入、全ツールの個別実行、データ更新操作、トークン期限切れ後の自動更新、Cursor以外でのこのPlugin形式の導入。

観測事項: Cursorの任意のresources取得では`Method not found`が記録されたが、ツール一覧取得と時刻取得は成功した。ログイン後のローカルcallbackに接続できない場合は、認証待受の期限切れを確認し、新しい認証を開始する。今回の再試行では認証完了を確認できた。

## 申請前の残作業

- 本README・申請資料の公開内容を確認し、承認後に対象ファイルだけを公開Repositoryへ反映する。
- [申請画面](https://cursor.com/marketplace/publish)の必須項目、ロゴ表示、公開者情報、規約を本人が確認し、送信を承認する。
- 申請後の審査結果を確認し、掲載された場合はMarketplace経由の導入を追加検証する。

この資料には個人のタスク・メモ・予定、認証コード、トークン、クライアントシークレットを含めない。

## 公式資料

- [Cursor Plugins](https://cursor.com/docs/plugins)
- [Cursor Plugins Reference・申請チェックリスト](https://cursor.com/docs/reference/plugins)
- [Agent Plugins manifest schema](https://agent-plugins.org/schemas/1.0.0/plugin.schema.json)
