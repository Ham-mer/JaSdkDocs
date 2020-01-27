# AdLimeAdLoader - インタースティシャル広告  

AdLimeAdLoader は広告のキャッシュを管理、効率的に広告を表示する機能です。広告のキャッシュを管理することで、広告ロード回数を減らしたり、広告ロードのタイミングの効率化に望むことができます。

このガイドでは AdLimeAdLoader を用いたインタースティシャル広告の実装方法について説明します。

## AdLimeAdLoader による基本的な実装  

AdLimeAdLoader は各広告枠 ID ごとに広告のキャッシュを識別しています。AdLimeAdLoader を使って広告のロードや表示をする場合は、広告枠 ID ごとに広告をリクエストする必要があります。また一つの広告枠 ID に一つの広告を管理するため、複数の広告を同時に表示する際は対応する数の広告枠 ID を発行してください。

## AdLimeInterstitialAd オブジェクトの取得  

AdLimeAdLoader を用いて広告のイベントを制御するなどのカスタマイズする必要がある場合は `AdLimeInterstitialAd` オブジェクトを取得する必要があります。`AdLimeInterstitialAd`を用いた実装方法は[インタースティシャル広告](./interstitial.md)を参考にしてください。

:::: tabs

::: tab Objective-C

```objectivec
AdLimeInterstitialAd *interstitialAd = [AdLimeAdLoader getInterstitialAd:@"広告枠 ID"];
```

:::

::: tab Swift

```swift
let interstitialAd = AdLimeAdLoader.getInterstitialAd("広告枠 ID")
```

:::

::::

## 広告のロード  

まず、広告をロードしてみましょう。`AdLimeAdLoader`クラスの`loadInterstitialAd` を実行してください。

:::: tabs

::: tab Objective-C

```objectivec
[AdLimeAdLoader loadInterstitialAd:@"広告枠 ID"];
```

:::

::: tab Swift

```swift
AdLimeAdLoader.loadInterstitialAd("広告枠 ID")
```

:::

::::

## 広告の表示  

広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `AdLimeAdLoader` の `isInterstitialAdReady` メソッドで確認してから `showInterstitialAd` メソッドで表示します。

:::: tabs

::: tab Objective-C

```objectivec
if([AdLimeAdLoader isInterstitialAdReady:@"広告枠 ID"]) {
    [AdLimeAdLoader showInterstitialAd:@"広告枠 ID" viewController:self]
} else {
    NSLog(@"Ad wasn't ready");
}
```

:::

::: tab Swift

```swift
if(AdLimeAdLoader.isInterstitialAdReady("広告枠 ID")){
    AdLimeAdLoader.showInterstitialAd("広告枠 ID", viewController: self)
} else {
    print("Ad wasn't ready")
}
```

:::

::::

## 広告のイベント  

`AdLimeInterstitialAdDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### インタースティシャル広告イベントを登録する  

インタースティシャル広告のライフサイクルイベントを取得するためには `AdLimeInterstitialAdDelegate` を継承します。 AdLimeAdLoader では 広告枠 ID ごとに広告を管理するため `getInterstitialAd` メソッドで `AdLimeInterstitialAd` オブジェクトを取得し、そのオブジェクトに継承します。この処理は `loadInterstitialAd` メソッドまたは `showInterstitialAd` メソッドを呼び出す前に実行する必要があります。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController () <AdLimeInterstitialAdDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    AdLimeInterstitialAd *interstitialAd = [AdLimeAdLoader getInterstitialAd:@"広告枠 ID"];
    intersititalAd.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController, AdLimeInterstitialAdDelegate {

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        let interstitialAd = AdLimeAdLoader.getInterstitialAd("広告枠 ID")
        interstitialAd.delegate = self
    }
}
```

:::

::::


### インタースティシャル広告イベントを実装する
広告イベントの制御は `AdLimeInterstitialAdDelegate` を用いて実現できます。実装方法は[インタースティシャル広告イベントを実装する](./interstitial.md#インタースティシャル広告イベントを実装する)を確認してください
