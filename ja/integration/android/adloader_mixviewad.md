# AdLimeLoader - MixViewAd  

AdLimeLoader は広告のキャッシュを管理、効率的に広告を表示する機能です。広告のキャッシュを管理することで、広告ロード回数を減らしたり、広告ロードのタイミングの効率化に望むことができます。

このガイドでは AdLimeLoader を用いた MixViewAd の実装方法について説明します。

## AdLimeLoader による基本的な実装  

AdLimeLoader は各広告枠 ID ごとに広告のキャッシュを識別しています。AdLimeLoader を使って広告のロードや表示をする場合は、広告枠 ID ごとに広告をリクエストする必要があります。また一つの広告枠 ID に一つの広告を管理するため、複数の広告を同時に表示する際は対応する数の広告枠 ID を発行してください。

## MixViewAd オブジェクトの取得  

AdLimeLoader を用いて広告を表示したり、広告のイベントを制御するなどのカスタマイズする必要がある場合は `MixViewAd` オブジェクトを取得する必要があります。`MixViewAd` を用いた実装方法は [MixViewAd](./mixviewad.md) を参考にしてください。

:::: tabs

::: tab Java

```java
MixViewAd mMixViewAd = AdLimeLoader.getMixViewAd(context, "広告枠 ID");
```

:::

::: tab Kotlin

```kotlin
val mMixViewAd = AdLimeLoader.getMixViewAd(context, "広告枠 ID")
```

:::

::::

## 広告レイアウトの作成

広告のロード時や広告を表示するときに広告のレイアウトを事前に設定しておきましょう。ネイティブレイアウトの詳細な設定方法は[NativeAdLayout](./native.md#広告レイアウトの作成)で確認できます。

広告レイアウトは MixViewAd のロード時に設定できます。その設定方法は後の節で説明します。また `MixViewAd` オブジェクトを取得して、そのオブジェクトにネイティブレイアウトを設定することもできます。

:::: tabs

::: tab Java

```java
MixViewAd mMixViewAd = AdLimeLoader.getMixViewAd(context, "広告枠 ID");
mMixViewAd.setNativeAdLayout(NativeAdLayout.getLargeLayout1());
```

:::

::: tab Kotlin

```kotlin
val mMixViewAd = AdLimeLoader.getMixViewAd(context, "広告枠 ID")
mMixViewAd.setNativeAdLayout(NativeAdLayout.getLargeLayout1())
```

:::

::::

ネイティブレイアウトの設定は基本的に 1 回実行すれば十分です。サイズが変更になるなどレイアウトが変更される場合は再読込する必要があります。

## 広告のロード  

次に、広告をロードしてみましょう。`AdLimdLoader`クラスの`loadMixViewAd` を実行してください。またこのときにネイティブ広告のレイアウトを設定できます。

:::: tabs

::: tab Java

```java
AdLimeLoader.loadMixViewAd(context, "広告枠 ID", NativeAdLayout.getLargeLayout1());
```

:::

::: tab Kotlin

```kotlin
AdLimeLoader.loadMixViewAd(context, "広告枠 ID", NativeAdLayout.getLargeLayout1())
```

:::

::::

## 広告の表示  

広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `AdLimeLoader` の `isMixViewAdReady` メソッドで確認してから表示します。広告を表示する場合は `MixViewAd` オブジェクトを `getMixViewAd` メソッドで取得して表示しましょう。

:::: tabs

::: tab Java

```java
if(AdLimeLoader.isMixViewAdReady("広告枠 ID")){
    MixViewAd mMixViewAd = AdLimeLoader.getMixViewAd(contextr, "広告枠 ID");
    View adView = mMixViewAd.getAdView();
    container.addView(adView);
} else {
    Log.d(TAG, "Ad isn't ready");
}
```

:::

::: tab Kotlin

```kotlin
if(AdLimeLoader.isMixViewAdReady("広告枠 ID")) {
    val mMixViewAd = AdLimeLoader.getMixViewAd(context, "広告枠 ID")
    val adView = mMixViewAd.adView
    container.addView(adView)
} else {
    println("Ad isn't ready")
}
```

:::

::::

## 広告のイベント  

AdListener を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### MixViewAd イベントを登録する  

MixViewAd のイベントを取得するには、`SimpleAdListener` インスタンスを作成し、`setAdListener()` で登録します。AdLimeLoader では 広告枠 ID ごとに広告を管理するため `getMixViewAd` メソッドで `MixViewAd` オブジェクトを取得し、そのオブジェクトにイベントを登録します。この処理は `loadMixViewAd` メソッド呼び出し前、または広告を表示する前に実行する必要があります。

:::: tabs

::: tab Java

```java
MixViewAd mMixViewAd = AdLimeLoader.getMixViewAd(context, "広告枠 ID");
mMixViewAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        // 広告のロード完了
        Log.d(TAG, "on MixViewAd Loaded");
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 広告の読み込み失敗、エラー詳細は adError から取得
        Log.d(TAG, "on MixViewAd FailedToLoad err: " + adError.toString());
    }

    @Override
    public void onAdShown() {
        // 広告を表示
        Log.d(TAG, "on MixViewAd Shown");
    }

    @Override
    public void onAdClicked() {
        // 広告をクリック
        Log.d(TAG, "on MixViewAd Clicked");
    }
});
```

:::

::: tab Kotlin

```kotlin
val mMixViewAd = AdLimeLoader.getMixViewAd(context, "広告枠 ID")
mMixViewAd.adListener = object: SimpleAdListener() {
    override fun onAdLoaded() {
        // 広告のロード完了
        println("on MixViewAd Loaded")
    }

    override fun onAdFailedToLoad(adError: AdError?) {
        //  広告の読み込み失敗、エラー詳細は adError から取得
        println("on MixViewAd FailedToLoad err: " + adError.toString())
    }

    override fun onAdShown() {
        //  広告を表示
        println("on MixViewAd Shown")
    }

    override fun onAdClicked() {
        //  広告をクリック
        println("on MixViewAd Clicked")
    }
}
```

:::

::::