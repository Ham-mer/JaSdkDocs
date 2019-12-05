#  MixViewAd
MixViewAdは名前通り、単一の容器で違うタイプの広告を組み合わせて使う。例えば、もともとバナー広告しかリクエストできない容器は MixViewAdを使うとバナー広告だけではなく、ネイティブ広告とフィードリスト広告もリクエストできる。そうすると、この広告容器のフィルレートとマネタイズ能力は高めらる。

今ではMixViewAd はバナー、ネイティブ、フィードリストをサポートする。MixViewAdは一回では一つのフィードリスト広告をリクエストする。

本ガイドではMixViewAdをAndroidのアプリに組み込む方法を紹介する。
## 前提条件
- AdlimeのSDKの導入

## MixViewAdの作成
MixViewAd はMixViewAdの対象でリクエストと展示。まずはMixViewAdを実例化してAdunit IDを設置する。

```java
MixViewAd mMixViewAd = new MixViewAd(context);
mMixViewAd.setAdUnitId("AdUnit_ID");
```

::: tip
もし広告枠にFlurry/Unity Adsのバナー広告がある場合にコンストラクタにActivityを送る必要がある。
:::

##  NetworkConfigsの設置

**NetworkConfigは必要ではなくて広告NWの特別配置を設置するためです。<br>[Mediation 文档](./mediation.md)で広告NWがサポートできるNetworkConfigを確認できる，広告NWドキュメントでは詳細は確認できる。**

ここの配置は[初期化](./init.md)時の全体配置をカバーする。例えばここの AppLovinBannerConfigは初期化時に配置される全体の AppLovinBannerConfigをカバーする。

```java
mMixViewAd.setNetworkConfigs(NetworkConfigs.Builder()
                .addConfig(AppLovinBannerConfig.Builder()
                            // 自動デストロイの設置
                            .setAutoDestroy(false)
                            .build())
                    .addConfig(...)
                .build());
```

## 広告のロード
MixViewAdをロードするために， MixViewAdのオブジェクトの loadAd() 方法を使ってください。

```java
mixViewAd.loadAd();
```

## 広告イベント
広告のライフサイクルに各イベントを追加できる。例えばロード、開く、閉じるなど。 AdListenerでモニターできる。

 MixViewAdでAdListenerを使うために， setAdListener() 方法を使ってください：

```java
mMixViewAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        // ロード成功
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // ロード失敗，adErrorはエラーコード
        Log.d(TAG, "onAdFailedToLoad: " + adError.toString());
    }

    @Override
    public void onAdShown() {
        // 広告展示
    }

    @Override
    public void onAdClicked() {
        // 広告クリック
    }

    @Override
    public void onAdClosed() {
        // 広告閉じる
    }
});

mMixViewAd.loadAd();
```

### エラーコード
広告ロード失敗の時に、当广告加载失败时， AdListener の onAdFailedToLoad(AdError adError)はコールバックされる 。 adError.getCode()、adError.toString()でエラーコードとエラー情報を取得できる。

エラーコードの定義は AdErrorにある ：
|定義                        |説明     |
|:--------------------------|:--------|
|ERROR_CODE_INTERNAL_ERROR  | 内部エラー |
|ERROR_CODE_INVALID_REQUEST | 無効リクエスト |
|ERROR_CODE_NETWORK_ERROR   | ネットエラー |
|ERROR_CODE_NO_FILL         | no fill   |
|ERROR_CODE_TIMEOUT         | リクエスト　タイムアウト |

エラー情報は AdUnit 、Network、LineItem の情報を含める、例は下記通り：
```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## 広告展示
広告ロードされてユーザさんに展示されることしかない<br>
MixViewAd のネイティブ広告とフィードリスト広告の外観は開発者のカスタムで設定できる。AdLime で提供される NativeAdLayoutで広告のレイアウトを管理できる。 ネイティブ広告の各 View は含まれる。<br>
AdLimeMixViewAd の getAdViewで: すでにフィルされる広告のクリエイティブのViewを取れる。Viewの外観は AdLimeNativeAdLayoutの要素と同じ。<br>
このViewをページの適当なところに追加してアプリはMixView広告を展示できる。

** NativeAdLayoutについて[NativeAdLayout](https://www.adlime.net/docs/ja/integration/android/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できる。**

```java
mMixViewAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        NativeAdLayout layout = NativeAdLayout.getLargeLayout1();
        View view = mMixViewAd.getAdView(layout);
        if(view != null) {
            mMixViewAdContainer.removeAllViews();
            mMixViewAdContainer.addView(view);
        }
    }
});

mMixViewAd.loadAd();
```

MixViewAdを作成してNativeAdLayoutを設置する。そうすると、MixViewAdのgetAdView()を調達する時に、layoutのパラメーターを送らなくても構わない。
```java
NativeAdLayout layout = NativeAdLayout.getLargeLayout1();
mMixViewAd.setNativeAdLayout(layout);

mMixViewAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        View view = mMixViewAd.getAdView();
        if(view != null) {
            mMixViewAdContainer.removeAllViews();
            mMixViewAdContainer.addView(view);
        }
    }
});

mMixViewAd.loadAd();
```

## プリロードとキャッシュ
プリロードで広告を事前に用意できて展示までの時間を短くする。<br>
プリロードに問わず、広告をキャッシュすることはお勧め。りゆうとして、一つのAdUnitにいくつかのLineitemはロード成功される。同じ広告オブジェクトを重複しようすると展示率を高めて必要ではない広告リクエストも減らせる。
自分の方法で広告をキャッシュできるし、 [AdLimeLoader](./adloader.md)で広告をキャッシュできる。