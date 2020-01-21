# AdLimeAdLoader - MixViewAd
AdLimeAdLoaderで広告をロード、展示する時、 AdUnit IDによって広告をキャッシュする，なので、各画面で広告のロードはできる。<br>
一つのAdUnit IDでは，AdLimeAdLoaderは一つの対象をキャッシュする。<br>
[AdLimeAdLoader destroyAd:@"AdUnit ID"]で広告をデストロイすると，AdLimeAdLoaderで広告をロードする時は新な対象を作成する。

AdLimeAdLoader はMixViewAdのキャッシュ、ロード、展示、デストロイをサポートする。

### 広告のロード
```objectivec
// イベント代理の設置
[AdLimeAdLoader getMixViewAd:@"MixView AdUnit ID" rootViewController:self].delegate = self;
// 広告のロード
[AdLimeAdLoader loadMixViewAd:@"MixView AdUnit ID" rootViewController:self nativeAdLayout:self.layout];
```

広告をロードする時に NativeAdLayoutのパラメーターのない loadMixViewAdを使えるが、広告を展示する時はNativeAdLayoutがついているshowMixViewAdを使う。

**NativeAdLayoutについて [NativeAdLayout](https://www.adlime.net/docs/zh/integration/ios/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認ください。**

### 広告は用意できるかどうかの判断
```objectivec
BOOL isReady = [AdLimeAdLoader isMixViewAdReady:@"MixView AdUnit ID"];
```

### 広告の展示
MixViewAd はViewContainerで展示されるはずだ 。

```objectivec
[AdLimeAdLoader showMixViewAd:@"MixView AdUnit ID" container:self.viewContainer];
```

### 広告のデストロイ
```objectivec
[AdLimeAdLoader destroyAd:@"MixView AdUnit ID"];
```

### MixViewAd対象の取得
AdLimeAdLoaderで広告対象を取得できる。<br>
この対象で広告をロード、展示、上記のAdlimeAdloaderで提供される方法ではない。<br>
[MixViewAd]を参考(./mixviewad.md)。
```objectivec
[AdLimeAdLoader getMixViewAd:@"MixView AdUnit ID" rootViewController:self];
```