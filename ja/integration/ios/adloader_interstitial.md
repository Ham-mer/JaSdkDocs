# AdLimeAdLoader - 插屏广告
AdLimeAdLoaderで広告をロード、展示する時、 AdUnit IDによって広告をキャッシュする，なので、各画面で広告のロードはできる。<br>
一つのAdUnit IDでは，AdLimeAdLoaderは一つの対象をキャッシュする。<br>
[AdLimeAdLoader destroyAd:@"AdUnit ID"] で広告をデストロイすると，AdLimeAdLoaderで広告をロードする時は新な対象を作成する

AdLimeAdLoaderはインタースティシャ広告のキャッシュ、ロード、展示、デストロイをサポートする。

### 広告のロード
```objectivec
// イベント代理の設置
[AdLimeAdLoader getInterstitialAd:@"Interstitial AdUnit ID"].delegate = self;
// 広告のロード
[AdLimeAdLoader loadInterstitialAd:@"Interstitial AdUnit ID"];
```

### 広告は用意できるかどうかの判断
```objectivec
BOOL isReady = [AdLimeAdLoader isInterstitialAdReady:@"Interstitial AdUnit ID"];
```

### 広告の展示
```objectivec
// 広告の展示
[AdLimeAdLoader showInterstitialAd:@"Interstitial AdUnit ID" viewController:self];
```

### 広告のデストロイ
```objectivec
[AdLimeAdLoader destroyAd:@"Interstitial AdUnit ID"];
```

### インタースティシャ広告対象の取得
AdLimeAdLoaderで広告対象を取得できる。<br>
この対象で広告をロード、展示、上記のAdlimeAdloaderで提供される方法ではない。<br>
[插屏广告]を参考(./Interstitial.md)。
```objectivec
AdLimeInterstitialAd *interstitialAd = [AdLimeAdLoader getInterstitialAd:@"Interstitial AdUnit ID"];
```