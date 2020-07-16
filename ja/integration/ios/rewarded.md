# 動画リワード広告

動画リワード広告とは、アプリ内で使用可能な報酬をユーザーに付与する代わりに、動画広告を最後までフルスクリーン表示する広告です。ネイティブ広告やインタースティシャル広告など自動で再生する動画広告とは異なり、視聴を希望したユーザーにのみ動画広告を再生します。他の広告フォーマットに比べ広告効果が高いため、広告単価が高く、効果的に収益を得ることが可能です。

このガイドでは 動画リワード広告 を iOS のアプリに実装する方法を説明します。

## 前提条件
- AdLime SDK が導入済みであること

## 動画リワード広告の作成
広告を表示するまでのサイクルは `AdLimeRewardedVideoAd` オブジェクトを用いて広告をリクエストし、広告を表示することです。広告を表示するための最初のステップとして 広告枠 ID を設定した `AdLimeRewardedVideoAd` を生成します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController ()

@property(nonatomic, strong) AdLimeRewardedVideoAd *rewardedVideoAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.rewardedVideoAd = [[AdLimeRewardedVideoAd alloc] initWithAdUnitId:@"広告枠 ID"];
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
        self.rewardedVideoAd = AdLimeRewardedVideoAd.init(adUnitId: "広告枠 ID")
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

動画広告を表示する前に広告がロード済みかどうかを `isReady` メソッドで確認してから `AdLimeRewardedVideoAd` の `show` で表示します。展示する前に、getRewardItem でリワードの内容を取ってユーザーさんにお知らせします。下記の例でUIViewControllerでの流れを説明します。

:::: tabs

::: tab Objective-C

```objectivec
@implementation ViewController

    - (IBAction)doSomething:(id)sender {
        ...

        if([rewardedVideoAd isReady]) {
            // 広告を展示する前に、Dialogでリワードの内容をユーザーさんにお知らせることができます
            // AdLimeRewardItem *rewardItem = [self.rewardedVideoAd getRewardItem];
            // NSLog(@"RewardItem: %@", rewardItem);

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
            // 広告を展示する前に、Dialogでリワードの内容をユーザーさんにお知らせることができます
            // var rewardItem: AdLimeRewardItem! = self.rewardedVideoAd.getRewardItem()
            // NSLog(@"RewardItem: %@", rewardItem);

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
@import UIKit;

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
import UIKit

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
/// 広告が正しくロードされたことを通知するデリゲートメソッド
- (void)adLimeRewardedVideoDidReceiveAd:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidReceiveAd");
}

/// 広告のロード失敗を通知するデリゲートメソッド
- (void)adLimeRewardedVideo:(AdLimeRewardedVideoAd *)rewardedVideoAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"adLimeRewardedVideo:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@",
        adError.getCode, adError.description);
}

/// 動画リワード広告が表示されたことを通知するデリゲートメソッド
- (void)adLimeRewardedVideoDidOpen:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidOpen");
}

/// 動画リワード広告が閉じられたことを通知するデリゲートメソッド
- (void)adLimeRewardedVideoDidClose:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidClose");
}

/// 動画が開始したことを通知するデリゲートメソッド
- (void)adLimeRewardedVideoDidStart:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidStart");
}

/// 動画を最後まで視聴したことを通知するデリゲートメソッド
- (void)adLimeRewardedVideoDidComplete:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidComplete");
}

/// ユーザーがリワード（報酬）を獲得したことを通知するデリゲートメソッド
- (void)adLimeRewardedVideo:(AdLimeRewardedVideoAd *)rewardedVideoAd didReward:(AdLimeRewardItem *)item {
    NSLog(@"adLimeRewardedVideo:didReward, rewardItem type is %@, amount is %d",
        item.rewardType, item.rewardAmount);
}

/// ユーザーがリワード（報酬）の獲得に失敗したことを通知するデリゲートメソッド
- (void)adLimeRewardedVideoDidFailedToReward:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoDidFailedToReward");
}

/// ユーザーが広告をタップして外部リンク（App Storeなど）へ遷移したことを通知するデリゲートメソッド
- (void)adLimeRewardedVideoWillLeaveApplication:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    NSLog(@"adLimeRewardedVideoWillLeaveApplication");
}
```

:::

::: tab Swift

```swift
/// 広告が正しくロードされたことを通知するデリゲートメソッド
func adLimeRewardedVideoDidReceive(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidReceiveAd")
}

/// 広告のロード失敗を通知するデリゲートメソッド
func adLimeRewardedVideo(_ rewardedVideoAd: AdLimeRewardedVideoAd!, didFailToReceiveAdWithError adError: AdLimeAdError!) {
    print("adLimeRewardedVideo:didFailToReceiveAdWithError, errorCode is \(adError.getCode().rawValue), errorMessage is \(adError.description)")
}

/// 動画リワード広告が表示されたことを通知するデリゲートメソッド
func adLimeRewardedVideoDidOpen(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidOpen")
}

/// 動画リワード広告が閉じられたことを通知するデリゲートメソッド
func adLimeRewardedVideoDidClose(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidClose")
}

/// 動画が開始したことを通知するデリゲートメソッド
func adLimeRewardedVideoDidStart(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidStart")
}

/// 動画を最後まで視聴したことを通知するデリゲートメソッド
func adLimeRewardedVideoDidComplete(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidComplete");
}

/// ユーザーがリワード（報酬）を獲得したことを通知するデリゲートメソッド
func adLimeRewardedVideo(_ rewardedVideoAd: AdLimeRewardedVideoAd!, didReward item: AdLimeRewardItem!) {
    if let item = item {
        print("リワード付与完了しました, リワードのタイプ： \(String(describing: item.rewardType)), リワードの量： \(item.rewardAmount) \n")
    } else {
        print("リワード付与完了しました, リワードはnilです\n")
    }
}

/// ユーザーがリワード（報酬）の獲得に失敗したことを通知するデリゲートメソッド
func adLimeRewardedVideoDidFailed(toReward rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoDidFailedToReward")
}

/// ユーザーが広告をタップして外部リンク（App Storeなど）へ遷移したことを通知するデリゲートメソッド
func adLimeRewardedVideoWillLeaveApplication(_ rewardedVideoAd: AdLimeRewardedVideoAd!) {
    print("adLimeRewardedVideoWillLeaveApplication")
}
```

:::

::::


### 広告ロードエラーについて

広告のロードに失敗した場合は、`AdLimeRewardedVideoAdDelegate` の  `adLimeRewardedVideo:didFailToReceiveAdWithError:` が呼び出されます。 `adError.getCode`、`adError.description` を用いてエラーコードとエラーメッセージを取得できます。

#### エラーコードとエラーメッセージについて

[エラー情報](./error.md#エラーコードとエラーメッセージ)を確認してください。

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

## プリロードとキャッシュ

広告の表示の待ち時間は広告のインプレッション獲得に影響します。広告を事前にロードすることで広告が表示されるまでの待ち時間を短縮することを推奨します。またロードした広告を表示しないことは広告の eCPM を下げる原因となります。広告の表示がされたかどうかを管理し、表示しなかった広告をリサイクルして再度表示を試みることを推奨します。これらの推奨事項は、[AdLimeAdLoader](./adloader.md) によって実現が可能です。

## 次のステップ
- 他の広告フォーマットを追加で利用したい場合は[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、iOSアプリに実装しましょう。
- 広告が正しく表示できるか確認したい場合は[広告表示テスト](./test.md)に従い、App ID と各広告ネットワークに対応する広告フォーマットの広告枠 ID を設定して広告を表示してみましょう。
