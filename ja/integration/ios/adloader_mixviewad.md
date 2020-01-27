# AdLimeAdLoader - MixViewAd  

AdLimeAdLoader は広告のキャッシュを管理、効率的に広告を表示する機能です。広告のキャッシュを管理することで、広告ロード回数を減らしたり、広告ロードのタイミングの効率化に望むことができます。

このガイドでは AdLimeAdLoader を用いた MixViewAd の実装方法について説明します。

## AdLimeAdLoader による基本的な実装  

AdLimeAdLoader は各広告枠 ID ごとに広告のキャッシュを識別しています。AdLimeAdLoader を使って広告のロードや表示をする場合は、広告枠 ID ごとに広告をリクエストする必要があります。また一つの広告枠 ID に一つの広告を管理するため、複数の広告を同時に表示する際は対応する数の広告枠 ID を発行してください。

## AdLimeMixViewAd オブジェクトの取得  

AdLimeAdLoader を用いて広告を表示したり、広告のイベントを制御するなどのカスタマイズする必要がある場合は `AdLimeMixViewAd` オブジェクトを取得する必要があります。`AdLimeMixViewAd` を用いた実装方法は [MixViewAd](./mixviewad.md) を参考にしてください。

:::: tabs

::: tab Objective-C

```objectivec
AdLimeMixViewAd *mixViewAd = [AdLimeAdLoader getMixViewAd:@"広告枠 ID" rootViewController:self];
```

:::

::: tab Swift

```swift
let mixViewAd = AdLimeAdLoader.getMixViewAd("広告枠 ID", rootViewController: self)
```

:::

::::

## 広告レイアウトの作成

広告のロード時や広告を表示するときに広告のレイアウトを事前に設定しておきましょう。ネイティブレイアウトの詳細な設定方法は [AdLimeNativeAdLayout](./native.md#広告レイアウトの作成) で確認できます。

広告レイアウトはネイティブ広告のロード時に設定できます。その設定方法は後の節で説明します。また `AdLimeMixViewAd` オブジェクトを取得して、そのオブジェクトにネイティブ広告のレイアウトを設定することもできます。


:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...
    AdLimeMixViewAd *mixViewAd = [AdLimeAdLoader getMixViewAd:@"広告枠 ID" rootViewController:self];
    AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getLargeLayout1WithWidth:(CGFloat) width];
    [mixViewAd setNativeAdLayout:layout];
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        let mixViewAd = AdLimeAdLoader.getMixViewAd("広告枠 ID", rootViewController: self)
        mixViewAd.setNativeAdLayout(AdLimeNativeAdLayout.getLargeLayout1(withWidth: width))
    }
}
```

:::

::::

ネイティブ広告のレイアウトの設定は基本的に 1 回実行すれば十分です。サイズが変更になるなどレイアウトが変更される場合は再読込する必要があります。

## 広告のロード  

次に、広告をロードしてみましょう。`AdLimeAdLoader`クラスの`load` を実行してください。またこのときにネイティブ広告のレイアウトを設定できます。

:::: tabs

::: tab Objective-C

```objectivec
AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getLargeLayout1WithWidth:(CGFloat) width];
[AdLimeAdLoader loadMixViewAd:@"広告枠 ID" rootViewController:self nativeAdLayout:layout];
```

:::

::: tab Swift

```swift
AdLimeAdLoader.loadMixViewAd("広告枠 ID", rootViewController: self, nativeAdLayout: AdLimeNativeAdLayout.getLargeLayout1(withWidth: width))
```

:::

::::

## 広告の表示  

広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `AdLimeAdLoader` の `isMixViewAdReady` メソッドで確認してから表示します。広告を表示する場合は `AdLimeMixViewAd` オブジェクトを `getNativeAd` メソッドで取得して表示しましょう。

:::: tabs

::: tab Objective-C

```objectivec
if([AdLimeAdLoader isMixViewAdReady:@"広告枠 ID"]) {
    AdLimeMixViewAd *mixAd = [AdLimeAdLoader getMixViewAd:@"広告枠 ID" rootViewController:self];
    UIView *adView = [mixAd getAdView];
    [viewContainer addSubview:adView];
} else {
    NSLog(@"Ad wasn't ready");
}
```

:::

::: tab Swift

```swift
if(AdLimeAdLoader.isMixViewAdReady("広告枠 ID")) {
    let mixAd = AdLimeAdLoader.getMixViewAd("広告枠 ID", rootViewController: self)
    let adView = mixAd.getView()
    viewContainer.addSubview(adView)
} else {
    print("Ad wasn't ready")
}
```

:::

::::

## 広告のイベント  

`AdLimeMixViewAdDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### MixViewAd イベントを登録する  

MixViewAd のライフサイクルイベントを取得するためには `AdLimeMixViewAdDelegate` を継承します。 AdLimeAdLoader では 広告枠 ID ごとに広告を管理するため `getMixViewAd` メソッドで `AdLimeMixViewAd` オブジェクトを取得し、そのオブジェクトに継承します。この処理は `loadMixViewAd` メソッド呼び出し前、または広告を表示する前に実行する必要があります。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;]
@import UIKit;

@interface ViewController () <AdLimeMixViewAdDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    AdLimeMixViewAd *mixViewAd = [AdLimeAdLoader getMixViewAd:@"広告枠 ID" rootViewController:self];
    mixViewAd.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController, AdLimeMixViewAdDelegate {

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        let mixViewAd = AdLimeAdLoader.getMixViewAd("広告枠 ID", rootViewController: self)
        mixViewAd.delegate = self
    }
}
```

:::

::::


### MixViewAd イベントを実装する
広告イベントの制御は `AdLimeMixViewAdDelegate` を用いて実現できます。実装方法は[MixViewAd イベントを実装する](./mixviewad.md#MixViewAd-イベントを実装する)を確認してください
