# AdLimeAdLoader - ネイティブ広告  

AdLimeAdLoader は広告のキャッシュを管理、効率的に広告を表示する機能です。広告のキャッシュを管理することで、広告ロード回数を減らしたり、広告ロードのタイミングの効率化に望むことができます。

このガイドでは AdLimeAdLoader を用いたネイティブ広告の実装方法について説明します。

## AdLimeAdLoader による基本的な実装  

AdLimeAdLoader は各広告枠 ID ごとに広告のキャッシュを識別しています。AdLimeAdLoader を使って広告のロードや表示をする場合は、広告枠 ID ごとに広告をリクエストする必要があります。また一つの広告枠 ID に一つの広告を管理するため、複数の広告を同時に表示する際は対応する数の広告枠 ID を発行してください。

## AdLimeNativeAd オブジェクトの取得  

AdLimeAdLoader を用いて広告を表示したり、広告のイベントを制御するなどのカスタマイズする必要がある場合は `AdLimeNativeAd` オブジェクトを取得する必要があります。`AdLimeNativeAd` を用いた実装方法は [ネイティブ広告](./native.md) を参考にしてください。

:::: tabs

::: tab Objective-C

```objectivec
AdLimeNativeAd *nativeAd = [AdLimeAdLoader getNativeAd:@"広告枠 ID"];
```

:::

::: tab Swift

```swift
let nativeAd = AdLimeAdLoader.getNativeAd("広告枠 ID")
```

:::

::::

## 広告レイアウトの作成

広告のロード時や広告を表示するときに広告のレイアウトを事前に設定しておきましょう。ネイティブレイアウトの詳細な設定方法は[AdLimeNativeAdLayout](./native.md#広告レイアウトの作成)で確認できます。

広告レイアウトはネイティブ広告のロード時に設定できます。その設定方法は後の節で説明します。また `AdLimeNativeAd` オブジェクトを取得して、そのオブジェクトにネイティブ広告のレイアウトを設定することもできます。


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

    AdLimeNativeAd *nativeAd = [AdLimeAdLoader getNativeAd:@"広告枠 ID"];

    AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getLargeLayout1WithWidth:(CGFloat) width];
    [nativeAd setNativeAdLayout: layout];
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
        let nativeAd = AdLimeAdLoader.getNativeAd("広告枠 ID")
        nativeAd.setNativeAdLayout(AdLimeNativeAdLayout.getLargeLayout1(withWidth: width))
    }
}
```

:::

::::


ネイティブ広告のレイアウトの設定は基本的に 1 回実行すれば十分です。画面が回転するなどでフレームサイズが変更される場合はレイアウトを再読み込みする必要があります。また広告ロード時と広告表示時でフレームサイズが変更される場合にもレイアウトを再読み込みする必要があります。

## 広告のロード  

次に、広告をロードしてみましょう。`AdLimeAdLoader`クラスの`loadNativeAd` を実行してください。またこのときにネイティブ広告のレイアウトを設定できます。

:::: tabs

::: tab Objective-C

```objectivec
AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getLargeLayout1WithWidth:(CGFloat) width];
[AdLimeAdLoader loadNativeAd:@"広告枠 ID" nativeAdLayout:layout];
```

:::

::: tab Swift

```swift
AdLimeAdLoader.loadNativeAd("広告枠 ID", nativeAdLayout: AdLimeNativeAdLayout.getLargeLayout1(withWidth: width))
```

:::

::::

## 広告の表示  

広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `AdLimeAdLoader` の `isNativeAdReady` メソッドで確認してから表示します。広告を表示する場合は `AdLimeNativeAd` オブジェクトを `getNativeAd` メソッドで取得して表示しましょう。

:::: tabs

::: tab Objective-C

```objectivec
if ([AdLimeAdLoader isNativeAdReady:@"広告枠 ID"]) {
    AdLimeNativeAd *nativeAd = [AdLimeAdLoader getNativeAd:@"広告枠 ID"];
    UIView *adView = [nativeAd getAdView];
    [viewContainer addSubview:adView];
} else {
    NSLog(@"Ad wasn't ready");
}
```

:::

::: tab Swift

```swift
if(AdLimeAdLoader.isNativeAdReady("広告枠 ID")) {
    let nativeAd = AdLimeAdLoader.getNativeAd("広告枠 ID")
    let adView = nativeAd.getView()
    viewContainer.addSubview(adView)
} else {
    print("Ad wasn't ready")
}
```

:::

::::

## 広告のイベント  

`AdLimeNativeAdDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### ネイティブ広告イベントを登録する  

ネイティブ広告のライフサイクルイベントを取得するためには `AdLimeNativeAdDelegate` を継承します。 AdLimeAdLoader では 広告枠 ID ごとに広告を管理するため `getNativeAd` メソッドで `AdLimeNativeAd` オブジェクトを取得し、そのオブジェクトに継承します。この処理は `loadNativeAd` メソッド呼び出し前、及び広告を表示する前に実行する必要があります。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController () <AdLimeNativeAdDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    AdLimeNativeAd *nativeAd = [AdLimeAdLoader getNativeAd:@"aaaa"];
    nativeAd.delegate = self
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController, AdLimeNativeAdDelegate {

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        let nativeAd = AdLimeAdLoader.getNativeAd("広告枠 ID")
        nativeAd.delegate = self
    }
}
```

:::

::::


### ネイティブ広告イベントを実装する
広告イベントの制御は `AdLimeNativeAdDelegate` を用いて実現できます。実装方法は[ネイティブ広告イベントを実装する](./native.md#ネイティブ広告イベントを実装する)を確認してください
