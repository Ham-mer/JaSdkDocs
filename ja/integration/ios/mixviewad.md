#  MixViewAd
MixViewAd とはバナー広告やネイティブ広告などの別種の広告を単一の View で表示ができる機能です。各ネットワークの提供する広告は、個別のフォーマットで独立した広告が提供されていました。この機能を実装することにより、1つの広告枠で表示できる広告の種類と数を増やし、より高い効率で収益を増やすことができます。

現時点では MixViewAd は[バナー広告](./banner.md)と[ネイティブ広告](./native.md)をサポートしています。このガイドでは MixViewAd を iOS のアプリに実装する方法を説明します。

## 前提条件
- AdLime SDK が導入済みであること

## MixViewAdの作成
広告を表示するまでのサイクルは `AdLimeMixViewAd` オブジェクトを用いて広告をリクエストし、その後広告を表示するためのViewを取得することです。広告を表示するための最初のステップとして AdUnit ID を設定した `MixViewAd` を生成します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController ()

@property(nonatomic, strong) AdLimeMixViewAd *mixViewAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.mixViewAd = [[AdLimeMixViewAd alloc] initWithAdUnitId:@"AdUnit_ID" rootViewController:self];
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewControllerd {
    var mixViewAd: AdLimeMixViewAd!

    override func viewDidLoad() {
        super.viewDidLoad()
        self.mixViewAd = AdLimeMixViewAd.init(adUnitId: "AdUnit_ID"), rootViewController: self)
    }
}
```

:::

::::

## ネイティブ広告のレイアウト
`AdLimeMixViewAd` オブジェクトを生成したら広告をロードする前にネイティブ広告のレイアウトを事前に設定しておきましょう。ネイティブ広告のレイアウトは AdLime SDK の `AdLimeNativeAdLayout` によって管理しています。また、ネイティブ広告のレイアウトはカスタムで設定できます<br>
**`AdLimeNativeAdLayout` の情報について[AdLimeNativeAdLayout](https://www.adlime.net/docs/ja/integration/ios/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できます。**

:::: tabs

::: tab Objective-C

```objc
AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getLargeLayout1WithWidth:360];
[self.mixViewAd setNativeAdLayout:layout];
```

:::

::: tab Swift

```swift
let layout = AdLimeNativeAdLayout.getLargeLayout1(withWidth: 360)
self.mixViewAd.setNativeAdLayout(layout)
```

:::

::::


## 広告のロード
`AdLimeMixViewAd` オブジェクトを生成したら広告をロードしてみましょう。広告ロード完了のタイミングは後に紹介する `AdLimeMixViewAdDelegate` の `adLimeMixViewAdDidReceiveAd` を用いることで取得できます。

:::: tabs

::: tab Objective-C

```objectivec
[self.mixViewAd loadAd];
```

:::

::: tab Swift

```swift
self.mixViewAd.load()
```

:::

::::



## 広告の表示
広告をロード完了したら広告を表示してみましょう。`AdLimeMixViewAd` の `getView` メソッドで、ロードした広告の UIView が取得できます。ここでは広告を表示する前に広告がロード済みかどうかを`isReady`メソッドを用いて確認しています。<br>

:::: tabs

::: tab Objective-C

```objectivec
if([self.mixViewAd isReady]) {
    UIView *adView = [mixViewAd getAdView:layout];
    [self.view addSubview:adView];
}
```

:::

::: tab Swift

```swift
if(self.mixViewAd.isReady()) {
    let mixView = mixViewAd.getView()
    self.view.addSubview(mixView)
}
```

:::

::::


## 広告イベント

`AdLimeMixViewAdDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### MixViewAd 広告イベントを登録する
MixViewAd のライフサイクルイベントを取得するためには `AdLimeMixViewAdDelegate` を継承します。通常、`AdLimeMixViewAd` を実装するクラスがデリゲートクラスとなる場合が多いので、本ガイドでは `delegate` プロパティを `self` に設定します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeMixViewAdDelegate>

@property(nonatomic, strong) AdLimeMixViewAd *mixViewAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    self.mixViewAd.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController, AdLimeMixViewAdDelegate {
    var mixViewAd: AdLimeMixViewAd!

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        self.mixViewAd.delegate = self
    }
}
```

:::

::::


### MixViewAd イベントを実装する
広告のイベントの制御は `AdLimeMixViewAdDelegate` を用いて実現できます。以下のサンプルでは、各メソッドを実装し、コンソールにログを出力します。

:::: tabs

::: tab Objective-C

```objectivec
/// A MixView ad has loaded, and can be displayed.
- (void)adLimeMixViewAdDidReceiveAd:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdDidReceiveAd");
}

/// The MixView ad request failed, and a new request can be sent.
- (void)adLimeMixViewAd:(AdLimeMixViewAd *)mixViewAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"AdLimeMixViewAd:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@", adError.getCode, adError.description);
}

/// The MixView ad was shown.
- (void)adLimeMixViewAdWillPresentScreen:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdWillPresentScreen");
}

/// The MixView ad will cause the application to become inactive and open a new application.
- (void)adLimeMixViewAdWillLeaveApplication:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdWillLeaveApplication");
}

/// The MixView ad did dismiss a full screen view.
- (void)adLimeMixViewAdDidDismissScreen:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdDidDismissScreen");
}
```

:::

::: tab Swift

```swift
/// A MixView ad has loaded, and can be displayed.
func adLimeMixViewAdDidReceive(_ mixViewAd: AdLimeMixViewAd!) {
    print("AdLimeMixViewAdDidReceiveAd")
}
/// The MixView ad request failed, and a new request can be sent.
func adLimeMixViewAd(_ mixViewAd: AdLimeMixViewAd!, didFailToReceiveAdWithError adError: AdLimeAdError!) {
    print("adLimeMixView:didFailToReceiveAdWithError, errorCode is \(adError.getCode().rawValue), errorMessage is \(adError.description)")
}
/// The MixView ad was shown.
func adLimeMixViewAdWillPresentScreen(_ mixViewAd: AdLimeMixViewAd!) {
    print("AdLimeMixViewAdWillPresentScreen")
}

/// The MixView ad will cause the application to become inactive and open a new application.
func adLimeMixViewAdWillLeaveApplication(_ mixViewAd: AdLimeMixViewAd!) {
    print("AdLimeMixViewAdWillLeaveApplication")
}
/// The MixView ad did dismiss a full screen view.
func adLimeMixViewAdDidDismissScreen(_ mixViewAd: AdLimeMixViewAd!) {
    print("AdLimeMixViewAdDidDismissScreen")
}
```

:::

::::


### エラー情報
広告のロードに失敗した場合は、`AdLimeMixViewAdDelegate` の `adLimeMixViewAd:didFailToReceiveAdWithError` が呼び出されます。 `adError.getCode` 、`adError.description` を用いてエラーコードとエラー情報を取得できます。

エラーコードは `AdLimeAdErrorCode` に定義される：
|定義                           |説明     |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | 無効リクエスト |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットエラー |
|ADLIME_ADERROR_NO_FILL         | 配信できる広告がない      |
|ADLIME_ADERROR_TIMEOUT         | タイムアウト |


エラーには 広告ユニットID(AdUnit)、広告ネットワーク名(Network)、広告のプロパティ(LineItem)が含まれます。
```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## 広告レイアウト作成作成の遅延

ネイティブ広告をロード前にレイアウトを作成するのではなく、ネイティブ広告のロード完了後に、  `AdLimeNativeAdLayout` を作成することも可能です。

:::: tabs

::: tab Objective-C

```objectivec
- (void)adLimeMixViewAdDidReceiveAd:(AdLimeMixViewAd *)mixViewAd {
    AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getLargeLayout1WithWidth:360];
    UIView *adView = [mixViewAd getAdView:layout];
    [self.view addSubview:adView];
}
```

:::

::: tab Swift

```swift
func adLimeMixViewAdDidReceive(_ mixViewAd: AdLimeMixViewAd!) {
    let layout = AdLimeNativeAdLayout.getLargeLayout1(withWidth: 360)
    let adView = mixViewAd.getView(layout)
    self.view.addSubview(view)
}
```

:::

::::

## プリロードとキャッシュ
事前に広告をロードをして、表示までの待ち時間を極力抑えましょう。<br>
また広告をプリロードする・しないに関わらず、広告をキャッシュすることをおすすめします。広告枠では、各広告ネットワークの広告がロードされますが、広告枠の1つのインスタンスを繰り返し使用することで、高いインプレッションを得られ、不要なリクエストも抑えることができます。これらは、[AdLimeAdLoader](./adloader.md)で実現が可能です。

