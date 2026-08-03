# livechat

トークイベント用のリアルタイムコメント・アンケートシステムです。
観客はスマートフォンから匿名でコメントとスタンプを送り、発表画面のスライドの上に弾幕として流れます。
発表中にアンケートを出して、その場で集計を見せることもできます。

## 参加する

<img src="qr_readme.png" width="200" alt="投稿ページのQRコード">

**→ [投稿ページを開く](https://naotaro713.github.io/livechat/)**

## 画面の構成

| 画面 | 役割 | 使う人 |
| --- | --- | --- |
| [投稿ページ](https://naotaro713.github.io/livechat/) （`index.html`） | コメント・スタンプの投稿とアンケートへの回答 | 観客 |
| [発表画面](https://naotaro713.github.io/livechat/present.html) （`present.html`） | PDFスライドの表示、弾幕、アンケートの集計 | 登壇者 |
| [管理画面](https://naotaro713.github.io/livechat/admin.html) （`admin.html`） | 保留コメントの確認・削除、全体停止、アンケートの作成 | 運営 |

管理画面はログインが必要です。発表画面と管理画面のURLは観客には配らず、QRコードで案内するのは投稿ページだけにしてください。

イベントを分けたいときは、URL の末尾に `?e=イベントID` を付けると別のイベントとして動きます。
例: `https://naotaro713.github.io/livechat/?e=talk-0901`

`present.html` は PowerPoint を PDF で書き出したファイルを読み込みます。
PDF はブラウザの中だけで処理され、どこにも送信されません。

## 発表画面のキー操作

| キー | 動作 |
| --- | --- |
| `→` `Space` | 次のページ |
| `←` | 前のページ |
| `F` | 全画面の切り替え |
| `C` | コメント表示の ON・OFF |
| `P` | アンケート集計の表示・非表示 |
| `D` | テスト用のダミーコメントを流す |

市販のプレゼンリモコンは `→` `←` を送るので、そのまま使えます。

## 構成

- ホスティング: GitHub Pages
- データベース: Cloud Firestore（Spark 無料プラン）
- 管理画面のログイン: Firebase Authentication（メール／パスワード）
- ビルド不要。3つの HTML ファイルだけで動きます。

## セキュリティルール

`firestore.rules` の内容を Firebase コンソールの Firestore Database → ルール に貼り付けて公開してください。
観客は作成のみ可能で、書き換え・削除・非表示化はログイン済みの管理者だけができます。

なお、HTML 内の `apiKey` は Firebase の仕様上、公開されても問題のない識別子です。
アクセスの制御はセキュリティルール側で行っています。
