# AdLimeLoader - MixFullScreenAd
 AdLimeLoaderで広告をロードまたは展示する時に、AdUnit IDによって広告をキャッシュする。そうすると各ページに広告をろーどまたは展示することをできる。<br>
同じAdUnit IDに対して，AdLimeLoader はオブジェクトを一つしかキャッシュしない。<br>
AdLimeLoader.destroyAd()で広告をデストロイすると、AdLimeLoaderで広告をロードする時は新たなオブジェクトを作成する。

AdLimeLoader はMixFullScreenAd のキャッシュ、ロード、展示、デストロイをサポートする。

### 広告のロード
```java
// ロード結果をモニターします
AdLimeLoader.getMixFullScreenAd(context, "MixFullScreen AdUnit ID").setAdListener(new SimpleAdListener() {
            @Override
            public void onAdLoaded() {
                // 広告のロード完了
            }

            @Override
            public void onAdFailedToLoad(AdError adError) {
                // 広告の読み込み失敗、エラー詳細は adError から取得
                Log.d(TAG, "onAdFailedToLoad: " + adError.toString());
            }

            @Override
            public void onAdShown() {
                // 広告を表示
            }

            @Override
            public void onAdClicked() {
                // 広告をクリック
            }

            @Override
            public void onAdClosed() {
                // 広告を閉じる
            }
        });
// 広告のロード
AdLimeLoader.loadMixFullScreenAd(context, "MixFullScreen AdUnit ID", nativeAdLayout);
```

**NativeAdLayoutについての情報は[NativeAdLayout](https://www.adlime.net/docs/ja/integration/android/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できる。**

::: tip
もし広告枠にFlurry/Unity Adsのバナー広告がある場合にloadMixFullScreenAd()にActivityを送る必要がある。<br>
もし広告枠にChartboost/Flurry/IronSource/Maio/Tapjoy/Unity Ads のインタースティシャル広告がある場合にloadMixFullScreenAd()にActivityを送る必要がある
:::

### 広告の用意を確認
```java
boolean isReady = AdLimeLoader.isMixFullScreenAdReady("MixFullScreen AdUnit ID");
```

### 広告の展示
```java
AdLimeLoader.showMixFullScreenAd("MixFullScreen AdUnit ID");
```

MixFullScreenAdは展示されると、backボタンをクリックするのは無効と黙認される。 showMixFullScreenAd(String adUnitId, boolean enableBack) を使える。

### 広告のデストロイ
```java
AdLimeLoader.destroyAd("MixFullScreen AdUnit ID");
```

### 获取 MixFullScreenAd 对象
AdLimeLoaderでキャッシュされる広告オブジェクトを取得できる 。<br>
このオブジェクトで広告をロードして展示する上記のAdLimeLoaderの方法ではない。 <br>
参考[MixFullScreenAd](./mixfullscreenad.md)。
```java
AdLimeLoader.getMixFullScreenAd(context, "MixFullScreen AdUnit ID");
```