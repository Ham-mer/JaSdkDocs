# AdLimeAdLoader - 動画リワード広告  

AdLimeAdLoader は広告のキャッシュを管理、効率的に広告を表示する機能です。広告のキャッシュを管理することで、広告ロード回数を減らしたり、広告ロードのタイミングの効率化に望むことができます。

このガイドでは AdLimeAdLoader を用いた動画リワード広告の実装方法について説明します。

## AdLimeAdLoader による基本的な実装  

AdLimeAdLoader は各広告枠 ID ごとに広告のキャッシュを識別しています。AdLimeAdLoader を使って広告のロードや表示をする場合は、広告枠 ID ごとに広告をリクエストする必要があります。また一つの広告枠 ID に一つの広告を管理するため、複数の広告を同時に表示する際は対応する数の広告枠 ID を発行してください。

## AdLimeRewardedVideoAd オブジェクトの取得  

AdLimeAdLoader を用いて広告のイベントを制御するなどのカスタマイズする必要がある場合は `AdLimeRewardedVideoAd` オブジェクトを取得する必要があります。`AdLimeRewardedVideoAd` を用いた実装方法は [動画リワード広告](./rewarded.md) を参考にしてください。

:::: tabs

::: tab Objective-C

```objectivec
AdLimeRewardedVideoAd *rewardedVideoAd = [AdLimeAdLoader getRewardedVideoAd:@"広告枠 ID"];
```

:::

::: tab Swift

```swift
let rewardedVideoAd = AdLimeAdLoader.getRewardedVideoAd("広告枠 ID")
```

:::

::::

## 広告のロード  

まず、広告をロードしてみましょう。`AdLimeAdLoader`クラスの`loadRewardedVideoAd` を実行してください。

:::: tabs

::: tab Objective-C

```objectivec
[AdLimeAdLoader loadRewardedVideoAd:@"広告枠 ID"];
```

:::

::: tab Swift

```swift
AdLimeAdLoader.loadRewardedVideoAd("広告枠 ID")
```

:::

::::

## 広告の表示  

広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `AdLimeAdLoader` の `isRewardedVideoAdReady` メソッドで確認してから `showRewardedVideoAd` メソッドで表示します。

:::: tabs

::: tab Objective-C

```objectivec
if([AdLimeAdLoader isRewardedVideoAdReady:@"広告枠 ID"]){
    [AdLimeAdLoader showRewardedVideoAd:@"広告枠 ID" viewController:self];
} else {
    NSLog(@"Ad wasn't ready");
}
```

:::

::: tab Swift

```swift
if(AdLimeAdLoader.isRewardedVideoAdReady("広告枠 ID")){
    AdLimeAdLoader.showRewardedVideoAd("広告枠 ID", viewController: self)
} else {
    print("Ad wasn't ready")
}
```

:::

::::

## 広告のイベント  

`AdLimeRewardedVideoAdDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### 動画リワード広告イベントを登録する  

動画リワード広告のライフサイクルイベントを取得するためには `AdLimeRewardedVideoAdDelegate` を継承します。 AdLimeAdLoader では 広告枠 ID ごとに広告を管理するため `getRewardedVideoAd` メソッドで `AdLimeRewardedVideoAd` オブジェクトを取得し、そのオブジェクトに継承します。この処理は `loadRewardedVideoAd` メソッド及び `showRewardedVideoAd` メソッドを呼び出す前に実行する必要があります。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController () <AdLimeRewardedVideoAdDelegate>

@property(nonatomic, strong) AdLimeRewardedVideoAd *rewardedVideoAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    AdLimeRewardedVideoAd *rewardedVideoAd = [AdLimeAdLoader getRewardedVideoAd:@"広告枠 ID"];
    rewardedVideoAd.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController, AdLimeRewardedVideoAdDelegate {

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        let rewardedVideoAd:AdLimeRewardedVideoAd = AdLimeAdLoader.getRewardedVideoAd("広告枠 ID")
        rewardedVideoAd.delegate = self
    }
}
```

:::

::::


### 動画リワード広告イベントを実装する
広告イベントの制御は `AdLimeRewardedVideoAdDelegate` を用いて実現できます。実装方法は[動画リワード広告イベントを実装する](./rewarded.md#動画リワード広告イベントを実装する)を確認してください

