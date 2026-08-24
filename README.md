# cats apk project — サイト

`https://catscatsnekoneko.github.io/` として GitHub Pages で公開している静的サイト。

Androidアプリ「マイ電話番号」の紹介と、**プライバシーポリシー**を置いている。
ポリシーのURLは Play Console とアプリ本体（`AppNavHost.kt` の `PRIVACY_POLICY_URL`）から
参照されているため、**ページのファイル名を変えるときは両方を直すこと。**

## 構成

| ファイル | 内容 |
|---|---|
| `index.html` | トップ |
| `myphonenumber.html` | アプリ「マイ電話番号」の紹介 |
| `privacy/index.html` | プライバシーポリシーの索引 |
| `privacy/myphonenumber.html` | **マイ電話番号のポリシー**（日本語） |
| `privacy/myphonenumber.en.html` | 同（English） |
| `privacy-policy.html` / `.en.html` | 旧URLからのリダイレクト。消さないこと |
| `assets/style.css` | 全ページ共通のスタイル |
| `assets/*.png` | アイコンとスクリーンショット |

### プライバシーポリシーは必ずアプリごとに分ける

**1枚にまとめないこと。** アプリによって広告やデータ収集の有無が違うため、
1枚に詰め込むとどの記述がどのアプリのものか曖昧になる。
Play Console に登録するURLも、そのアプリ専用のページを指す。

新しいアプリを配信するときは、

1. `privacy/<アプリ名>.html` を作る（既存のものをコピーして中身を実態に合わせる）
2. `privacy/index.html` のリストに1行足す
3. そのアプリの Play Console にそのURLを登録する

**既存のポリシーのURLは変えない。** 公開後に変えると、リリース済みのアプリと
Play Console の登録が食い違う。

ビルドは不要。ファイルをそのまま配信している（`.nojekyll` で Jekyll の処理を止めている）。

## 書くときの注意

- **日本語の文は1行に収める。** ソースの改行は半角スペースとして描画されるので、
  文の途中で改行すると「情報の 取り扱い」のように余計な空きが出る。英文は改行してよい
- 配色は `assets/style.css` の CSS 変数にまとめてある。アプリアイコンの緑
  （`#63B54D` → `#1C6B33`）に合わせている。ダークテーマは `prefers-color-scheme` で切り替わる
- スクリーンショットに**実在する電話番号を写さない**こと。
  アプリ側リポジトリの `docs/store-assets/README.md` に撮り方をまとめてある

## 手元での確認

```bash
python3 -m http.server 8765
# http://127.0.0.1:8765/ を開く
```
