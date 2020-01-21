# AdLimeAdLoader - 横幅广告
AdLimeAdLoaderで広告をロード、展示する時、 AdUnit IDによって広告をキャッシュする，なので、各画面で広告のロードはできる。<br>
一つのAdUnit IDでは，AdLimeAdLoaderは一つの対象をキャッシュする。<br>
[AdLimeAdLoader destroyAd:@"Banner AdUnit ID"] で広告をデストロイすると，AdLimeAdLoaderで広告をロードする時は新な対象を作成する。

AdLimeAdLoaderはバナー広告のキャッシュ、ロード、展示、デストロイをサポートする。

### 広告のロード
```objectivec
// イベント代理の設置
[AdLimeAdLoader getBannerAdView:@"Banner AdUnit ID" rootViewController:self].delegate = self;
// 広告のロード
[AdLimeAdLoader loadBanner:@"Banner AdUnit ID" rootViewController:self];
```

### 広告は用意できるかどうかの判断
```objectivec
BOOL isReady = [AdLimeAdLoader isBannerReady:@"Banner AdUnit ID"];
```

### 広告の展示
バナー広告はViewContainerで展示される。

```objectivec
// 広告の展示
[AdLimeAdLoader showBanner:@"Banner AdUnit ID" container:self.container];
```

### 広告のデストロイ
```objectivec
[AdLimeAdLoader destroyAd:@"Banner AdUnit ID"];
```

### バナー広告対象の取得
AdLimeAdLoaderで広告対象を取得できる。<br>
この対象で広告をロード、展示、上記のAdlimeAdloaderで提供される方法ではない。<br>
[横幅广告]を参考(./banner.md)。
```objectivec
AdLimeBannerAdView *bannerAdView = [AdLimeAdLoader getBannerAdView:@"Banner AdUnit ID" rootViewController:self];
```