# インタースティシャル広告

インタースティシャル広告とは、アプリ上を覆うように表示されるフルスクリーン広告です。一般的にアプリの画面が切り替わるタイミング（アクティビティが切り替わるタイミングやゲームのステージが変わる合間）で用いられます。アプリにインタースティシャル広告が表示されたとき、ユーザーは広告をタップしてリンク先 URL に移動するか、広告を閉じてアプリに戻るかを選ぶことができます。

このガイドは、インタースティシャル広告を iOS アプリに実装する方法について説明します。

## 前提条件
- AdLime SDK が導入済みであること

## インタースティシャル広告オブジェクトの作成
広告を表示するまでのサイクルは`AdLimeInterstitialAd`オブジェクトを用いて広告をリクエストし、広告を表示することです。広告を表示するための最初のステップとしてAdUnit IDを設定した`AdLimeInterstitialAd`を生成します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController ()

@property(nonatomic, strong) AdLimeInterstitialAd *interstitialAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.interstitialAd = [[AdLimeInterstitialAd alloc] initWithAdUnitId:@"AdUnit_ID"];
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController {
    var interstitialAd: AdLimeInterstitialAd!

    override func viewDidLoad() {
        super.viewDidLoad()
        self.rewardedVideoAd = AdLimeInterstitialAd.init(adUnitId: "AdUnit_ID")
    }
}
```

:::

::::


## 広告のロード
`AdLimeInterstitialAd` オブジェクトを生成したら広告をロードしてみましょう。広告ロード完了のタイミングは後に紹介する`AdLimeInterstitialAdDelegate` の`adLimeMixFullScreenAdDidReceiveAd` を用いることで取得できます

:::: tabs

::: tab Objective-C

```objectivec
@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    [self.interstitialAd loadAd];
}

@end
```

:::

::: tab Swift

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    ...
    self.interstitialAd.load()
}
```

:::

::::


## 広告の表示
広告をロードしたら広告を表示してみましょう。広告を表示する前に広告がロード済みかどうかを `isReady` メソッドで確認してから `AdLimeInterstitialAd` の `show` で表示します。

:::: tabs

::: tab Objective-C

```objectivec
- (IBAction)doSomething:(id)sender {
  ...
    if ([self.interstitialAd isReady]) {
        [self.interstitialAd showFromViewController:self];
    } else {
        NSLog(@"Ad wasn't ready");
    }
}
```

:::

::: tab Swift

```swift
class ViewController: UIViewController {
    @IBAction func doSomething(sender: Any) {
        if(self.interstitialAd.isReady()) {
            self.interstitialAd.show(from: self)
        } else {
            print("Ad wasn't ready")
        }
    }
}
```

:::

::::


## 広告イベント
AdLimeInterstitialAdDelegate によって、広告を閉じたとき、またユーザーがアプリから離れたときなど、広告のライフサイクルイベントを受け取ることができます。

### インタースティシャル広告イベントを登録する
インタースティシャル広告のライフサイクルイベントを取得するためには `AdLimeInterstitialAdDelegate` を継承します。通常、 `AdLimeInterstitialAd` を実装するクラスがデリゲートクラスとなる場合が多いので、本ガイドでは `delegate` プロパティを `self` に設定します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeInterstitialAdDelegate>

@property(nonatomic, strong) AdLimeInterstitialAd *interstitialAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    self.interstitialAd.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
class ViewController: UIViewController, AdLimeInterstitialAdDelegate {
    var interstitialAd: AdLimeInterstitialAd!

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        self.interstitialAd.delegate = self
    }
}
```

:::

::::


### インタースティシャル広告イベントを実装する
広告のイベントの制御は `AdLimeInterstitialAdDelegate` を用いて実現できます。以下のサンプルでは、各メソッドを実装し、コンソールにログを出力します。

:::: tabs

::: tab Objective-C

```objectivec
/// Tells the delegate an ad request succeeded.
- (void)adLimeInterstitialDidReceiveAd:(AdLimeInterstitialAd *)interstitialAd {
    NSLog(@"interstitialDidReceiveAd");
}

/// Tells the delegate an ad request failed.
- (void)adLimeInterstitial:(AdLimeInterstitialAd *)interstitialAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"adLimeInterstitial:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@",
            adError.getCode, adError.description);
}

/// Tells the delegate that an interstitial will be presented.
- (void)adLimeInterstitialWillPresentScreen:(AdLimeInterstitialAd *)interstitialAd {
    NSLog(@"adLimeInterstitialWillPresentScreen");
}

/// Tells the delegate the interstitial had been animated off the screen.
- (void)adLimeInterstitialDidDismissScreen:(AdLimeInterstitialAd *)interstitialAd {
    NSLog(@"adLimeInterstitialDidDismissScreen");
}

/// Tells the delegate that a user click will open another app (such as the App Store), backgrounding the current app.
- (void)adLimeInterstitialWillLeaveApplication:(AdLimeInterstitialAd *)interstitialAd {
    NSLog(@"adLimeInterstitialWillLeaveApplication");
}
```

:::

::: tab Swift

```swift
/// Tells the delegate an ad request succeeded.
func adLimeInterstitialDidReceive(_ interstitialAd: AdLimeInterstitialAd!) {
    print("interstitialDidReceiveAd")
}

/// Tells the delegate an ad request failed.
func adLimeInterstitial(_ interstitialAd: AdLimeInterstitialAd!, didFailToReceiveAdWithError adError: AdLimeAdError!) {
    print("adLimeInterstitial:didFailToReceiveAdWithError, errorCode is \(adError.getCode().rawValue), errorMessage is \(adError.description)")
}

/// Tells the delegate that an interstitial will be presented.
func adLimeInterstitialWillPresentScreen(_ interstitialAd: AdLimeInterstitialAd!) {
    print("adLimeInterstitialWillPresentScreen")
}

/// Tells the delegate the interstitial had been animated off the screen.
func adLimeInterstitialDidDismissScreen(_ interstitialAd: AdLimeInterstitialAd!) {
    print("adLimeInterstitialDidDismissScreen")
}

/// Tells the delegate that a user click will open another app (such as the App Store), backgrounding the current app.
func adLimeInterstitialWillLeaveApplication(_ interstitialAd: AdLimeInterstitialAd!) {
    print("adLimeInterstitialWillLeaveApplication")
}
```

:::

::::


### エラーの情報

広告のロードに失敗した場合は、`AdLimeInterstitialAdDelegate` の  `adLimeInterstitial:didFailToReceiveAdWithError:` が呼び出されます。 `adError.getCode`、`adError.description` を用いてエラーコードとエラー情報を取得できます。

AdLimeAdErrorCode  エラーコード一覧
|定義                           |説明    |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | リクエストが無効 |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットワークエラー |
|ADLIME_ADERROR_NO_FILL         | 配信できる広告がない    |
|ADLIME_ADERROR_TIMEOUT         | リクエスト　タイムアウト |

エラーには 広告ユニットID(AdUnit)、広告ネットワーク名(Network)、広告のプロパティ(LineItem)が含まれます。

```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## インタースティシャル広告を再リクエストする
インタースティシャル広告を表示後、新たにインタースティシャル広告のリクエストするための適切なタイミングは表示しているインタースティシャル広告を閉じたタイミングです。具体的には `AdLimeInterstitialAdDelegate` の `adLimeInterstitialDidDismissScreen` メソッド内で次のインタースティシャル広告のロードを開始することができます。

:::: tabs

::: tab Objective-C

```objectivec
- (void)adLimeInterstitialDidDismissScreen:(AdLimeInterstitialAd *)interstitialAd {
    [self.interstitialAd loadAd];
}
```

:::

::: tab Swift

```swift
func adLimeInterstitialDidDismissScreen(_ interstitialAd: AdLimeInterstitialAd!){
    self.interstitialAd.load()
}
```

:::

::::

## 推奨事項
### インタースティシャル広告がアプリに適しているかどうか確認してください

インタースティシャル広告は、画面の切り替わりがあるアプリに適しています。
例えば、画像の共有やゲームステージのクリアなど、アプリで特定のタスクが完了した際に発生します。ユーザーはこのタイミングで中断が入ることを認知しているので、インタースティシャル広告を表示してもユーザーエクスペリエンスに悪影響を及ぼすことはありません。アプリプロセスの、どの時点でインタースティシャル広告を表示するか、またユーザーがそれにどう反応するかを共に考慮に入れてください。


### インタースティシャル広告を表示する際には、必ず操作を一時停止してください

インタースティシャル広告には、テキスト・イメージ・動画など様々な種類があります。インタースティシャル広告を表示する際に、アプリのリソースを一時停止させることが極重要です。たとえば、インタースティシャル広告を呼び出した後、アプリの音声出力や複雑な計算処理（ゲームループなど）を一時停止してください。これらの処理はイベントハンドラ `adLimeInterstitialDidDismissScreen` によって再開できます。このハンドラは、ユーザーが広告に対する操作を完了した後に呼び出されます。処理を一時停止することで、画像の読み込みが遅くなったり、あるいは反応しなくなったり、動画が頻繁に途切れたりするリスクを抑えることができます。

### 十分な広告のロード時間を確保してください

インタースティシャル広告を表示するタイミングを確保すると共に、広告のロード時間を確保することも重要です。広告を表示する前に十分な時間を確保して広告をロードすることで広告を表示するまでの待ち時間を節約できます。また広告を表示する前に必ず `AdLimeInterstitialAd` の `isReady` メソッドをチェックして広告の表示の準備ができているかを確認してください。

### 過度に広告を表示しないように注意してください

インタースティシャル広告の表示頻度を増やすことで収益の向上が見込めますが、それが原因でユーザーエクスペリエンスが損なわれ、ユーザーの離脱に繋がる可能性があります。ユーザーがアプリを楽しめるように、適度な広告表示頻度を調節しましょう。
