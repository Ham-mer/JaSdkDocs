# AdLimeLoader - MixViewAd
AdLimeLoaderで広告をロードまたは展示する時に、AdUnit IDによって広告をキャッシュする。そうすると各ページに広告をろーどまたは展示することをできる。<br>
同じAdUnit IDに対して，AdLimeLoader はオブジェクトを一つしかキャッシュしない。<br>
AdLimeLoader.destroyAd()で広告をデストロイすると、AdLimeLoaderで広告をロードする時は新たなオブジェクトを作成する。

AdLimeLoader はMixViewAd のキャッシュ、ロード、展示、デストロイをサポートする。

### 広告のロード
```java
// 広告のロード
AdLimeLoader.loadMixViewAd(context, "MixView AdUnit ID", nativeAdLayout);
```

```java
// 広告をロードして結果をモニターする
AdLimeLoader.loadMixViewAd(context, "MixView AdUnit ID", nativeAdLayout, new SimpleAdListener() {
            @Override
            public void onAdLoaded() {
            }

            @Override
            public void onAdFailedToLoad(AdError adError) {
            }
        });
```

広告をロードする時に NativeAdLayoutのパラメーターがない loadMixViewAd()を調達する、広告を展示する時にNativeAdLayoutのパラメーターがない loadMixViewAd()を調達する。

**NativeAdLayoutについての情報は[NativeAdLayout](https://www.adlime.net/docs/ja/integration/android/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できる。**

::: tip
もし広告枠に360/Flurry/Tencent Social Ads/Unity Adsのバナー広告がある場合にloadMixViewAd()にActivityを送る必要がある<br>
もし広告枠に4399/Aligames/vivo のネイティブ広告がある場合にloadMixViewAd()にActivityを送る必要がある
:::

### 広告の用意を確認
```java
boolean isReady = AdLimeLoader.isMixViewAdReady("MixView AdUnit ID");
```

### 広告の展示
MixViewAd は ViewGroupに展示される 。

```java
viewGroup.removeAllViews();
AdLimeLoader.showMixViewAd("MixView AdUnit ID", viewGroup);
```

```java
// 広告を展示して結果をモニターする
viewGroup.removeAllViews();
AdLimeLoader.showMixViewAd("MixView AdUnit ID", viewGroup, new SimpleAdListener() {
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

### 広告のデストロイ
```java
AdLimeLoader.destroyAd("MixView AdUnit ID");
```

###  MixViewAdのオブジェクトを取得
AdLimeLoaderでキャッシュされる広告オブジェクトを取得できる 。。<br>
上記のAdLimeLoaderの方法ではなくてこのオブジェクトでも広告をロードして展示できる <br>
参考[MixViewAd](./mixviewad.md)。
```java
AdLimeLoader.getMixViewAd(context, "MixView AdUnit ID");
```