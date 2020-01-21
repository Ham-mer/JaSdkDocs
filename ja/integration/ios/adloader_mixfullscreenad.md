# AdLimeAdLoader - MixFullScreenAd
AdLimeAdLoaderで広告をロード、展示する時、 AdUnit IDによって広告をキャッシュする，なので、各画面で広告のロードはできる。<br>
一つのAdUnit IDでは，AdLimeAdLoaderは一つの対象をキャッシュする。<br>
[AdLimeAdLoader destroyAd:@"AdUnit ID"] で広告をデストロイすると，AdLimeAdLoaderで広告をロードする時は新な対象を作成する。

AdLimeAdLoader はMixFullScreenAdのキャッシュ、ロード、展示、デストロイをサポートする。

### 広告のロード
```objectivec
// イベント代理の設置
[AdLimeAdLoader getMixFullScreenAd:@"MixFullScreen AdUnit ID"].delegate = self;
// 広告のロード
[AdLimeAdLoader loadMixFullScreenAd:@"MixFullScreen AdUnit ID" nativeAdLayout:self.layout];
```

** NativeAdLayoutについて[NativeAdLayout](https://www.adlime.net/docs/zh/integration/ios/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認ください。**

### 広告は用意できるかどうかの判断
```objectivec
BOOL isReady = [AdLimeAdLoader isMixFullScreenAdReady@"MixFullScreen AdUnit ID"];
```

### 広告の展示
```objectivec
[AdLimeAdLoader showMixFullScreenAd:@"MixFullScreen AdUnit ID" viewController:self];
```

### 広告のデストロイ
```objectivec
[AdLimeAdLoader destroyAd:@"MixFullScreen AdUnit ID"];
```

### MixFullScreenAd 対象の取得
AdLimeAdLoaderで広告対象を取得できる。<br>
この対象で広告をロード、展示、上記のAdlimeAdloaderで提供される方法ではない<br>
[MixFullScreenAd]を参考(./mixfullscreenad.md)。
```objectivec
[AdLimeAdLoader getMixFullScreenAd:@"MixFullScreen AdUnit ID"];
```