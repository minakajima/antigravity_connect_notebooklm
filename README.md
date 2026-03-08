# antigravity_connect_notebooklm
Google AntigravityからGoogle NotebookLMへ接続するテスト

## 実行したセットアップ手順

AntigravityとNotebookLMを連携させるために、以下のセットアップ作業を実行しました。

### 1. ツールのインストール
`uv` パッケージマネージャーを使用して、NotebookLMと通信するためのMCPサーバー（CLIツール）をインストールしました。

```powershell
uv tool install notebooklm-mcp-cli
```

### 2. Google アカウントへのログイン認証
以下のコマンドを実行し、ブラウザ上でGoogleアカウントによる認証セッションを確立しました。

```powershell
nlm login
```

### 3. MCPサーバーの設定追加
AntigravityからこのMCPサーバーを利用できるようにするため、設定ファイル（`C:\Users\(username)\.gemini\antigravity\mcp_config.json`）へ以下の構成を登録しました。

```json
{
  "mcpServers": {
    "notebooklm": {
      "command": "uvx",
      "args": [
        "notebooklm-mcp-cli",
        "mcp"
      ]
    }
  }
}
```

※ これらを反映させるため、ブラウザでの認証完了後に **Antigravity本体の再起動** が必要となります。


次のステップ（ユーザーにお願いしたい操作）
ブラウザでログインしてください: 現在Google Chromeのログイン画面が開いているはずです。そこから、NotebookLMを使用するGoogleアカウントでログインを完了させてください。
Antigravityの再起動（推奨）: 設定を反映させるために、ログインが完了したら一度このAntigravity（ウィンドウ）を閉じて再度立ち上げてください。
再起動後、ここ（チャット）で「私の現在のNotebook一覧を表示して」などと指示していただければ、NotebookLMと実際に連携して動作するか確認することができます！もし上手くいかない、ブラウザが開かなかった等の問題があれば教えてくださいね。
