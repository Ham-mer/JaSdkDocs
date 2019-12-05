# AdLimeLoader - 動画リワード
AdLimeLoaderで広告をロードして展示する場合に、 AdUnit IDによって広告をキャッシュして各ページで広告をロードまたは展示する。<br>
同じAdUnit IDの場合に，AdLimeLoaderはインスタンスを一つしかキャッシュしない。<br>
AdLimeLoader.destroyAd()で広告をデストロイすると、  AdLimeLoaderで広告を再ロードする時新たなインスタンスを作成する。

AdLimeLoaderは動画リワードのキャッシュ、ロード、展示、デストロイをサポートする。

### 広告をロード
```java
// 広告をロード
AdLimeLoader.loadRewardedVideo(context, "RewardedVideo AdUnit ID");
```

```java
// 広告をロードしてまた結果をモニターする
AdLimeLoader.loadRewardedVideo(context, "RewardedVideo AdUnit ID", new SimpleRewardedVideoAdListener() {
            @Override
            public void onAdLoaded() {
            }

            @Override
            public void onAdFailedToLoad(AdError adError) {
            }
        });
```

::: tip
もし広告枠に Chartboost/Flurry/IronSource/Maio/MoPub/Tapjoy/Unity Adsがある場合に，loadRewardedVideo()にActivityを送らいないといけない。<br>
Nend/TikTokの場合に，loadRewardedVideo() にActivityを送らいないといけない、あるいはshowRewardedVideo(activity, ...)を使って広告を展示する。
:::

### 広告は準備完了かどうかの判断
```java
boolean isReady = AdLimeLoader.isRewardedVideoReady("RewardedVideo AdUnit ID");
```

### 広告の展示
```java
// 広告の展示
AdLimeLoader.showRewardedVideo("RewardedVideo AdUnit ID");
```

```java
// 広告をロードしてまた結果をモニターする
AdLimeLoader.showRewardedVideo("RewardedVideo AdUnit ID", new SimpleRewardedVideoAdListener() {
            @Override
            public void onAdShown() {
            }

            @Override
            public void onAdClicked() {
            }

            @Override
            public void onAdClosed() {
            }
        });
```

::: tip
 Nend/TikTokの場合に，loadRewardedVideo()にActivityを送らいないといけない、あるいはshowRewardedVideo(activity, ...)で広告を展示する。
:::

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