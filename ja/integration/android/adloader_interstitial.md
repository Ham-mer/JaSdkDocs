# AdLimeLoader - インタースティシャル広告
AdLimeLoaderで広告をロードして展示する場合に、 AdUnit IDによって広告をキャッシュして各ページで広告をロードまたは展示する 。<br>
同じAdUnit IDの場合に，AdLimeLoaderはインスタンスを一つしかキャッシュしない。<br>
AdLimeLoader.destroyAd()で広告をデストロイすると、  AdLimeLoaderで広告を再ロードする時新たなインスタンスを作成する。

AdLimeLoaderはインタースティシャル広告のキャッシュ、ロード、展示、デストロイをサポートする。 

### 広告をロード
```java
// ロード結果をモニターします
AdLimeLoader.getInterstitial(context, "Interstitial AdUnit ID").setAdListener(new SimpleAdListener() {
            @Override
            public void onAdLoaded() {
                // 広告のロード完了
            }

            @Override
            public void onAdFailedToLoad(AdError adError) {
                // 広告の読み込み失敗、エラー詳細は adError から取得
                Log.d(TAG, "on BannerAd FailedToLoad err:" + adError.toString());
            }

            @Override
            public void onAdShown() {
                // 広告を表示
                Log.d(TAG, "on BannerAd Shown");
            }

            @Override
            public void onAdClicked() {
                // 広告をクリック
                Log.d(TAG, "on BannerAd Clicked");
            }

            @Override
            public void onAdClosed() {
                // 広告を閉じる
                Log.d(TAG, "on BannerAd Closed");
            }
        });
// 広告をロード
AdLimeLoader.loadInterstitial(context, "Interstitial AdUnit ID");
```

::: tip
もし広告枠に Chartboost/Flurry/IronSource/Maio/Tapjoy/Unity Adsがある場合に，loadInterstitial()に  Activityを送らないといけない。
:::

### 広告は準備完了かどうかの判断
```java
boolean isReady = AdLimeLoader.isInterstitialReady("Interstitial AdUnit ID");
```

### 広告の展示
```java
// 広告の展示
AdLimeLoader.showInterstitial(activity, "Interstitial AdUnit ID");
```

::: tip
Nend/TikTokの場合に，loadInterstitial()に  Activityを送らないといけない、あるいは  showInterstitial(activity, ...) を使う。
:::

### 広告をデストロイする
```java
AdLimeLoader.destroyAd("Interstitial AdUnit ID");
```

### インタースティシャル広告のインスタンスの取得
AdLimeLoaderでキャッシュされる広告のインスタンスを取得できる。<br>
これを使って広告をロードまた展示する、上記のADLimeLoaderで提供される方法ではない。<br>
参考[インタースティシャル広告](./Interstitial.md)。
```java
InterstitialAd interstitialAd = AdLimeLoader.getInterstitial(context, "Interstitial AdUnit ID");
```