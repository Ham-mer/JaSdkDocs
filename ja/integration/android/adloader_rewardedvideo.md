# AdLimeLoader - 動画リワード広告  

AdLimeLoader は広告のキャッシュを管理、効率的に広告を表示する機能です。広告のキャッシュを管理することで、広告ロード回数を減らしたり、広告ロードのタイミングの効率化に望むことができます。

このガイドでは AdLimeLoader を用いた動画リワード広告の実装方法について説明します。

## AdLimeLoader による基本的な実装  

AdLimeLoader は各広告枠 ID ごとに広告のキャッシュを識別しています。AdLimeLoader を使って広告のロードや表示をする場合は、広告枠 ID ごとに広告をリクエストする必要があります。また一つの広告枠 ID に一つの広告を管理するため、複数の広告を同時に表示する際は対応する数の広告枠 ID を発行してください。

## RewardedVideoAd オブジェクトの取得  

AdLimeLoader を用いて広告を表示したり、広告のイベントを制御するなどのカスタマイズする必要がある場合は `RewardedVideoAd` オブジェクトを取得する必要があります。`RewardedVideoAd` を用いた実装方法は [動画リワード広告](./rewarded.md) を参考にしてください。

:::: tabs

::: tab Java

```java
RewardedVideoAd mRewardedVideoAd = AdLimeLoader.getRewardedVideo(context, "広告枠 ID");
```

:::

::: tab Kotlin

```kotlin
val mRewardedVideoAd = AdLimeLoader.getRewardedVideo(this, "広告枠 ID")
```

:::

::::

## 広告のロード  

まず、広告をロードしてみましょう。`AdLimeLoader`クラスの`loadRewardedVideo` を実行してください。

:::: tabs

::: tab Java

```java
AdLimeLoader.loadRewardedVideo(context, "広告枠 ID");
```

:::

::: tab Kotlin

```kotlin
AdLimeLoader.loadRewardedVideo(context, "広告枠 ID")
```

:::

::::

## 広告の表示  

広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `AdLimeLoader` の `isRewardedVideoReady` メソッドで確認してから `showRewardedVideo` メソッドで表示します。

:::: tabs

::: tab Java

```java
if(AdLimeLoader.isRewardedVideoReady("広告枠 ID")) {
    AdLimeLoader.showRewardedVideo(this, "広告枠 ID");
} else {
    Log.d(TAG, "Ad isn't ready");
}
```

:::

::: tab Kotlin

```kotlin
if(AdLimeLoader.isRewardedVideoReady("広告枠 ID")) {
    AdLimeLoader.showRewardedVideo(context, "広告枠 ID")
} else {
    println("Ad isn't ready")
}
```

:::

::::

## 広告のイベント  

AdListener を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### 動画リワード広告イベントを登録する  

動画リワード広告のイベントを取得するには、`RewardedVideoAdListener` インスタンスを作成し、`setAdListener()` で登録します。AdLimeLoader では 広告枠 ID ごとに広告を管理するため `getRewardedVideo` メソッドで `RewardedVideoAd` オブジェクトを取得し、そのオブジェクトにイベントを登録します。この処理は `loadRewardedVideo` メソッド呼び出し前、または広告を表示する前に実行する必要があります。

:::: tabs

::: tab Java

```java
RewardedVideoAd mRewardedVideoAd = AdLimeLoader.getRewardedVideo(context, "広告枠 ID");
mRewardedVideoAd.setAdListener(new SimpleRewardedVideoAdListener() {
    @Override
    public void onAdLoaded() {
        // 動画のロード完了
        Log.d(TAG, "onAdLoaded");
    }

    @Override
    public void onAdShown() {
        // 動画を表示
        Log.d(TAG, "onAdShown");
    }

    @Override
    public void onAdClicked() {
        // 動画をクリック
        Log.d(TAG, "onAdClicked");
    }

    @Override
    public void onAdClosed() {
        // 動画を閉じる
        Log.d(TAG, "onAdClosed");
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 動画の読み込み失敗
        LogUtil.d(TAG, "onAdFailedToLoad, " + adError);
    }

    @Override
    public void onVideoStarted() {
        // 動画の再生開始
        LogUtil.d(TAG, "onVideoStarted");
    }

    @Override
    public void onVideoCompleted() {
        // 動画の再生完了
        LogUtil.d(TAG, "onVideoCompleted");
    }

    @Override
    public void onRewarded(RewardedVideoAd.RewardItem rewardItem) {
        // リワードを獲得
        LogUtil.d(TAG, "onRewarded, " + rewardItem);
    }

    @Override
    public void onRewardFailed() {
        // リワード獲得失敗
        LogUtil.d(TAG, "onRewardFailed");
    }
});
```

:::

::: tab Kotlin

```kotlin
val mRewardedVideoAd = AdLimeLoader.getRewardedVideo(this, "広告枠 ID")
mRewardedVideoAd.adListener = object : SimpleAdListener() {
    override fun onAdLoaded() {
        // 動画のロード完了
        print("onAdLoaded")
    }

    override fun onAdShown() {
        //  広告を表示
        print("onAdShown")
    }

    override fun onAdClicked() {
        //  広告をクリック
        print("onAdClicked")
    }

    override fun onAdClosed() {
        //  広告を閉じる
        print("onAdClosed")
    }

    override fun onAdFailedToLoad(adError: AdError) {
        //  広告の読み込み失敗、エラー詳細は adError から取得
        print("onAdFailedToLoad: " + adError.toString())
    }

    override fun onVideoStarted() {
        // 動画の再生開始
        print("onVideoStarted")
    }

    override fun onVideoCompleted() {
        // 動画の再生完了
        print("onVideoCompleted")
    }

    override fun onRewarded(RewardedVideoAd.RewardItem rewardItem) {
        // リワードを獲得
        print("onRewarded, " + rewardItem)
    }

    override fun onRewardFailed() {
        // リワード獲得失敗
        print("onRewardFailed")
    }
}
```

:::

::::