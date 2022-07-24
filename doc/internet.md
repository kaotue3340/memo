1. ブラウザの検索ボタンクリック
1. URLを解読
1. キャッシュにIPアドレスがあるか確認
1. DNSからIPアドレスを取得
1. IPアドレスでサーバーにリクエストを実行
1. ポート番号を割り当てる
1. HTTPリクエストを送信する
1. HTTPレスポンスを受信する
1. レンダリング

```mermaid
flowchart TD
  A1["ブラウザのアドレスバーにURLを入力\nhttps://twitter.com/kaotue1"]-->
  A2["検索ボタンクリック"]-->B1
　subgraph URLを解読
  B1{"キャッシュに\nIPアドレスがあるか"} --> |Yes| B2[OK]
  B1 --> |No| B9[DNSサーバへ問い合わせ] --> B9
  B2["ポート番号を割り当てる"] -->
  B3{"URLにポート番号が\n指定されているか"} --> |Yes| B4
  B3 --> |No| B99["ブラウザが自動付与\nHTTP->80\nHTTPS->443"] --> B4
  B4["【URLの解析結果】\n\nhttps://twitter.com/kaotue1\n↓\nhttps://:443"]
  end
```

## URL (Uniform Resource Locator)
インターネット上のリソースを一意に特定するための名前

## DNS (Domain Name System)
IPアドレスとドメインを関連して管理する仕組み
