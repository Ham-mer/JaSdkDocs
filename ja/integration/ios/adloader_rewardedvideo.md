# AdLimeAdLoader - 動画リワード
AdLimeAdLoaderで広告をロード、展示する時、 AdUnit IDによって広告をキャッシュする，なので、各画面で広告のロードはできる。<br>
一つのAdUnit IDでは，AdLimeAdLoaderは一つの対象をキャッシュする。<br>
[AdLimeAdLoader destroyAd:@"RewardedVideo AdUnit ID"]で広告をデストロイすると，AdLimeAdLoaderで広告をロードする時は新な対象を作成する。

AdLimeAdLoaderは動画リワードののキャッシュ、ロード、展示、デストロイをサポートする。

### 広告のロード
```objectivec
// イベント代理の設置
[AdLimeAdLoader getRewardedVideoAd:@"RewardedVideo AdUnit ID"].delegate = self;
// 広告のロード
[AdLimeAdLoader loadRewardedVideoAd:@"RewardedVideo AdUnit ID"];
```

### 広告は用意できるかどうかの判断
```objectivec
BOOL isReady = [AdLimeAdLoader isRewardedVideoAdReady:@"RewardedVideo AdUnit ID"];
```

### 広告の展示
```objectivec
// 広告の展示
[AdLimeAdLoader showRewardedVideoAd:@"RewardedVideo AdUnit ID" viewController:self];
```

### 広告のデストロイ
```objectivec
[AdLimeAdLoader destroyAd:@"RewardedVideo AdUnit ID"];
```

### 動画リワード広告対象の取得
AdLimeAdLoaderで広告対象を取得できる。<br>
この対象で広告をロード、展示、上記のAdlimeAdloaderで提供される方法ではない。<br>
[激励视频]を参考(./rewarded.md)。
```objectivec
[AdLimeAdLoader getRewardedVideoAd:@"RewardedVideo AdUnit ID"];
```