1. ブラウザの検索ボタンクリック
1. URLを解読
1. キャッシュにIPアドレスがあるか確認
1. DNSからIPアドレスを取得
1. ポート番号を割り当てる
1. IPアドレスでサーバーにリクエストを実行
1. HTTPリクエストを送信する
1. HTTPレスポンスを受信する
1. レンダリング

```mermaid
flowchart TD
　subgraph ブラウザ
  A1["検索ボタンクリック"]-->
  A2["URLを解析\nhttps://twitter.com/kaotue1"]-->B1
  B1{"キャッシュに\n「twitter.com」の\nIPアドレスがあるか"} --> |Yes| B2[OK]
  B1 --> |No| B9
  B2["ポート番号を割り当てる"] -->
  B3{"URLにポート番号が\n指定されているか"} --> |Yes| B4
  B3 --> |No| B99["ブラウザが自動付与\nHTTP->80\nHTTPS->443"] --> B4
  B4["【URLの解析結果】\n\nhttps://twitter.com/kaotue1\n↓\nhttps://133.106.196.78:443"]-->C1
  end
  subgraph "リゾルバ(プロトコル・スタック)"
  B9[DNSサーバへ\n問い合わせ開始]-->
  R0["DNS名前解決の開始\nトップダウン形式"]-->
  R1[("【最寄りのDNSサーバ】\n\nルートドメインサーバの\nIPアドレスを取得")]-->
  R2[("【ルートドメインサーバ】\n\nトップレベルドメイン(com)サーバの\nIPアドレスを取得")]-->
  R3[("【トップレベルドメインサーバ(com)】\n\ntwitterのIPアドレスを取得")]-->B2
  end
  subgraph "プロトコル・スタック"
  C1["HTTPリクエスト送信"]-->
  C2["twitterへリクエスト"]-->
  C3[("【twitterサーバ】\nレスポンスを返却")]-->D0
  end
  subgraph "ブラウザ"
  D0["ブラウザへレスポンス返却"]-->
  D2["Loading\nHTML・CSSなどを読み込み"]-->
  D3["Scripting\nJavascriptを実行"]-->
  D4["Rendering"]-->
  D5["Painting"]
  end
```

## URL (Uniform Resource Locator)
インターネット上のリソースを一意に特定するための名前

## DNS (Domain Name System)
IPアドレスとドメインを関連して管理する仕組み

## Socketライブラリ
OSに組み込まれているネットワーク機能をアプリケーション(ブラウザなど)から呼び出すためのプログラム群

## DNSリゾルバ
Socketライブラリの中の一プログラム
DNSの名前解決を実行するプログラム

## プロトコル・スタック
OSに組み込まれているネットワーク制御用のプログラム
