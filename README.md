# Monthly Nest

収入と支出を記録して、月の予算の残りをひと目で確認できる家計簿アプリです。
単一の `index.html` で動作する静的サイトです（ビルド不要）。

## ファイル構成

| ファイル | 役割 |
|---|---|
| `index.html` | アプリ本体 |
| `404.html` | 存在しないURLにアクセスしたときの表示 |
| `robots.txt` | 検索エンジン向けの設定 |
| `.nojekyll` | GitHub Pages の Jekyll 処理を無効化 |

## 公開手順（GitHub Pages）

1. GitHub で新しいリポジトリを作成（例: `monthly-nest`）
2. このフォルダの中身をすべてリポジトリ直下にアップロード（または `git push`）
3. リポジトリの **Settings → Pages** を開く
4. **Source** を `Deploy from a branch`、Branch を `main` / `/ (root)` にして **Save**
5. 数分後に `https://<ユーザー名>.github.io/<リポジトリ名>/` で公開されます

## 公開後に必ずやること（Firebase 認証）

ログイン機能に Firebase Authentication を使っています。公開URLでログインできるよう、次の設定をしてください。

1. Firebase コンソール → **Authentication → 設定 → 承認済みドメイン** に `<ユーザー名>.github.io` を追加
2. （推奨）Google Cloud コンソール → **APIとサービス → 認証情報** で該当のAPIキーに
   **HTTPリファラー制限** を設定（`https://<ユーザー名>.github.io/*` と、ローカル確認用に `http://localhost/*`）
3. 使うログイン方法（メール/パスワード、Google、匿名）が Authentication で有効になっているか確認

> Firebase のWeb用APIキーは秘密情報ではなくクライアントに含まれる前提の値ですが、
> 上記のリファラー制限を設定しておくと、他サイトからの不正利用を防げます。

## ローカルでの確認

`file://` で開くとログイン画面が出ず、認証なしで動作します。
認証込みで確認する場合は簡易サーバーを使ってください。

```bash
python3 -m http.server 8000
# http://localhost:8000/ を開く
```

## 外部依存

- Google Fonts（IBM Plex Mono / M PLUS Rounded 1c）
- html2canvas 1.4.1 / jsPDF 2.5.1（cdnjs・PDFレポート出力用）
- Firebase JS SDK 10.14.1（gstatic・認証用）
