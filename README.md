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
| `codebook.html` | アプリ「二次元コード帳」の紹介 |
| `steplengthpro.html` | アプリ「歩幅計Pro」の紹介 |
| `privacy/index.html` | プライバシーポリシーの索引 |
| `privacy/myphonenumber.html` | **マイ電話番号のポリシー**（日本語） |
| `privacy/myphonenumber.en.html` | 同（English） |
| `privacy/codebook.html` / `.en.html` | **二次元コード帳のポリシー**（広告あり） |
| `privacy/steplengthpro.html` / `.en.html` | **歩幅計Proのポリシー**（広告あり・位置情報あり） |
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
- **アプリごとに「何を収集するか」が違う。ポリシーを流用しないこと。**
  「マイ電話番号」は収集なし、「二次元コード帳」は広告あり、
  「歩幅計Pro」は広告に加えて**位置情報も扱う**（端末内保存だが、CSVに出力される）

### 歩幅計Pro のポリシーで未確定の箇所

**同意管理（UMP）がまだアプリに実装されていない。**
「二次元コード帳」のポリシーには UMP で同意を確認すると書いてあるが、
歩幅計Pro に写すと事実と違う記述になるため、あえて書いていない。

UMP を実装したら、または配信国を EEA / 英国以外に限定したら、
`privacy/steplengthpro.html` と `.en.html` に同意についての節を足すこと。

## 手元での確認

```bash
python3 -m http.server 8765
# http://127.0.0.1:8765/ を開く
```
