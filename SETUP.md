# Matri-X GitBook セットアップ手順

## 1. GitHubリポジトリ作成

1. https://github.com/new にアクセス
2. リポジトリ名: `matri-x-docs`
3. 説明: `Matri-X アルゴリズム解析プラットフォーム 公式ドキュメント`
4. 公開設定: **Public**（GitBook無料プランの制約）
5. Initialize this repository with: **何もチェックしない**
6. 「Create repository」をクリック

## 2. ローカルリポジトリをプッシュ

リポジトリ作成後に表示される手順を実行:

```bash
cd /home/node/.openclaw/workspace/matri-x-docs
git remote add origin https://github.com/yumaim/matri-x-docs.git
git branch -M main
git push -u origin main
```

## 3. GitBook連携

### 3-1. GitBookでSpace作成

1. https://app.gitbook.com/ にログイン
2. 「New Space」をクリック
3. 「Import from Git」を選択
4. GitHubを選択
5. `yumaim/matri-x-docs` を選択
6. Branch: `main`
7. 「Create Space」をクリック

### 3-2. 双方向同期設定

GitBookの設定で、以下を有効化:

- **GitBook → GitHub sync**: ON（GitBookでの編集をGitHubに反映）
- **GitHub → GitBook sync**: ON（GitHubでの更新をGitBookに反映）

## 4. カスタムドメイン設定

### 4-1. DNSレコード追加

ドメイン管理画面（お名前.com / Cloudflare等）で、以下のCNAMEレコードを追加:

```
タイプ: CNAME
名前: docs
値: hosting.gitbook.io
TTL: 3600（または自動）
```

### 4-2. GitBookでドメイン設定

1. GitBook Space → Settings → Domain
2. 「Add custom domain」をクリック
3. `docs.matri-x-algo.wiki` を入力
4. 「Add domain」をクリック
5. DNS検証が完了するまで待つ（最大24時間）

## 5. 完成！

以下のURLでアクセス可能になります:

- GitBook: `https://<your-space>.gitbook.io/`
- カスタムドメイン: `https://docs.matri-x-algo.wiki`

---

## 今後の更新方法

### GitBookで編集（推奨）

1. GitBook Space にログイン
2. 編集したいページを開く
3. 「Edit」をクリック
4. 編集後、「Save」をクリック
5. 自動的にGitHubにコミットされる

### GitHubで編集

1. https://github.com/yumaim/matri-x-docs でファイルを編集
2. コミット後、自動的にGitBookに反映される

### ローカルで編集（上級者向け）

```bash
cd /home/node/.openclaw/workspace/matri-x-docs
# ファイルを編集
git add .
git commit -m "Update documentation"
git push origin main
```

---

## トラブルシューティング

### Q. GitHubにプッシュできない

A. GitHub Personal Access Token が必要な場合があります:
1. https://github.com/settings/tokens で新しいトークンを作成
2. `git remote set-url origin https://<token>@github.com/yumaim/matri-x-docs.git`

### Q. カスタムドメインが反映されない

A. DNS伝播には最大24時間かかることがあります。`nslookup docs.matri-x-algo.wiki` で確認できます。

### Q. GitBook同期が動かない

A. GitBook Space → Settings → Integrations で GitHub連携を再認証してください。
