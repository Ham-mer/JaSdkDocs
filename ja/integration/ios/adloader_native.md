# AdLimeAdLoader - ネイティブ広告
AdLimeAdLoaderで広告をロード、展示する時、 AdUnit IDによって広告をキャッシュする，なので、各画面で広告のロードはできる。。<br>
一つのAdUnit IDでは，AdLimeAdLoaderは一つの対象をキャッシュする。<br>
[AdLimeAdLoader destroyAd:@"Native AdUnit ID"]で広告をデストロイすると，AdLimeAdLoaderで広告をロードする時は新な対象を作成する。

AdLimeAdLoader はネイティブ広告のキャッシュ、ロード、展示、デストロイをサポートする。

### 広告のロード
```objectivec
// 広告のロード
[AdLimeAdLoader loadNativeAd:@"Native AdUnit ID"];
```

```objectivec
// 広告のロードまたはレイアウトに導入
[AdLimeAdLoader loadNativeAd:@"Native AdUnit ID" withLayout:(AdLimeNativeAdLayout *)layout andDelegate:(id<AdLimeNativeAdDelegate> )delegate];
```

広告をロードする時に NativeAdLayoutのパラメーターのないloadNativeAdを使えるが，広告を展示する時はNativeAdLayoutがついているshowNativeAd()を使う。

**NativeAdLayoutについて [NativeAdLayout](https://www.adlime.net/docs/zh/integration/ios/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認ください。**


### 広告は用意できるかどうかの判断
```objectivec
BOOL isReady = [AdLimeAdLoader isNativeAdReady:@"Native AdUnit ID"];
```

### 広告の展示
ネイティブ広告はViewContainerで展示される。

```objectivec
[AdLimeAdLoader showNativeAd:@"Native AdUnit ID"  viewContainer: (UIView *)viewContainer];
```

```objectivec
// 広告の展示またはイベント代理の設定
[AdLimeAdLoader showNativeAd:@"Native AdUnit ID" viewContainer: (UIView *)viewContainer withDelegate:(id<AdLimeNativeAdDelegate>)delegate];
```

### 広告のデストロイ
```objectivec
[AdLimeAdLoader destroyAd:@"Native AdUnit ID"];
```

### ネイティブ広告対象の取得
AdLimeAdLoaderで広告対象を取得できる。<br>
この対象で広告をロード、展示、上記のAdlimeAdloaderで提供される方法ではない。<br>
[ネイティブ広告]を参考(./native.md)。
```objectivec
[AdLimeAdLoader getNativeAd:@"Native AdUnit ID"];
```
