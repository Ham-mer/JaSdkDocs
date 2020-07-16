# AdLimeLoader - インタースティシャル  

AdLimeLoader は広告のキャッシュを管理、効率的に広告を表示する機能です。広告のキャッシュを管理することで、広告ロード回数を減らしたり、広告ロードのタイミングの効率化に望むことができます。

このガイドでは AdLimeLoader を用いたインタースティシャル広告の実装方法について説明します。

## AdLimeLoader による基本的な実装  

AdLimeLoader は各広告枠 ID ごとに広告のキャッシュを識別しています。AdLimeLoader を使って広告のロードや表示をする場合は、広告枠 ID ごとに広告をリクエストする必要があります。また一つの広告枠 ID に一つの広告を管理するため、複数の広告を同時に表示する際は対応する数の広告枠 ID を発行してください。

## InterstitialAd オブジェクトの取得  

AdLimeLoader を用いて広告を表示したり、広告のイベントを制御するなどのカスタマイズする必要がある場合は `InterstitialAd` オブジェクトを取得する必要があります。`InterstitialAd` を用いた実装方法は [インタースティシャル広告](./interstitial.md) を参考にしてください。

:::: tabs

::: tab Java

```java
InterstitialAd mInterstitialAd = AdLimeLoader.getInterstitial(context, "広告枠 ID");
```

:::

::: tab Kotlin

```kotlin
val mInterstitialAd = AdLimeLoader.getInterstitial(context, "広告枠 ID")
```

:::

::::

## 広告のロード  

まず、広告をロードしてみましょう。`AdLimeLoader`クラスの`loadInterstitial` を実行してください。

:::: tabs

::: tab Java

```java
AdLimeLoader.loadInterstitial(context, "広告枠 ID");
```

:::

::: tab Kotlin

```kotlin
AdLimeLoader.loadInterstitial(context, "広告枠 ID")
```

:::

::::

## 広告の表示  

広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `AdLimeLoader` の `isInterstitialReady` メソッドで確認してから `showInterstitial` メソッドで表示します。

:::: tabs

::: tab Java

```java
if(AdLimeLoader.isInterstitialReady("広告枠 ID")){
    AdLimeLoader.showInterstitial(context, "広告枠 ID");
} else {
    Log.d(TAG, "Ad isn't ready");
}
```

:::

::: tab Kotlin

```kotlin
if(AdLimeLoader.isInterstitialReady("広告枠 ID")) {
    AdLimeLoader.showInterstitial(context, "広告枠 ID")
} else {
    println("Ad isn't ready")
}
```

:::

::::

## 広告のイベント  

AdListener を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### インタースティシャル広告イベントを登録する  

インタースティシャル広告のイベントを取得するには、`SimpleAdListener` インスタンスを作成し、`setAdListener()` で登録します。AdLimeLoader では 広告枠 ID ごとに広告を管理するため `getInterstitial` メソッドで `InterstitialAd` オブジェクトを取得し、そのオブジェクトにイベントを登録します。この処理は `loadInterstitial` メソッド呼び出し前、または広告を表示する前に実行する必要があります。

:::: tabs

::: tab Java

```java
InterstitialAd mInterstitialAd = AdLimeLoader.getInterstitial(context, "広告枠 ID");
mInterstitialAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        // 広告のロード完了
        Log.d(TAG, "on InterstitialAd Loaded");
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 広告の読み込み失敗、エラー詳細は adError から取得
        Log.d(TAG, "on InterstitialAd FailedToLoad err:" + adError.toString());
    }

    @Override
    public void onAdShown() {
        // 広告を表示
        Log.d(TAG, "on InterstitialAd Shown");
    }

    @Override
    public void onAdClicked() {
        // 広告をクリック
        Log.d(TAG, "on InterstitialAd Clicked");
    }

    @Override
    public void onAdClosed() {
        // 広告を閉じる
        Log.d(TAG, "on InterstitialAd Closed");
    }
});
```

:::

::: tab Kotlin

```kotlin
val mInterstitialAd = AdLimeLoader.getInterstitial(this, "広告枠 ID")
mInterstitialAd.adListener = object: SimpleAdListener() {
    override fun onAdLoaded() {
        // 広告のロード完了
        print("on InterstitialAd Loaded")
    }

    override fun onAdFailedToLoad(adError: AdError?) {
        //  広告の読み込み失敗、エラー詳細は adError から取得
        print("onAdFailedToLoad: " + adError.toString())
    }

    override fun onAdShown() {
        //  広告を表示
        print("on InterstitialAd Shown")
    }

    override fun onAdClicked() {
        //  広告をクリック
        print("on InterstitialAd Clicked")
    }

    override fun onAdClosed() {
        //  広告を閉じる
        print("on InterstitialAd Closed")
    }
}
```

:::

::::
