# Komari

![komari](https://socialify.git.ci/kadidalax/komari-classic/image?description=1&font=Inter&forks=1&issues=1&language=1&logo=https%3A%2F%2Fraw.githubusercontent.com%2Fkomari-monitor%2Fkomari-web%2Fd54ce1288df41ead08aa19f8700186e68028a889%2Fpublic%2Ffavicon.png&name=1&owner=1&pattern=Plus&pulls=1&stargazers=1&theme=Auto)

Komariは、サーバーのパフォーマンスを監視するためのシンプルで効率的なソリューションを提供することを目的とした、軽量の自己ホスト型サーバー監視ツールです。Webインターフェースを介してサーバーのステータスを表示し、軽量エージェントを介してデータを収集します。

> [!WARNING]
> Komariは、自己ホスト型の監視/制御プログラムであり、所有しているシステム、または管理権限を得ているシステムでのみ使用してください。Komariを武器化したり、許可なく展開、アクセス、永続化、コマンド実行、その他の不正利用に使用したりしないでください。実際の悪用リスクについては、Huntressの分析をご参照ください：[Komari C2 agent abuse](https://www.huntress.com/blog/komari-c2-agent-abuse)。
> Komariの展開および運用方法については、利用者自身が責任を負います。開発者は、無許可または不正な利用、およびその結果について責任を負いません。
> Windows端末でリモートコントロールを有効にした場合、クライアントはユーザーがログインするたびに、KomariがリモートコントロールソフトウェアであることをWindows通知で知らせます。

[ドキュメント](https://komari-document.pages.dev/)

## 特徴

- **軽量で効率的**: リソース消費が少なく、あらゆる規模のサーバーに適しています。
- **自己ホスト型**: データプライバシーを完全に制御でき、展開も簡単です。
- **Webインターフェース**: 直感的な監視ダッシュボードで、使いやすいです。

## クイックスタート

### 1. ワンクリックインストールスクリプトを使用する

systemdを使用するディストリビューション（Ubuntu、Debianなど）に適しています。

```bash
curl -fsSL https://raw.githubusercontent.com/kadidalax/komari-classic/main/install-komari.sh -o install-komari.sh
chmod +x install-komari.sh
sudo ./install-komari.sh
```

### 2. Docker展開

1. データディレクトリを作成します:
   ```bash
   mkdir -p ./data
   ```
2. Dockerコンテナを実行します:
   ```bash
   docker run -d \
     -p 25774:25774 \
     -v $(pwd)/data:/app/data \
     --name komari \
     ghcr.io/kadidalax/komari-classic:latest
   ```
3. デフォルトのユーザー名とパスワードを表示します:
   ```bash
   docker logs komari
   ```
4. ブラウザで `http://<your_server_ip>:25774` にアクセスします。

> [!NOTE]
> 環境変数 `ADMIN_USERNAME` と `ADMIN_PASSWORD` を使用して、初期のユーザー名とパスワードをカスタマイズすることもできます。

### 3. バイナリファイル展開

1. Komariの[GitHubリリース](https://github.com/kadidalax/komari-classic/releases)ページにアクセスして、お使いのオペレーティングシステム用の最新のバイナリをダウンロードします。
2. Komariを実行します:
   ```bash
   ./komari server -l 0.0.0.0:25774
   ```
3. ブラウザで `http://<your_server_ip>:25774` にアクセスします。デフォルトのポートは `25774` です。
4. デフォルトのユーザー名とパスワードは、起動ログで確認するか、環境変数 `ADMIN_USERNAME` と `ADMIN_PASSWORD` を介して設定できます。

> [!NOTE]
> バイナリに実行権限があることを確認してください（`chmod +x komari`）。データは実行ディレクトリの `data` フォルダに保存されます。

### 手動ビルド

#### 依存関係

- Go 1.18+ および Node.js 20+（手動ビルド用）

1. フロントエンドの静的ファイルをビルドします:
   ```bash
   git clone https://github.com/kadidalax/komari-web-1.2.5-fix2
   cd komari-web
   npm install
   npm run build
   ```
2. バックエンドをビルドします:
   ```bash
   git clone https://github.com/kadidalax/komari-classic
   cd komari
   ```
   ステップ1で生成された静的ファイルを `komari` プロジェクトのルートにある `/web/public/defaultTheme/dist` フォルダにコピーし、`komari-theme.json` と `preview.png`/`perview.png` を `/web/public/defaultTheme` にコピーします。
   ```bash
   go build -o komari
   ```
3. 実行:
   ```bash
   ./komari server -l 0.0.0.0:25774
   ```
   デフォルトのリスニングポートは `25774` です。`http://localhost:25774` にアクセスします。

## フロントエンド開発ガイド

[Komariテーマ開発ガイド | Komari](https://komari-document.pages.dev/dev/theme.html)

[CrowdinでKomariを翻訳する](https://crowdin.com/project/komari/invite?h=cd051bf172c9a9f7f1360e87ffb521692507706)

## クライアントエージェント開発ガイド

[Komariエージェント情報レポートおよびイベント処理ドキュメント](https://komari-document.pages.dev/dev/agent.html)

## 貢献

IssueやPull Requestを歓迎します！

## 謝辞

### オープンソースコミュニティ

PR を送ってくれた方、テーマを作成してくれた全ての開発者

—— そして：こんなに暇でいられる自分に感謝

## Star履歴

[![Star History Chart](https://api.star-history.com/svg?repos=kadidalax/komari-classic&type=Date)](https://www.star-history.com/#kadidalax/komari-classic&Date)
