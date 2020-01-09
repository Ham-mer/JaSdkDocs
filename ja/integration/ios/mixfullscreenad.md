#  MixFullScreenAd
MixFullScreenAd はフルスクリーンで表示することができるインタースティシャル広告を拡張した機能です。また、インタースティシャル広告を表示するだけではなく、バナー広告やネイティブ広告なども同じ広告枠にフルスクリーン表示することができます。各ネットワークの提供する広告は、個別のフォーマットで独立した広告が提供されていました。この機能を実装することにより、1つの広告枠で表示できる広告の種類と数を増やし、より高い効率で収益を増やすことができます。

現時点では MixViewAd は[バナー広告](./banner.md)と[ネイティブ広告](./native.md)と[インタースティシャル広告](./Interstitial.md)をサポートしています。
このガイドでは MixFullScreenAd を iOS のアプリに実装する方法を説明します。

## 前提条件
- AdLime SDKの導入

## MixFullScreenAd の作成
広告を表示するまでのサイクルは `AdLimeMixFullScreenAd` オブジェクトを用いて広告をリクエストし、広告を表示することです。広告を表示するための最初のステップとして AdUnit ID を設定した `MixFullScreeenAd` を生成します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;

@interface ViewController ()

@property(nonatomic, strong) AdLimeMixFullScreenAd *mixFullScreenAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.mixFullScreenAd = [[AdLimeMixFullScreenAd alloc] initWithAdUnitId:@"AdUnit_ID"];
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController {
    var mixFullScreenAd: AdLimeMixFullScreenAd!

    override func viewDidLoad() {
        super.viewDidLoad()
        self.mixFullScreenAd = AdLimeMixFullScreenAd.init(adUnitId: "AdUnit_ID") 
    }
}
```

:::

::::


## ネイティブ広告のレイアウト
`AdLimeMixFullScreenAd` オブジェクトを生成したら広告をロードする前にネイティブ広告のレイアウトを事前に設定しておきましょう。ネイティブ広告のレイアウトは AdLime SDK の `AdLimeNativeAdLayout` によって管理しています。また、ネイティブ広告のレイアウトはカスタムで設定できます<br>
**`AdLimeNativeAdLayout` の情報について[AdLimeNativeAdLayout](https://www.adlime.net/docs/ja/integration/ios/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できます。**

:::: tabs

::: tab Objective-C

```objc
AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getFullLayout1];
[self.mMixFullScreenAd setNativeAdLayout:layout];
```

:::

::: tab Swift

```swift
let layout = AdLimeNativeAdLayout.getFullLayout1()
self.mixFullScreenAd.setNativeAdLayout(layout)
```

:::

::::



## 広告のロード
`AdLimeMixFullScreenAd` オブジェクトを生成したら広告をロードしてみましょう。広告ロード完了のタイミングは後に紹介する `AdLimeMixFullScreenAdDelegate` の `adLimeMixFullScreenAdDidReceiveAd`  を用いることで取得できます。

:::: tabs

::: tab Objective-C

```objectivec
[self.mixFullScreenAd loadAd];
```

:::

::: tab Swift

```swift
self.mixFullScreenAd.load()
```

:::

::::


## 広告の表示
広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `isReady` メソッドで確認してから `AdLimeMixFullScreenAd` の `show` で表示します。

:::: tabs

::: tab Objective-C

```objectivec
if([self.mixFullScreenAd isReady]) {
    [self.mixFullScreenAd showFromViewController:self];
}
```

:::

::: tab Swift

```swift
if(self.mixFullScreenAd.isReady()) {
        self.mixFullScreenAd.show(from: self)
}
```

:::

::::



## 広告イベント

`AdLimeMixFullScreenAdDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### MixFullScreenAd イベントを登録する
MixFullScreenAd のライフサイクルイベントを取得するためには `AdLimeMixFullScreenAdDelegate` を継承します。通常、`AdLimeMixFullScreenAd` を実装するクラスがデリゲートクラスとなる場合が多いので、本ガイドでは `delegate` プロパティを `self` に設定します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeMixFullScreenAdDelegate>

@property(nonatomic, strong) AdLimeMixFullScreenAd *mixFullScreenAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    self.mixFullScreenAd.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
class ViewController: UIViewController, AdLimeMixViewAdDelegate {
    var mixFullScreenAd: AdLimeMixFullScreenAd!

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        self.mixFullScreenAd.delegate = self
    }
}
```

:::

::::


### MixViewAd イベントを実装する
広告のイベントの制御は `AdLimeMixFullScreenAdDelegate` を用いて実現できます。以下のサンプルでは、各メソッドを実装し、コンソールにログを出力します。

:::: tabs

::: tab Objective-C

```objectivec
/// A MixFullScreen ad has loaded, and can be displayed.
- (void)adLimeMixFullScreenAdDidReceiveAd:(AdLimeMixFullScreenAd *)mixFullScreenAd {
    NSLog(@"AdLimeMixFullScreenAdDidReceiveAd");
}

/// The MixFullScreen ad request failed, and a new request can be sent.
- (void)adLimeMixFullScreenAd:(AdLimeMixFullScreenAd *)mixFullScreenAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"AdLimeMixFullScreenAd:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@",
            adError.getCode, adError.description);
}

/// The MixFullScreen ad was shown.
- (void)adLimeMixFullScreenAdWillPresentScreen:(AdLimeMixFullScreenAd *)mixFullScreenAd {
    NSLog(@"AdLimeMixFullScreenAdWillPresentScreen");
}

/// The MixFullScreen ad will cause the application to become inactive and open a new application.
- (void)adLimeMixFullScreenAdWillLeaveApplication:(AdLimeMixFullScreenAd *)mixFullScreenAd {
    NSLog(@"AdLimeMixFullScreenAdWillLeaveApplication");
}

/// The MixView ad did dismiss a full screen view.
- (void)adLimeMixFullScreenAdDidDismissScreen:(AdLimeMixFullScreenAd *)mixFullScreenAd {
    NSLog(@"AdLimeMixFullScreenAdDidDismissScreen");
}
```

:::

::: tab Swift

```swift
/// A MixFullScreen ad has loaded, and can be displayed.
func adLimeMixFullScreenAdDidReceive(_ mixFullScreenAd: AdLimeMixFullScreenAd!) {
    print("AdLimeMixFullScreenAdDidReceiveAd")
}
/// The MixFullScreen ad request failed, and a new request can be sent.
func adLimeMixFullScreenAd(_ mixFullScreenAd: AdLimeMixFullScreenAd!, didFailToReceiveAdWithError adError: AdLimeAdError!) {
    print("adLimeMixFullScreenAd:didFailToReceiveAdWithError, errorCode is \(adError.getCode().rawValue), errorMessage is \(adError.description)")
}
/// The MixFullScreen ad was shown.
func adLimeMixFullScreenAdWillPresentScreen(_ mixFullScreenAd: AdLimeMixFullScreenAd!) {
    print("AdLimeMixFullScreenAdWillPresentScreen")
}
/// The MixFullScreen ad will cause the application to become inactive and open a new application.
func adLimeMixFullScreenAdWillLeaveApplication(_ mixFullScreenAd: AdLimeMixFullScreenAd!) {
    print("AdLimeMixFullScreenAdWillLeaveApplication")
}
/// The MixView ad did dismiss a full screen view.
func adLimeMixFullScreenAdDidDismissScreen(_ mixFullScreenAd: AdLimeMixFullScreenAd!) {
    print("AdLimeMixFullScreenAdDidDismissScreen")
}
```

:::

::::


### エラー情報
広告のロードに失敗した場合は、`AdLimeMixFullScreenAdDelegate` の `adLimeMixFullScreenAd:didFailToReceiveAdWithError` が呼び出されます。`adError.getCode` 、`adError.description` を用いてエラーコードとエラー情報を取得できます。

エラーコードは AdLimeAdErrorCode に定義される ：
|定義                           |説明     |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | 無効リクエスト |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットエラー |
|ADLIME_ADERROR_NO_FILL         | 配信できる広告がない   |
|ADLIME_ADERROR_TIMEOUT         | タイムアウト |

エラーには 広告ユニットID(AdUnit)、広告ネットワーク名(Network)、広告のプロパティ(LineItem)が含まれます。
```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## 広告レイアウト作成作成の遅延

ネイティブ広告のロード前にレイアウトを作成するのではなく、ネイティブ広告のロード完了後に、`AdLimeNativeAdLayout` を作成することも可能です。

:::: tabs

::: tab Objective-C

```objectivec
if([self.mixFullScreenAd isReady]) {
    AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getFullLayout1];
    [self.mMixFullScreenAd setNativeAdLayout:layout];
    [self.mixFullScreenAd showFromViewController:self];
}
```

:::

::: tab Swift

```swift
if(self.mixFullScreenAd.isReady()) {
    let layout = AdLimeNativeAdLayout.getFullLayout1()
    self.mixFullScreenAd.setNativeAdLayout(layout)
    self.mixFullScreenAd.show(from: self)
}
```

:::

::::

