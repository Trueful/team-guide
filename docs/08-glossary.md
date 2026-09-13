# 8. 用語集

GitHub や開発でよく出てくる言葉をまとめました。[1. Git と GitHub の基本](01-git-github-basics.md#用語集) に Git/GitHub 特有の用語（コミット・ブランチ・マージなど）はあるので、ここではそれ以外に「会話や記事でよく見るけど意味を確認したい」言葉を中心に集めています。

知らない言葉が出てきたら、まずここを検索（`Ctrl+F` / `Cmd+F`）してみてください。載っていなければ Discord で聞くか、このページに追加してPRを出してください（このリポジトリは練習場です）。

## GitHub・開発フローの略語

| 用語 | 読み方・元の単語 | 意味 |
|---|---|---|
| PR | Pull Request | ブランチを main に合体させてほしいという申請。[詳しくはこちら](01-git-github-basics.md#pullrequestpr合体の申請) |
| MVP | Minimum Viable Product | 「まず動く最小限の機能」のこと。最初から完璧を目指さず、必要最低限のものを作って試す考え方 |
| POC | Proof of Concept | 「これ実現できそう？」を確かめるための試作・検証 |
| WIP | Work In Progress | 「作業中」。まだ完成していないPRのタイトルによく付ける（例：`[WIP] タブグループ機能`） |
| LGTM | Looks Good To Me | 「良さそうです」。レビューで問題なかったときのコメントの定番 |
| RFC | Request for Comments | 「この設計どう思う？」と意見を募るための提案書・Issue |
| FYI | For Your Information | 「参考までに」。返信不要な情報共有につける |
| ASAP | As Soon As Possible | 「できるだけ早く」 |
| TBD | To Be Determined | 「未定・後で決める」 |
| ETA | Estimated Time of Arrival | 「完了予定時刻・見込み」 |

## プログラム・データの用語

| 用語 | 元の単語 | 意味 |
|---|---|---|
| API | Application Programming Interface | プログラム同士がやり取りするための窓口。「このURLにこう頼めば、こう返ってくる」という約束事 |
| CLI | Command Line Interface | ターミナルに文字で打ち込んで操作する画面。このガイドの `git` コマンドもCLI |
| GUI | Graphical User Interface | ボタンやアイコンをクリックして操作する画面。VS Code のソース管理パネルなど |
| UI | User Interface | ユーザーが直接触る画面・見た目の部分 |
| UX | User Experience | 使いやすさ・使ったときの体験そのもの |
| SDK | Software Development Kit | 特定の機能を作るための道具一式（ライブラリ＋ドキュメントなど） |
| DB | Database | データを保存しておく場所。「データベース」の略 |
| SQL | Structured Query Language | データベースに「これを取ってきて」と頼むための言語 |
| CRUD | Create / Read / Update / Delete | データ操作の基本4種（作成・読み取り・更新・削除） |
| JSON | JavaScript Object Notation | `{"key": "value"}` のような形式のデータ。設定ファイルやAPIのやり取りでよく使う |
| YAML | YAML Ain't Markup Language | インデントで構造を表すデータ形式。GitHub Actions の設定ファイルなどで使う |
| ENV | Environment Variable | 環境変数。APIキーなど「コードに直接書きたくない値」を入れておく仕組み。`.env` ファイルはコミットしない（[README](../README.md) 参照） |
| tmp | temporary | 「一時的」の略。`tmp` フォルダや `/tmp` は、一時的に使ってあとで消してもいいファイルの置き場所 |
| localhost | local host | 「自分のPCの中」を指すアドレス（`127.0.0.1`）。自分のPCで動かしているものを自分のブラウザで見るときに使う |
| キャッシュ（cache） | ― | 一度取得・計算した結果を保存しておいて、次回は速く済ませる仕組み |
| LRU | Least Recently Used | キャッシュがいっぱいになったとき、「一番長く使われていないもの」から捨てる方式 |

## インフラ・環境の用語

| 用語 | 元の単語 | 意味 |
|---|---|---|
| AWS | Amazon Web Services | Amazon が提供するクラウドサービス群。サーバーやデータベースをネット上で借りられる |
| サーバー（server） | ― | リクエストを受け取って処理・応答するコンピューター（役割） |
| デプロイ（deploy） | ― | 作ったものを本番環境（実際にユーザーが使う場所）に反映すること |
| ステージング環境 | staging | 本番公開の前に、本番に近い条件で最終確認するための環境 |
| 本番環境（production） | ― | 実際にユーザーが使っている環境。ここが壊れると全員に影響する |
| サンドボックス（sandbox） | ― | 本番に影響しない、自由に試せる隔離された環境 |
| CI/CD | Continuous Integration / Continuous Delivery(Deployment) | コードを push するたびに、自動でテストしたり本番に反映したりする仕組み。GitHub Actions など |

## その他よく見る言葉

| 用語 | 意味 |
|---|---|
| リポジトリ・repo | [1. Git と GitHub の基本](01-git-github-basics.md#用語集) 参照 |
| OSS | Open Source Software。ソースコードが公開されていて、誰でも見たり改良したりできるソフトウェア |
| README | リポジトリの説明書。このリポジトリの `README.md` もそれ |
| CHANGELOG | 「何がどう変わったか」を記録したファイル・リスト |
| バグ（bug） | プログラムの不具合 |
| デバッグ（debug） | バグの原因を探して直す作業 |
| ログ（log） | プログラムが動いた記録。エラー調査に使う |
| 依存関係（dependency） | あるプログラムが動くために必要な、他のライブラリ・パッケージ |
| ライブラリ / パッケージ | 誰かが作った「よく使う機能」をまとめて配布しているもの |

---

用語を追加したい場合は、この表に行を足してPRを出してください。実際にPull Requestを経験する練習にもなります。
