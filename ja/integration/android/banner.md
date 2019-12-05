# バナー広告を導入する

バナー広告とは、アプリのレイアウトにおいて特定の位置を占める矩形のイメージ広告またはテキスト広告です。この種の広告は、ユーザーがアプリを操作している間は画面に広告が残り、一定の時間が経過すると自動的に更新することが特徴です。モバイル広告を初めて掲載する場合は、まずバナー広告から始めることが最適です。

このガイドでは、AdLime のバナー広告を Android アプリに組み込む方法について説明します。

## 前提条件
- AdLime SDK が導入済みであること

## レイアウトに BannerAdView を追加する

バナー広告を表示するには、まず広告を表示する Activity か Fragment のレイアウトに BannerAdView を追加する必要があります。該当するコンテナのレイアウトファイルにそれを追加することはお勧めの方法です。

```java
// 広告ユニットID の定義
String bannerId = "47033ec3-5bf9-4865-a5d7-d1fbb9f7fbc8";
// BannerAdView を作成
BannerAdView mBannerAdView = new BannerAdView(context);
mBannerAdView.setAdUnitId(bannerId);
// バナーのコンテナを取得
ViewGroup container = findViewById(R.id.banner_container);
// コンテナに BannerAdView を追加する
container.addView(mBannerAdView);
```

## NetworkConfigsの設置
NetworkConfigsを通じて，各NWの特殊な設置を満たせる。ここでの設置は[初期化](./init.md)の全体の設置をカバーする<br>
[Mediation ドキュメント](./mediation.md)でNWにサポートされるNetworkConfigを確認できる。

```java
mBannerAdView.setNetworkConfigs(NetworkConfigs.Builder()
                    .addConfig(AppLovinBannerConfig.Builder()
                            // 自動デストロイかどうかの設置
                            .setAutoDestroy(false)
                            .build())
                    .addConfig(...)
                    .build());
```

## 広告を読み込む

BannerAdView を追加したら、次は広告の読み込みです。BannerAdView クラスの loadAd() メソッドで行うことができます。

```java
// 広告を読み込む
mBannerAdView.loadAd();
```
これでアプリにバナー広告を表示できるようになりました。

## 広告イベント
広告の動作をより細かくカスタマイズするには、広告のライフサイクルで発生するイベント（読み込み、開始、終了など）を追加することができ、AdListener クラスを使い、これらのイベントを受け取ることができます。

BannerAdView で AdListener を利用するには、 setAdListener() メソッドを呼び出してください。

```java
mBannerAdView.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 広告の読み込み失敗、エラー詳細は adError から取得
        Log.d(TAG, "on BannerAd FailedToLoad err:" + adError.toString());
    }

    @Override
    public void onAdLoaded() {
        // 広告のロード完了
    }

    @Override
    public void onAdClosed() {
        // 広告を閉じる
        Log.d(TAG, "on BannerAd Closed");
    }

    @Override
    public void onAdClicked() {
        // 広告をクリック
        Log.d(TAG, "on BannerAd Clicked");
    }

    @Override
    public void onAdShown() {
        // 広告を表示
        Log.d(TAG, "on BannerAd Shown");
    }
});
```

### エラー
広告の読み込に失敗した場合は、AdListener の onAdFailedToLoad(AdError adError) が呼び出されます。その際に adError.getCode()、adError.toString() から、エラーコード、エラー情報が取得できます。

 AdError エラーコード一覧
|定義                        |説明     |
|:--------------------------|:--------|
|ERROR_CODE_INTERNAL_ERROR  | 内部エラー |
|ERROR_CODE_INVALID_REQUEST | リクエストが無効 |
|ERROR_CODE_NETWORK_ERROR   | ネットワークエラー |
|ERROR_CODE_NO_FILL         | 配信できる広告がない    |
|ERROR_CODE_TIMEOUT         | リクエスト　タイムアウト |

エラーは AdUnit、ネットワーク、ラインアイテムの各情報が含まれています。

```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## バナーのサイズ

**注意：広告を配置するコンテナのサイズは、バナーのサイズと同じか、それ以上の大きさにする必要があります。コンテナにパディングがある場合は、それだけバナーを表示できるコンテナの領域が小さくなります。**  

標準のバナーサイズについて、下記の表をご参照ください。

サイズ（dp）|説明          |対応端末  
:-                         |:-            |:- 
|320 x 50                    |バナー      |スマートフォン・タブレット 
|320 x 100                   |バナー（大）      |スマートフォン・タブレット
|300 x 250                   |IABレクタングル（中）    |スマートフォン・タブレット
|468 x 60                    |IAB フルサイズバナー  |タブレット
|728 x 90                    |IAB ビッグバナー   |タブレット
|smart                     |スマートバナー        |スマートフォン・タブレット

### スマートバナー

スマートバナーは、画面のサイズや向きにかかわらず、横幅いっぱいに広告が表示されます。現在は一部の広告プラットフォームのみに対応しています。

## プリロードとキャッシュ
プリロードで事前に広告を用意して展示するまでの時間を短くする<br>
広告をプリロードするかどうかにもかかわらず、広告をキャッシュすることはお勧め。理由としては一つのAdUnitに各LineItemはロードされるはずで、一つの広告インスタンスを繰り返して使うと、展示率を高めて必要ではないリクエストも減らせる。
自ら広告キャッシュを実現できるし、[AdLimeLoader](./adloader.md)でも実現できる。