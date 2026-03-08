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
        "--from",
        "notebooklm-mcp-cli",
        "notebooklm-mcp"
      ]
    }
  }
}
```

### 4. エキスパートガイド（スキル）のインストール

Antigravity上でNotebookLMツールをより効果的に使用させるためのエキスパートガイド（スキル）をインストールします。Windows環境などで `cp932` エンコーディングエラーが発生する場合は以下のコマンドを実行してください。

```powershell
$env:PYTHONUTF8="1"; nlm skill install antigravity
```

※ 後からスキルを最新の状態に更新したい場合は `nlm skill update` を実行します。
※ インストール後に正しく設定されているか確認したい場合は `nlm doctor` コマンドが利用できます。

※ これらを反映させるため、ブラウザでの認証やスキルのインストール完了後に **Antigravity本体の再起動** が必要となります。


## 次のステップ（ユーザーにお願いしたい操作）

1. **ブラウザでログインしてください**: ターミナルで `nlm login` を実行するとGoogle Chromeなどのブラウザが開きます。NotebookLMを使用するGoogleアカウントでログインを完了させてください。
2. **スキルをインストールしてください**: 認証完了後、ターミナルで `$env:PYTHONUTF8="1"; nlm skill install antigravity` を実行してください。
3. **Antigravityの再起動**: 設定を反映させるため、ログインとインストールが完了したら一度このAntigravity（ウィンドウ）を閉じて再度立ち上げてください。
4. **動作確認**: 再起動後、ここ（チャット）で「私の現在のNotebook一覧を表示して」などと指示していただければ、NotebookLMと実際に連携して動作するか確認することができます！もし上手くいかない等の問題があれば教えてくださいね。
