# AdLimeLoader - インタースティシャル広告
AdLimeLoaderで広告をロードして展示する場合に、 AdUnit IDによって広告をキャッシュして各ページで広告をロードまたは展示する 。<br>
同じAdUnit IDの場合に，AdLimeLoaderはインスタンスを一つしかキャッシュしない。<br>
AdLimeLoader.destroyAd()で広告をデストロイすると、  AdLimeLoaderで広告を再ロードする時新たなインスタンスを作成する。

AdLimeLoaderはインタースティシャル広告のキャッシュ、ロード、展示、デストロイをサポートする。 

### 広告をロード
```java
// 広告をロード
AdLimeLoader.loadInterstitial(context, "Interstitial AdUnit ID");
```

```java
// 広告をロードしてまた結果をモニターする
AdLimeLoader.loadInterstitial(context, "Interstitial AdUnit ID", new SimpleAdListener() {
            @Override
            public void onAdLoaded() {
            }

            @Override
            public void onAdFailedToLoad(AdError adError) {
            }
        });
```

::: tip
もし広告枠に Chartboost/Flurry/IronSource/Maio/Tapjoy/Unity Adsがある場合に，loadInterstitial()に  Activityを送らないといけない。<br>
Nend/TikTokの場合に，loadInterstitial()に  Activityを送らないといけない、あるいは  showInterstitial(activity, ...) を使う。
:::

### 広告は準備完了かどうかの判断
```java
boolean isReady = AdLimeLoader.isInterstitialReady("Interstitial AdUnit ID");
```

### 広告の展示
```java
// 広告の展示
AdLimeLoader.showInterstitial("Interstitial AdUnit ID");
```

```java
// 広告を展示してまた結果をモニターする
AdLimeLoader.showInterstitial("Interstitial AdUnit ID", new SimpleAdListener() {
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