# 6. オーナー向け設定

オーナーが最初に一度だけ行う設定です。「取り返しのつかない事態」を仕組みで防ぐのが目的です。
（GitHub の画面の文言は変わることがあります。見つからなければ近い名前の項目を探してください）

## 6-1. メンバーを招待する

Settings → Collaborators → **Add people** → メンバーの GitHub ユーザー名

- Organization のリポジトリの場合は、Organization の People から招待し、リポジトリに **Write** 権限を付与
- **Admin 権限はオーナーだけ**。メンバーは Write で十分（Write ならブランチ作成・push・PR・マージができる。設定変更や削除はできない）

## 6-2. main ブランチを保護する（最重要）

Settings → Rules → Rulesets → **New ruleset** → New branch ruleset

| 項目 | 設定 |
|---|---|
| Ruleset name | `protect-main` |
| Enforcement status | **Active** |
| Bypass list | **空のまま**（オーナーも同じルールで練習する） |
| Target branches | Add target → **Include default branch** |
| Restrict deletions | ✅（main の削除を禁止） |
| Block force pushes | ✅（履歴の書き換えを禁止） |
| Require a pull request before merging | ✅ |
| └ Required approvals | **1** |
| └ Dismiss stale pull request approvals when new commits are pushed | ✅（承認後に変更されたら再承認が必要） |
| └ Require conversation resolution before merging | ✅（未解決のコメントがあるとマージできない） |

これで、main への直接 push・force push・削除がすべて GitHub 側でブロックされます。

> Public リポジトリなら無料プランでも使えます。

## 6-3. マージ方法を統一する

Settings → General → Pull Requests

- ✅ Allow squash merging（Default commit message は「Pull request title」推奨）
- ⬜ Allow merge commits（オフ）
- ⬜ Allow rebase merging（オフ）
- ✅ **Automatically delete head branches**（マージ後にブランチを自動削除）

Squash だけにすることで、main の履歴が「1 PR ＝ 1 コミット」になり、後から読みやすく、戻すのも簡単になります。

## 6-4. 秘密情報の流出対策

Settings → 左メニュー「Security and quality」の中の **Advanced Security**

- **Secret Protection** の右にある「Enable」を押す（以前は「Secret scanning」という名前だった機能）
- 有効にすると、その下に出る **Push protection** も有効になっているか確認（既知の形式の API キーなどを含む push を GitHub が止める）
- Dependabot alerts も有効にしておく（依存パッケージの脆弱性通知）

> GitHub の画面は名前や場所がよく変わります。見つからないときは Settings の左メニューで「Security」を含む項目を探してください。Public リポジトリなら無料で使えます。

加えて、リポジトリの `.gitignore` に以下が入っているか確認：

```gitignore
# 依存関係・ビルド成果物
node_modules/
dist/
out/
release/

# 秘密情報
.env
.env.*
!.env.example

# ローカルDB・実験
*.sqlite3
*.db

# OS・エディタ
.DS_Store
Thumbs.db
.vscode/*
!.vscode/extensions.json
!.vscode/settings.json
```

既存の `.gitignore`（`app/_experiments/` まわりなど）と突き合わせて、足りないものだけ追加してください。

## 6-5. テンプレートとファイルを置く

`for-trueful-repo/` フォルダの中身を Trueful リポジトリのルートにコピーして、PR でマージします（これ自体を最初の PR にするのがおすすめ）。

| ファイル | 役割 |
|---|---|
| `CONTRIBUTING.md` | 参加ルールの要約。GitHub が PR/Issue 作成時にリンクを表示する |
| `.github/pull_request_template.md` | PR 作成時に本文の雛形が自動で入る |
| `.github/ISSUE_TEMPLATE/*.md` | Issue 作成時にバグ報告／機能提案を選べる |
| `.gitattributes` | 改行コードを LF に統一（Mac/Windows 混在対策） |

> `.gitattributes` を後から追加した場合、既存ファイルの改行を揃えるために一度 `git add --renormalize .` → コミットしておくと安心です。

## 6-6. ラベルを整える

Issues → Labels。最初からある `bug` `enhancement` `documentation` `good first issue` `question` で十分です。必要なら追加：

- `priority: high` … 急ぎ
- `blocked` … 他の作業待ち

## 6-7. （任意）Discord に通知を流す

GitHub の動き（PR 作成、Issue 作成、マージなど）を Discord の専用チャンネルに流すと、GitHub を見に行くきっかけになります。

1. Discord：通知用チャンネルの設定 → 連携サービス → ウェブフック → 新しいウェブフック → URL をコピー
2. GitHub：Settings → Webhooks → Add webhook
   - Payload URL：コピーした URL の **末尾に `/github` を付ける**
   - Content type：`application/json`
   - イベント：「Let me select individual events」→ Issues、Pull requests、Pull request reviews、Pushes など
3. 保存して、テスト用 Issue を作って通知が来るか確認

通知が多すぎると見なくなるので、専用チャンネルを作るのがおすすめです。

## 6-8. （任意）GitHub Projects

Issue をカンバン（Todo / In Progress / Done）で見たくなったら、Projects タブで Board を作ります。3人なら最初は Issue 一覧だけで十分なので、慣れてから導入すれば大丈夫です。

## 6-9. OSS として

- `LICENSE` ファイルがあるか確認（ないと、他人は法的にコードを使えない）
- `CONTRIBUTING.md` があると、外部の人も参加ルールを把握できる

## 設定後の動作確認

- [ ] メンバーが main に直接 push しようとすると拒否される
- [ ] 承認なしでは PR をマージできない
- [ ] マージ後にブランチが自動削除される
- [ ] PR 作成時にテンプレートが表示される
