# AdLimeLoader - バナー広告
AdLimeLoaderで広告をロードして展示する場合に、 AdUnit IDによって広告をキャッシュして各ページで広告をロードまたは展示する 。<br>
同じAdUnit IDの場合に，AdLimeLoaderはインスタンスを一つしかキャッシュしない。 <br>
 AdLimeLoader.destroyAd()で広告をデストロイすると、  AdLimeLoaderで広告を再ロードする時新たなインスタンスを作成する。 

AdLimeLoaderはバナー広告のキャッシュ、ロード、展示、デストロイをサポートする。 

### 広告のロード
```java
// 広告のロード
AdLimeLoader.loadBanner(context, "Banner AdUnit ID");
```

```java
// 広告をロードしてまた結果をモニターする
AdLimeLoader.loadBanner(context, "Banner AdUnit ID", new SimpleAdListener() {
            @Override
            public void onAdLoaded() {
            }

            @Override
            public void onAdFailedToLoad(AdError adError) {
            }
        });
```

::: tip
もし広告枠に Flurry/IronSource/Unity Adsがある場合に，loadBanner() に Activityを送らないといけない。
:::

### 広告は準備完了かどうかの判断
```java
boolean isReady = AdLimeLoader.isBannerReady("Banner AdUnit ID");
```

### 広告の展示
バナー広告は ViewGroupで展示される 。

```java
// 広告の展示
viewGroup.removeAllViews();
AdLimeLoader.showBanner("Banner AdUnit ID", viewGroup);
```

```java
// 広告を展示してまた結果をモニターする
viewGroup.removeAllViews();
AdLimeLoader.showBanner("Banner AdUnit ID", viewGroup, new SimpleAdListener() {
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

### 広告をデストロイする
```java
AdLimeLoader.destroyAd("Banner AdUnit ID");
```

### バナー広告のインスタンスの取得
 AdLimeLoaderでキャッシュされる広告のインスタンスを取得できる。 <br>
これを使って広告をロードまた展示する、上記のADLimeLoaderで提供される方法でなはい。<br>
参考[バナー広告](./banner.md)。
```java
BannerAdView bannerAdView = AdLimeLoader.getBanner(context, "Banner AdUnit ID");
```