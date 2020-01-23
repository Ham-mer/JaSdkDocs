#  MixViewAd
MixViewAd とはバナー広告やネイティブ広告などの別種の広告を単一の View で表示ができる機能です。各ネットワークの提供する広告は、個別のフォーマットで独立した広告が提供されていました。この機能を実装することにより、1つの広告枠で表示できる広告の種類と数を増やし、より高い効率で収益を増やすことができます。

現時点では MixViewAd は[バナー広告](./banner.md)と[ネイティブ広告](./native.md)をサポートしています。このガイドでは MixViewAd を iOS のアプリに実装する方法を説明します。

## 前提条件
- AdLime SDK が導入済みであること

## MixViewAdの作成
広告を表示するまでのサイクルは `AdLimeMixViewAd` オブジェクトを用いて広告をリクエストし、その後広告を表示するためのViewを取得することです。広告を表示するための最初のステップとして 広告枠 ID を設定した `MixViewAd` を生成します。

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

    self.mixViewAd = [[AdLimeMixViewAd alloc] initWithAdUnitId:@"広告枠 ID" rootViewController:self];
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
        self.mixViewAd = AdLimeMixViewAd.init(adUnitId: "広告枠 ID"), rootViewController: self)
    }
}
```

:::

::::

## ネイティブ広告のレイアウト
`AdLimeMixViewAd` オブジェクトを生成したら広告をロードする前にネイティブ広告のレイアウトを事前に設定しておきましょう。ネイティブ広告のレイアウトは AdLime SDK の `AdLimeNativeAdLayout` によって管理しています。また、ネイティブ広告のレイアウトはカスタムで設定できます<br>
**`AdLimeNativeAdLayout` の情報について[AdLimeNativeAdLayout](./native.md#広告レイアウトの作成))で確認できます。**

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
広告をロード完了したら広告を表示してみましょう。`AdLimeMixViewAd` の `getView` メソッドで、ロードした広告の UIView が取得できます。また広告を表示する前に広告がロード済みかどうかを`isReady`メソッドを用いて確認できます。<br>

:::: tabs

::: tab Objective-C

```objectivec
- (void)adLimeMixViewAdDidReceiveAd:(AdLimeMixViewAd *)mixViewAd {
    UIView *adView = [mixViewAd getAdView:layout];
    [self.view addSubview:adView];
}
```

:::

::: tab Swift

```swift
func adLimeMixViewAdDidReceive(_ mixViewAd: AdLimeMixViewAd!) {
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
@import UIKit;

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
/// 広告が正しくロードされたことを通知するデリゲートメソッド
- (void)adLimeMixViewAdDidReceiveAd:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdDidReceiveAd");
}

/// 広告のロード失敗を通知するデリゲートメソッド 
- (void)adLimeMixViewAd:(AdLimeMixViewAd *)mixViewAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"AdLimeMixViewAd:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@", adError.getCode, adError.description);
}

/// タップ可能な広告を表示されたことを通知するデリゲートメソッド
- (void)adLimeMixViewAdWillPresentScreen:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdWillPresentScreen");
}

/// ユーザーが広告をタップして外部リンク（App Storeなど）へ遷移したことを通知するデリゲートメソッド
- (void)adLimeMixViewAdWillLeaveApplication:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdWillLeaveApplication");
}

```

:::

::: tab Swift

```swift
/// 広告が正しくロードされたことを通知するデリゲートメソッド
func adLimeMixViewAdDidReceive(_ mixViewAd: AdLimeMixViewAd!) {
    print("AdLimeMixViewAdDidReceiveAd")
}

/// 広告のロード失敗を通知するデリゲートメソッド
func adLimeMixViewAd(_ mixViewAd: AdLimeMixViewAd!, didFailToReceiveAdWithError adError: AdLimeAdError!) {
    print("adLimeMixView:didFailToReceiveAdWithError, errorCode is \(adError.getCode().rawValue), errorMessage is \(adError.description)")
}

/// タップ可能な広告を表示されたことを通知するデリゲートメソッド
func adLimeMixViewAdWillPresentScreen(_ mixViewAd: AdLimeMixViewAd!) {
    print("AdLimeMixViewAdWillPresentScreen")
}

/// ユーザーが広告をタップして外部リンク（App Storeなど）へ遷移したことを通知するデリゲートメソッド
func adLimeMixViewAdWillLeaveApplication(_ mixViewAd: AdLimeMixViewAd!) {
    print("AdLimeMixViewAdWillLeaveApplication")
}
```

:::

::::


### 広告ロードエラーについて  

広告のロードに失敗した場合は、`AdLimeMixViewAdDelegate` の `adLimeMixViewAd:didFailToReceiveAdWithError` が呼び出されます。 `adError.getCode` 、`adError.description` を用いてエラーコードとエラーメッセージを取得できます。

#### エラーコードとエラーメッセージについて

[エラー情報](./error.md#エラーコードとエラーメッセージ)を確認してください。

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

## 次のステップ
- 他の広告フォーマットを追加で利用したい場合は[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、iOSアプリに実装しましょう。
- 広告が正しく表示できるか確認したい場合は[広告表示テスト](./test.md)に従い、App ID と各広告ネットワークに対応する広告フォーマットの広告枠 ID を設定して広告を表示してみましょう。
