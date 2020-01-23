# AdLimeAdLoader - バナー広告  

AdLimeAdLoader は広告のキャッシュを管理、効率的に広告を表示する機能です。広告のキャッシュを管理することで、広告ロード回数を減らしたり、広告ロードのタイミングの効率化に望むことができます。

このガイドでは AdLimeAdLoader を用いたバナー広告の実装方法について説明します。

## AdLimeAdLoader による基本的な実装  

AdLimeAdLoader は各広告枠 ID ごとに広告のキャッシュを識別しています。AdLimeAdLoader を使って広告のロードや表示をする場合は、広告枠 ID ごとに広告をリクエストする必要があります。また一つの広告枠 ID に一つの広告を管理するため、複数の広告を同時に表示する際は対応する数の広告枠 ID を発行してください。

## AdLimeBannerView オブジェクトの取得  

AdLimeAdLoader を用いて広告を表示したり、広告のイベントを制御するなどのカスタマイズする必要がある場合は `AdLimeBannerView` オブジェクトを取得する必要があります。`AdLimeBannerView` を用いた実装方法は [バナー広告](./banner.md) を参考にしてください。

:::: tabs

::: tab Objective-C

```objectivec
AdLimeBannerAdView *bannerAdView = [AdLimeAdLoader getBannerAdView:@"広告枠 ID" rootViewController: self];
```

:::

::: tab Swift

```swift
let bannerView = AdLimeAdLoader.getBannerAdView("広告枠 ID", rootViewController: self)
```

:::

::::

## 広告のロード  

まず、広告をロードしてみましょう。`AdLimeAdLoader`クラスの`loadBanner` を実行してください。

:::: tabs

::: tab Objective-C

```objectivec
[AdLimeAdLoader loadBanner:@"広告枠 ID"  rootViewController: self];
```

:::

::: tab Swift

```swift
AdLimeAdLoader.loadBanner("広告枠 ID", rootViewController: self)
```

:::

::::

## 広告の表示  

広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `AdLimeAdLoader` の `isBannerReady` メソッドで確認してから表示します。広告を表示する場合は `AdLimeBannerView` オブジェクトを `getBannerAdView` メソッドで取得して表示しましょう。

:::: tabs

::: tab Objective-C

```objectivec
if ([AdLimeAdLoader isBannerReady:@"広告枠 ID"]) {
    AdLimeBannerView *bannerView = [AdLimeAdLoader getBannerAdView:@"広告枠 ID" rootViewController:self];
    [viewContainer addSubview: bannerView];
} else {
    NSLog(@"Ad wasn't ready");
}
```

:::

::: tab Swift

```swift
if(AdLimeAdLoader.isBannerReady("広告枠 ID")) {
    let bannerView = AdLimeAdLoader.getBannerAdView("広告枠 ID", rootViewController: self)
    viewContainer.addSubview(bannerView)
} else {
    print("Ad wasn't ready")
}
```

:::

::::

## 広告のイベント  

`AdLimeBannerViewDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### バナー広告イベントを登録する  

バナー広告のライフサイクルイベントを取得するためには `AdLimeBannerViewDelegate` を継承します。 AdLimeAdLoader では 広告枠 ID ごとに広告を管理するため `getBannerAdView` メソッドで `AdLimeBannerView` オブジェクトを取得し、そのオブジェクトに継承します。この処理は `loadBanner` メソッド呼び出し前、及び広告を表示する前に実行する必要があります。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController () <AdLimeBannerViewDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    AdLimeBannerView *bannerView = [AdLimeAdLoader getBannerAdView:@"広告枠 ID" rootViewController: self];
    bannerView.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController, AdLimeBannerViewDelegate {

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        let bannerView = AdLimeAdLoader.getBannerAdView("広告枠 ID", rootViewController: self)
        bannerView.delegate = self
    }
}
```

:::

::::


### バナー広告イベントを実装する
広告イベントの制御は `AdLimeBannerViewDelegate` を用いて実現できます。実装方法は[バナー広告イベントを実装する](./banner.md#バナー広告イベントを実装する)を確認してください


