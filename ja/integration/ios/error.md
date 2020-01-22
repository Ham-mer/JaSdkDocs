# AdLime SDK のエラー

ここでは AdLime SDK エラーコードとエラーメッセージについて説明します。

## エラーの確認方法

エラーの出力方法は大きく分けて二通りの方法があります。一つは広告のイベント制御によって取得する方法、２つ目はデバッグログによって取得する方法です。前者はプログラムの中で簡潔な広告のエラーを取得できる方法です。広告のエラーハンドリングを実装する場合は前者の方法を使ってください。後者は広告の詳細のエラーをデバッグログ中に取得する方法です。ある広告ネットワークで広告のリクエストに失敗したなど、広告のロードに問題があったときにその原因究明したい場合は後者を使ってください。

### 広告のイベント制御によるエラーの取得

各広告フォーマットごとのガイドを確認してください。

#### 基本的な広告フォーマット

- [バナー広告](./banner.md#広告イベント)
- [ネイティブ広告](./native.md#広告イベント)
- [インタースティシャル広告](./interstitial.md#広告イベント)
- [動画リワード広告](./rewarded.md#広告イベント)

### 複合型広告枠
- [MixViewAd](./mixviewad.md#広告イベント)
- [MixFullScreenAd](./mixfullscreenad.md#広告イベント)

## デバッグログによるエラーの取得方法

[AdLime SDK の導入](./init.md#初期化)を確認してください。


## エラーコードとエラーメッセージ

AdLimeAdErrorCode エラーコード一覧  
|定義                           |説明    |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | リクエストが無効 |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットワークエラー |
|ADLIME_ADERROR_NO_FILL         | 配信できる広告がない    |
|ADLIME_ADERROR_TIMEOUT         | リクエスト　タイムアウト |

エラーには 広告枠 ID(AdUnit)、広告ネットワーク名(Network)、広告のプロパティ(LineItem)が含まれます。

```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```


