# 2. 環境構築

最初に一度だけやります。Mac と Windows で違う部分は分けて書いています。

## 2-1. GitHub アカウントの準備

1. GitHub アカウントを作る（持っていればOK）
2. **2段階認証を有効にする**（Settings → Password and authentication）
3. **メールアドレスを非公開にする**
   Trueful は Public リポジトリなので、コミットに記録されたメールアドレスは誰でも見られます。
   - Settings → Emails → 「Keep my email addresses private」にチェック
   - 同じ画面に表示される `12345678+ユーザー名@users.noreply.github.com` をメモしておく（2-3で使う）
4. オーナーから届く **Collaborator の招待** を承認する（メールか GitHub の通知から）

## 2-2. Git のインストール

### Mac

ターミナルで次を実行します。

```bash
git --version
```

バージョンが出ればインストール済みです。出なければ、案内に従って「コマンドライン・デベロッパツール」をインストールしてください（`xcode-select --install` でも同じ）。

### Windows

1. https://git-scm.com/ から Git for Windows をダウンロードしてインストール
2. インストール中の選択肢は基本的に **初期値のままでOK**。変えるのは次の2つだけ：
   - 「Choosing the default editor」→ **Visual Studio Code**
   - 「Adjusting the name of the initial branch」→ **Override** を選んで `main`
3. インストール後、VS Code を再起動して、ターミナルで `git --version` が動けばOK

## 2-3. Git の初期設定（Mac/Windows 共通）

VS Code のターミナル（メニュー → ターミナル → 新しいターミナル）で実行します。

```bash
git config --global user.name "GitHubのユーザー名"
git config --global user.email "12345678+ユーザー名@users.noreply.github.com"
git config --global init.defaultBranch main
git config --global pull.rebase false
```

確認：

```bash
git config --global --list
```

> メールアドレスは 2-1 でメモした noreply アドレスを使います。本物のアドレスを入れると公開されます。

## 2-4. VS Code の準備

1. VS Code の左下のアカウントアイコン → **GitHub でサインイン**
   これで push/pull のときの認証が通るようになります
2. 入れておくと便利な拡張機能（任意）
   - **Git Graph** … ブランチの分岐を図で見られる。状況把握にとても便利
   - **GitHub Pull Requests** … VS Code 内で PR を見られる（慣れるまでは GitHub のサイトで操作する方が理解しやすいので、後回しでOK）

### どのツールを使うか

このチームでは **VS Code を基本** にします。この資料の手順はすべて「VS Code での操作」と「対応するコマンド」を並べて書いています。

- ボタン操作で進めてOK。ただしコマンドも横目で見ておくと、何が起きているか理解しやすい
- GitHub Desktop などの別ツールを使っても構いませんが、困ったときに助け合いやすいので揃えるのがおすすめ

## 2-5. リポジトリをクローンする

作業フォルダを決めておきます（例：`~/dev/`、Windows なら `C:\dev\`）。
**OneDrive や iCloud で同期されているフォルダの中には置かないでください。** 同期と Git がぶつかって壊れることがあります。

### VS Code

**やり方A：ボタンから（おすすめ）**

1. VS Code で何もフォルダを開いていない状態にする（開いていたら メニュー → ファイル → フォルダーを閉じる）
2. 左端のアイコン列から「ソース管理」（枝分かれしたようなアイコン）をクリック
3. 「**リポジトリのクローン**」ボタンを押す
4. 画面上部に入力欄が出るので、`https://github.com/Trueful/Trueful.git` を貼り付けて Enter
5. 保存先フォルダを選ぶ → クローンが終わったら「開く」

**やり方B：コマンドパレットから**

コマンドパレットは、VS Code のあらゆる機能を名前で検索して実行できる検索窓です。

1. Mac: `Cmd+Shift+P` / Windows: `Ctrl+Shift+P` を押す
2. 画面上部に検索窓が出るので `clone` と入力
3. 候補に出る「**Git: クローン**」（英語表示なら `Git: Clone`）をクリック
4. 以降はやり方Aの 4〜5 と同じ

### コマンド

```bash
cd ~/dev
git clone https://github.com/Trueful/Trueful.git
cd Trueful
```

最初の練習では、このガイドのリポジトリも同じ手順でクローンしてください。

## 2-6. Trueful 本体の開発環境

Trueful を動かすための環境（Node.js、pnpm など）は、Trueful 本体の README に従ってください。

> Windows メモ：Trueful は `better-sqlite3`（ネイティブモジュール）を使っています。インストールでビルドエラーが出たら、エラー文を Discord に貼ってください。一人で抱え込まないこと。

## 2-7. 確認チェックリスト

- [ ] GitHub の2段階認証を有効にした
- [ ] メールアドレスを非公開にし、noreply アドレスを `git config` に設定した
- [ ] Trueful の Collaborator 招待を承認した
- [ ] VS Code で GitHub にサインインした
- [ ] リポジトリをクローンできた
- [ ] VS Code のターミナルで `git status` を打つと `On branch main` と出る
