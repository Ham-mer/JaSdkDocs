# 動画リワード広告
動画リワード広告とは、アプリ内で使用可能な報酬をユーザーに付与する代わりに、動画広告を最後までフルスクリーン表示する広告です。
このガイドでは 動画リワード広告 を iOS のアプリに実装する方法を説明します

## 前提条件
- AdLime SDK が導入済みであること

## 動画リワード広告の作成
広告を表示するまでのサイクルは `AdLimeRewardedVideoAd` オブジェクトを用いて広告をリクエストし、広告を表示することです。広告を表示するための最初のステップとして AdUnit ID を設定した `AdLimeRewardedVideoAd` を生成します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;

@interface ViewController ()

@property(nonatomic, strong) AdLimeRewardedVideoAd *rewardedVideoAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.rewardedVideoAd = [[AdLimeRewardedVideoAd alloc] initWithAdUnitId:@"AdUnit_ID"];
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController {
    var rewardedVideoAd: AdLimeRewardedVideoAd!

    override func viewDidLoad() {
        super.viewDidLoad()
        self.rewardedVideoAd = AdLimeRewardedVideoAd.init(adUnitId: "AdUnit_ID")
    }
}
```

:::

::::



## 広告のロード
`AdLimeRewardedVideoAd` オブジェクトを生成したら広告をロードしてみましょう。広告ロード完了のタイミングは後に紹介する `AdLimeRewardedVideoAdDelegate` の `adLimeRewardedVideoDidReceiveAd` を用いることで取得できます。

:::: tabs

::: tab Objective-C

```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    [self.rewardedVideoAd loadAd];
}
```

:::

::: tab Swift

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    ...
    self.rewardedVideoAd.load()
}
```

:::

::::


## 広告の表示
動画リワード広告を表示する前に、広告のコンテンツを視聴して報酬を受け取るかどうか、明確な選択肢をユーザーに提示する必要があります。動画リワード広告は、必ずユーザーの許可を受けてから表示しなければなりません。

動画広告を表示する前に広告がロード済みかどうかを `isReady` メソッドで確認してから `AdLimeRewardedVideoAd` の `show` で表示します。

:::: tabs

::: tab Objective-C

```objectivec
@implementation ViewController

    - (IBAction)doSomething:(id)sender {
        ...

        if([rewardedVideoAd isReady]) {
            [self.rewardedVideoAd showFromViewController:self];
        } else {
            NSLog(@"Ad wasn't ready");
        }
    }

@end
```

:::

::: tab Swift

```swift
class ViewController: UIViewController {
    @IBAction func doSomething(sender: Any) {
        if(self.rewardedVideoAd.isReady()) {
            self.rewardVideoAd.show(from: self)
        } else {
            print("Ad wasn't ready")
        }
    }
}
```

:::

::::


## 動画リワード広告イベント

`AdLimeRewardedVideoAdDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。


### 動画リワード広告イベントを登録する

動画リワード広告のライフサイクルイベントを取得するためには `AdLimeRewardedVideoAdDelegate` を継承します。通常、`AdLimeRewardedVideoAd` を実装するクラスがデリゲートクラスとなる場合が多いので、本ガイドでは `delegate` プロパティを `self` に設定します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeRewardedVideoAdDelegate>

@property(nonatomic, strong) AdLimeRewardedVideoAd *rewardedVideoAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    self.rewardedVideoAd.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
class ViewController: UIViewController, AdLimeRewardedVideoAdDelegate {
    var rewardedVideoAd: AdLimeRewardedVideoAd!

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        self.rewardedVideoAd.delegate = self
    }
}
```

:::

::::


### 動画リワード広告イベントを実装する
広告のイベントの制御は `AdLimeRewardedVideoAdDelegate` を用いて実現できます。以下のサンプルでは、各メソッドを実装し、コンソールにログを出力します。

:::: tabs

::: tab Objective-C

```objectivec
/// Tells the delegate an ad request succeeded.
- (void)adLimeRewardedVideoDidReceiveAd:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidReceiveAd");
}

/// Tells the delegate an ad request failed.
- (void)adLimeRewardedVideo:(AdLimeRewardedVideoAd *)rewardedVideoAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"adLimeRewardedVideo:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@",
        adError.getCode, adError.description);
}

/// Tells the delegate that the rewarded ad was presented.
- (void)adLimeRewardedVideoDidOpen:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidOpen");
}

/// Tells the delegate that the rewarded ad was dismissed.
- (void)adLimeRewardedVideoDidClose:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidClose");
}

/// Tells the delegate that the rewarded video was began play.
- (void)adLimeRewardedVideoDidStart:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidStart");
}

/// Tells the delegate that the rewarded video was finished play.
- (void)adLimeRewardedVideoDidComplete:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidComplete");
}

/// Tells the delegate that the user earned a reward.
- (void)adLimeRewardedVideo:(AdLimeRewardedVideoAd *)rewardedVideoAd didReward:(AdLimeRewardItem *)item {
    NSLog(@"adLimeRewardedVideo:didReward, rewardItem type is %@, amount is %d",
        item.rewardType, item.rewardAmount);
}

/// Tells the delegate that the user failed to earned a reward.
- (void)adLimeRewardedVideoDidFailedToReward:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidFailedToReward");
}

/// Tells the delegate that a user click will open another app (such as the App Store), backgrounding the current app.
- (void)adLimeRewardedVideoWillLeaveApplication:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoWillLeaveApplication");
}
```

:::

::: tab Swift

```swift
/// Tells the delegate an ad request succeeded.
func adLimeRewardedVideoDidReceive(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidReceiveAd")
}

/// Tells the delegate an ad request failed.
func adLimeRewardedVideo(_ rewardedVideoAd: AdLimeRewardedVideoAd!, didFailToReceiveAdWithError adError: AdLimeAdError!) {
    print("adLimeRewardedVideo:didFailToReceiveAdWithError, errorCode is \(adError.getCode().rawValue), errorMessage is \(adError.description)")
}

/// Tells the delegate that the rewarded ad was presented.
func adLimeRewardedVideoDidOpen(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidOpen")
}

/// Tells the delegate that the rewarded ad was dismissed.
func adLimeRewardedVideoDidClose(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidClose")
}

/// Tells the delegate that the rewarded video was began play.
func adLimeRewardedVideoDidStart(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidStart")
}

/// Tells the delegate that the rewarded video was finished play.
func adLimeRewardedVideoDidComplete(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidComplete");
}

/// Tells the delegate that the user earned a reward.
func adLimeRewardedVideo(_ rewardedVideoAd: AdLimeRewardedVideoAd!, didReward item: AdLimeRewardItem!) {
    if let item = item {
        print("リワード付与完了しました, リワードのタイプ： \(String(describing: item.rewardType)), リワードの量： \(item.rewardAmount) \n")
    } else {
        print("リワード付与完了しました, リワードはnilです\n")
    }
}

/// Tells the delegate that the user failed to earned a reward.
func adLimeRewardedVideoDidFailed(toReward rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidFailedToReward")
}

/// Tells the delegate that a user click will open another app (such as the App Store), backgrounding the current app.
func adLimeRewardedVideoWillLeaveApplication(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoWillLeaveApplication")
}
```

:::

::::


### エラー情報

広告のロードに失敗した場合は、`AdLimeRewardedVideoAdDelegate` の  `adLimeRewardedVideo:didFailToReceiveAdWithError:` が呼び出されます。 `adError.getCode`、`adError.description` を用いてエラーコードとエラー情報を取得できます。

AdLimeAdErrorCode エラーコード一覧
|定義                           |説明    |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | リクエストが無効 |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットワークエラー |
|ADLIME_ADERROR_NO_FILL         | 配信できる広告がない    |
|ADLIME_ADERROR_TIMEOUT         | リクエスト タイムアウト |

エラーには 広告ユニットID(AdUnit)、広告ネットワーク名(Network)、広告のプロパティ(LineItem)が含まれます。

```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

### リワード情報

下記は `RewardedVideoAd.RewardItem` クラスのリワード情報メソッド一覧です。

|メソッド名  |型          | 説明        |
|----------|------------|-------------|
|getType   | String     |リワードタイプ |
|getAmount | int        | リワード数    |

## 動画リワード広告を再リクエストする

動画リワード広告を表示後、新たに動画リワード広告のリクエストするための適切なタイミングは表示している動画リワード広告を閉じたタイミングです。具体的には `AdLimeRewardedVideoAdDelegate` の `adLimeRewardedVideoDidClose` メソッド内で次の動画リワード広告のロードを開始することができます。

:::: tabs

::: tab Objective-C

```objectivec
- (void)adLimeRewardedVideoDidClose:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    [self.rewardedVideoAd loadAd];
}
```

:::

::: tab Swift

```swift
func adLimeRewardedVideoDidClose(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    self.rewardedVideoAd.load()
}
```

:::

::::
