# 3. 作業の流れ（PUSH手順書）

作業のたびにこの手順を上から順にやります。慣れるまではこのページを開いたまま作業してください。

```
① Issue を決める → ② main を最新にする → ③ ブランチを作る → ④ 編集してコミット
→ ⑤ push → ⑥ PR を出す → ⑦ レビュー → ⑧ マージ → ⑨ 後片付け
```

---

## ① Issue を決める

- GitHub の Issues タブで、やる作業の Issue を選ぶ（なければ作る）
- 右側の **Assignees** に自分を設定する（「これは自分がやってます」の宣言。作業の被りを防ぐ）
- Issue 番号をメモ（例：`#12`）

## ② main を最新にする

他の人の変更を取り込んでから始めます。**これを忘れるとコンフリクトの原因になります。**

| VS Code | コマンド |
|---|---|
| 左下のブランチ名をクリック → `main` を選ぶ | `git switch main` |
| 左下の同期ボタン（🔄）を押す。または ソース管理 → `…` → プル | `git pull` |

## ③ ブランチを作る

名前のルールは `種類/Issue番号-短い説明`（詳しくは [チームルール](04-team-rules.md#ブランチ名)）。

例：`feature/12-tab-group`、`fix/15-crash-on-startup`

| VS Code | コマンド |
|---|---|
| 左下のブランチ名 → 「新しいブランチを作成…」→ 名前を入力 | `git switch -c feature/12-tab-group` |

左下の表示が新しいブランチ名になっていれば成功です。

## ④ 編集してコミット

コードを書きます。キリのいいところで（動く単位で）こまめにコミットします。

| VS Code | コマンド |
|---|---|
| 左の「ソース管理」アイコンを開く | `git status` |
| 変更されたファイルを確認し、含めたいファイルの **＋** を押す | `git add ファイル名`（全部なら `git add .`） |
| 上の欄にメッセージを書く（例：`feat: タブのグループ化を追加`） | |
| 「コミット」ボタン | `git commit -m "feat: タブのグループ化を追加"` |

**コミット前に必ず確認：**
- [ ] 今いるのが作業ブランチである（**main ではない**）
- [ ] `.env`、APIキー、パスワード、個人的なメモファイルが含まれていない
- [ ] 関係ないファイル（`node_modules`、`.DS_Store` など）が含まれていない
- [ ] アプリが起動する（壊れたままコミットしない）

## ⑤ push する

| VS Code | コマンド |
|---|---|
| 初回：「ブランチの発行」ボタン | 初回：`git push -u origin feature/12-tab-group` |
| 2回目以降：同期ボタン | 2回目以降：`git push` |

### 作業中に main が進んでいた場合

自分が作業している間に、他の人の PR が main にマージされることがあります。PR 画面で「This branch is out-of-date」と出たり、コンフリクトの表示が出たら、main の変更を自分のブランチに取り込みます。

| VS Code | コマンド |
|---|---|
| ソース管理 → `…` → ブランチ → ブランチをマージ… → `origin/main` | `git fetch` → `git merge origin/main` |

コンフリクトが起きたら [困ったとき](05-troubleshooting.md#コンフリクトが起きた) へ。

> `rebase` というやり方もありますが、このチームでは **使いません**。慣れるまでは merge だけで十分です。

## ⑥ Pull Request を出す

1. push すると GitHub のリポジトリページに「Compare & pull request」ボタンが出るので押す
2. base が `main`、compare が自分のブランチになっているか確認
3. タイトルを書く（コミットと同じ形式：`feat: タブのグループ化を追加`）
4. 本文はテンプレートに沿って書く。**`Closes #12`** を必ず入れる
5. 右側の **Reviewers** に他のメンバーを1人以上指定
6. 「Create pull request」

まだ途中だけど見てほしいときは「Create draft pull request」で下書きとして出せます。

## ⑦ レビューを受ける／直す

- コメントがついたら、同じブランチで修正してコミット → push するだけ。PR に自動で追加されます
- 対応したコメントには返信して、「Resolve conversation」を押す
- 意見が割れたら、PR のコメントで話し合う（口頭・Discord で決めたら、結論を PR に書き残す）

## ⑧ マージする

承認（Approve）が1つ以上つき、未解決のコメントがなくなったら、**PR を出した本人がマージ** します。

1. PR 画面の下の「Squash and merge」を押す
2. まとめられたコミットメッセージを確認（PR タイトルになっていればOK）
3. 「Confirm squash and merge」
4. ブランチは自動で削除されます（されなければ「Delete branch」を押す）

## ⑨ 後片付け

| VS Code | コマンド |
|---|---|
| 左下から `main` に切り替え → 同期 | `git switch main` → `git pull` |
| ソース管理 → `…` → ブランチ → ブランチの削除… → 終わったブランチ | `git branch -d feature/12-tab-group` |

これで1サイクル完了です。次の作業は ① からまた始めます。

---

## 1枚まとめ（コマンド版）

```bash
git switch main
git pull
git switch -c feature/12-tab-group
# … 編集 …
git status
git add .
git commit -m "feat: タブのグループ化を追加"
git push -u origin feature/12-tab-group
# → GitHub で PR を作成 → レビュー → Squash and merge
git switch main
git pull
git branch -d feature/12-tab-group
```
