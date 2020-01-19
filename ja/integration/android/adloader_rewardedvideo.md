# AdLimeLoader - 動画リワード
AdLimeLoaderで広告をロードして展示する場合に、 AdUnit IDによって広告をキャッシュして各ページで広告をロードまたは展示する。<br>
同じAdUnit IDの場合に，AdLimeLoaderはインスタンスを一つしかキャッシュしない。<br>
AdLimeLoader.destroyAd()で広告をデストロイすると、  AdLimeLoaderで広告を再ロードする時新たなインスタンスを作成する。

AdLimeLoaderは動画リワードのキャッシュ、ロード、展示、デストロイをサポートする。

### 広告をロード
```java
// ロード結果をモニターします
AdLimeLoader.getRewardedVideo(this, "RewardedVideo AdUnit ID").setAdListener(new SimpleRewardedVideoAdListener() {
            @Override
            public void onAdLoaded() {
                // 動画のロード完了
                LogUtil.d(TAG, "onAdLoaded");
            }

            @Override
            public void onAdShown() {
                // 動画を表示
                LogUtil.d(TAG, "onAdShown");
            }

            @Override
            public void onAdClicked() {
                // 動画をクリック
                LogUtil.d(TAG, "onAdClicked");
            }

            @Override
            public void onAdClosed() {
                // 動画を閉じる
                LogUtil.d(TAG, "onAdClosed");
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
// 広告をロード
AdLimeLoader.loadRewardedVideo(context, "RewardedVideo AdUnit ID");
```

::: tip
もし広告枠に Chartboost/Flurry/IronSource/Maio/MoPub/Tapjoy/Unity Adsがある場合に，ContextのパラメーターにActivityを導入してください。
:::

### 広告は準備完了かどうかの判断
```java
boolean isReady = AdLimeLoader.isRewardedVideoReady("RewardedVideo AdUnit ID");
```

### 広告の展示
```java
// 広告の展示
AdLimeLoader.showRewardedVideo(activity, "RewardedVideo AdUnit ID");
```

### 広告のデストロイ
```java
AdLimeLoader.destroyAd("RewardedVideo AdUnit ID");
```

### 動画リワードのインスタンスの取得
AdLimeLoaderでキャッシュされる広告のインスタンスを取得できる。<br>
これを使って広告をロードまた展示する、上記のADLimeLoaderで提供される方法ではない。<br>
参考[動画リワード](./rewarded.md)。
```java
RewardedVideoAd rewardedVideoAd = AdLimeLoader.getRewardedVideo(context, "RewardedVideo AdUnit ID");
```