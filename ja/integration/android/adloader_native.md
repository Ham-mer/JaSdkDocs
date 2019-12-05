# AdLimeLoader - ネイティブ広告
AdLimeLoaderで広告をロードして展示する場合に、 AdUnit IDによって広告をキャッシュして各ページで広告をロードまたは展示する。<br>
同じAdUnit IDの場合に，AdLimeLoaderはインスタンスを一つしかキャッシュしない。<br>
AdLimeLoader.destroyAd()で広告をデストロイすると、  AdLimeLoaderで広告を再ロードする時新たなインスタンスを作成する。

AdLimeLoaderはネイティブ広告のキャッシュ、ロード、展示、デストロイをサポートする。

### 広告をロード
```java
// 広告をロード
AdLimeLoader.loadNativeAd(context, "Native AdUnit ID", nativeAdLayout);
```

```java
// 広告をロードしてまた結果をモニターする
AdLimeLoader.loadNativeAd(context, "Native AdUnit ID", nativeAdLayout, new SimpleAdListener() {
            @Override
            public void onAdLoaded() {
            }

            @Override
            public void onAdFailedToLoad(AdError adError) {
            }
        });
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

```java
// 広告を展示してまた結果をモニターする
viewGroup.removeAllViews();
AdLimeLoader.showNativeAd("Native AdUnit ID", viewGroup, new SimpleAdListener() {
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
AdLimeLoader.destroyAd("Native AdUnit ID");
```

### ネイティブ広告のインスタンスの取得
AdLimeLoaderでキャッシュされる広告のインスタンスを取得できる。<br>
これを使って広告をロードまた展示する、上記のADLimeLoaderで提供される方法ではない。<br>
参考[ネイティブ広告](./native.md)。
```java
NativeAd nativeAd = AdLimeLoader.getNativeAd(context, "Native AdUnit ID");
```