# AdLimeLoader - ネイティブ広告
AdLimeLoaderで広告をロードして展示する場合に、 AdUnit IDによって広告をキャッシュして各ページで広告をロードまたは展示する。<br>
同じAdUnit IDの場合に，AdLimeLoaderはインスタンスを一つしかキャッシュしない。<br>
AdLimeLoader.destroyAd()で広告をデストロイすると、  AdLimeLoaderで広告を再ロードする時新たなインスタンスを作成する。

AdLimeLoaderはネイティブ広告のキャッシュ、ロード、展示、デストロイをサポートする。

### 広告をロード
```java
// ロード結果をモニターします
AdLimeLoader.getNativeAd(this, "Native AdUnit ID").setAdListener(new SimpleAdListener() {
            @Override
            public void onAdLoaded() {
                // 広告のロード完了
            }

            @Override
            public void onAdFailedToLoad(AdError adError) {
                // 広告の読み込み失敗
                Log.d(TAG, "on BannerAd FailedToLoad err:" + adError.toString());
            }

            @Override
            public void onAdClicked() {
                // 広告をクリック
                Log.d(TAG, "on BannerAd Clicked");
            }

            @Override
            public void onAdShown() {
                // 広告を表示
                Log.d(TAG, "on BannerAd Shown");
            }

            @Override
            public void onAdClosed() {
                // 広告を閉じる
                Log.d(TAG, "on BannerAd Closed");
            }
        });
// 広告をロード
AdLimeLoader.loadNativeAd(context, "Native AdUnit ID", nativeAdLayout);
```

広告をロードする時にNativeAdLayoutないのloadNativeAd()を調達するが、広告を展示する時に NativeAdLayoutがあるshowNativeAd()を調達する。

**NativeAdLayoutに関する情報は [NativeAdLayout](https://www.adlime.net/docs/ja/integration/android/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できる。**

### 広告は準備完了かどうかの判断
```java
boolean isReady = AdLimeLoader.isNativeAdReady("Native AdUnit ID");
```

### 広告の展示
ネイティブ広告はViewGroupで展示される。

```java
viewGroup.removeAllViews();
AdLimeLoader.showNativeAd("Native AdUnit ID", viewGroup);
```

### 広告のデストロイ
```java
AdLimeLoader.destroyAd("Native AdUnit ID");
```

### ネイティブ広告のインスタンスの取得
AdLimeLoaderでキャッシュされる広告のインスタンスを取得できる。<br>
これを使って広告をロードまた展示する、上記のADLimeLoaderで提供される方法ではない。<br>
参考[ネイティブ広告](./native.md)。
```java
NativeAd nativeAd = AdLimeLoader.getNativeAd(context, "Native AdUnit ID");
```