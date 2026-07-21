# Language-processor — 言語処理系 試験対策サイト 共有リポジトリ

「言語処理系」の試験対策として、各自が作成したサイトや資料を共有するためのリポジトリです。

> この組織は **1授業 = 1リポジトリ** で運用しています。組織全体の方針・他授業のリポジトリ一覧は
> [Test-preparation プロフィール](https://github.com/Test-preparation) を参照してください。
> このREADMEは共通テンプレ [`CONTRIBUTING-TEMPLATE.md`](https://github.com/Test-preparation/.github/blob/main/CONTRIBUTING-TEMPLATE.md)
> から生成しています（授業名＝言語処理系 / リポジトリ名＝Language-processor）。

## 📁 ルール: 1人1フォルダ

**自分専用のサブフォルダを作り、その中に一式を置いてください。**
root 直下や他人のフォルダには触れないこと（上書き・衝突防止のため）。

```
Language-processor/
├── README.md            ← このファイル
├── kasuteara/           ← 蒲谷佳和 のサイト
│   ├── index.html
│   └── images/ …
├── <あなたのGitHub名>/   ← あなたのサイトはここに
│   └── index.html …
└── …
```

- フォルダ名は **自分のGitHubユーザー名** を推奨（半角英数で URL/Pages と相性が良い）。
- そのフォルダの中に `index.html` を置けば、あなたのサイトの入口になります。

## ⚠️ index.html だけで足りるか確認

- **自己完結型**（画像を `data:image` の base64 で埋め込み・外部ファイル参照なし）
  → `index.html` 1枚だけ置けばOK。
- **外部ファイル参照型**（`<img src="images/…">` のように別ファイルを読む）
  → `index.html` と一緒に **`images/` などの参照ファイルもすべて** 同じフォルダに入れること。
  入れ忘れると画像がリンク切れ（×表示）になります。

判定の目安（自分のindex.htmlがあるフォルダで実行）:
```bash
grep -c 'src="images/' index.html   # 1以上なら images/ フォルダも必要
grep -c 'data:image'   index.html   # 多ければ自己完結寄り
```

## 🤖 いちばん簡単: Claude Code / AIエージェントに任せる

[Claude Code](https://claude.com/claude-code) を使っているなら、下の文の `←ここ` を自分の値に書き換えて、そのまま貼り付けて頼めば全部やってくれます（フォーク→自分フォルダ作成→軽量化の確認→PR作成まで）。

```text
GitHubの Test-preparation/Language-processor に、私の言語処理系サイトを共有したい。
- 私のサイトのローカルパス: C:\path\to\my-site   ←ここ
- リポジトリのREADMEにある「1人1フォルダ規約」に従って、フォルダ名は私のGitHubユーザー名にして。
- 私はこのリポジトリへの直接の書き込み権限が無いので、フォーク→自分のフォルダに追加→プルリクエストの流れでお願い。
- index.htmlが外部画像(images/等)を参照しているなら、その参照ファイルも一緒に入れて。表示に使わない重いファイルは省いて軽量化して。
```

事前に GitHub CLI のログインだけ済ませておくこと（一度だけ）:
```bash
gh auth login
```

手動でやりたい人は下記の方法A/Bを参照。

## 🚀 手動で追加する方法

> **前提**: [GitHub CLI](https://cli.github.com/) (`gh`) と `git` が入っていて、`gh auth login` 済みであること。
> **Windows (PowerShell) の人**: `mkdir NAME` はそのまま使えます。コピーは `cp -r` の代わりに
> `Copy-Item -Recurse C:\path\to\my-site\* NAME\` を使ってください。
> `grep` が無ければ `Select-String 'src="images/' index.html` で代用できます。

### 方法A: フォーク + プルリクエスト（書き込み権限が無い人向け・推奨）

```bash
# 1. このリポジトリを自分のアカウントにフォークしてクローン
gh repo fork Test-preparation/Language-processor --clone
cd Language-processor           # フォークのローカルクローンに移動

# 2. 自分のフォルダ（=GitHubユーザー名）を作り、サイト一式をコピー
mkdir <あなたのGitHub名>
cp -r /path/to/あなたのサイト/* <あなたのGitHub名>/

# 3. コミットして自分のフォークに push（フォークの main へ）
git add <あなたのGitHub名>
git commit -m "Add <あなたの名前>'s site"
git push origin main

# 4. 本家へプルリクエストを作成（管理者がマージ）
gh pr create --repo Test-preparation/Language-processor --base main --head <あなたのGitHub名>:main
```

> 補足: 一度マージされた後にまた変更を出す時は、`git fetch upstream && git checkout -b 変更名 upstream/main`
> のように **upstream/main から新しいブランチを切って** PRを出すと衝突しません。

### 方法B: 直接 push（このリポジトリへの書き込み権限がある人向け）

```bash
git clone https://github.com/Test-preparation/Language-processor.git
cd Language-processor
mkdir <あなたのGitHub名>
cp -r /path/to/あなたのサイト/* <あなたのGitHub名>/
git add <あなたのGitHub名>
git commit -m "Add <あなたの名前>'s site"
git push origin main
```

## 💡 補足

- **軽量化**: サイト表示に使わない原資料スキャンや中間ファイルは、共有前に削っておくとリポジトリが軽くなります。
- **ブラウザ閲覧（GitHub Pages）**: Pages を有効化すると、各サイトを
  `https://test-preparation.github.io/Language-processor/<フォルダ名>/`
  のURLで直接閲覧できます（有効化は管理者が設定）。

## 参加者一覧

| フォルダ | 作者 | 内容 |
|---|---|---|
| `kasuteara/` | 蒲谷佳和 | 言語処理系 試験対策サイト（index.html + 図・過去問・MD資料） |
