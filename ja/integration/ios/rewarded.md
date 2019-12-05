# 動画リワード広告
動画リワード広告とは、ユーザーが動画を最後まで視聴することと引き換えに、アプリ内で報酬を獲得できる動画広告です。
このガイドは、動画リワード広告を AdLime から iOS アプリに導入する方法について説明します。

## 前提条件
- AdLime SDK が導入済みであること

## 動画リワード広告オブジェクトを作成する
動画リワード広告は AdLimeRewardedVideoAd オブジェクトによってリクエストし表示されます。このオブジェクトを使用するために、まず AdLimeRewardedVideoAd 実をインスタンス化し、広告ユニットIDを設定してください。
以下のサンプルコードでは UIViewController の viewDidLoad メソッドで AdLimeRewardedVideoAd を生成する方法を説明します。

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

## 動画の読み込み

動画を読み込むには、AdLimeRewardedVideoAd オブジェクト の loadAd メソッドを実行します。

```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    [self.rewardedVideoAd loadAd];
}
```

## 広告の表示
動画リワード広告を表示する前に、広告のコンテンツを視聴して報酬を受け取るかどうか、明確な選択肢をユーザーに提示する必要があります。動画リワード広告は、必ずユーザーの許可を受けてから表示しなければなりません。

動画を表示するには、AdLimeRewardedVideoAd クラス の isReady メソッド で広告の読み込みが完了したかどうかを確認して、showFromViewController: メソッドを実行します。

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

## 動画リワード広告イベント

広告のライフサイクルで発生する様々なイベント（読み込み、開始、終了など）を追加することができ、
AdLimeRewardedVideoAdDelegate クラスを使って、これらのイベントを受け取ることができます。

### 動画リワード広告イベントを登録する

動画リワード広告イベントを登録するには、 AdLimeRewardedVideoAd クラスの AdLimeRewardedVideoAdDelegate プロパティを設定します。通常、動画リワード広告を実装するクラスが、デリゲート クラスとしての役割も担うので、delegate プロパティを self に設定します。

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

### 動画リワード広告イベントを実装する
AdLimeRewardedVideoAdDelegate の各メソッドは必須ではないため、必要なメソッドだけを実装するかたちで問題はありません。以下のサンプルでは、各メソッドを実装し、コンソールにログを出力します。

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

### エラーの情報

広告の読み込に失敗した場合は、AdLimeRewardedVideoAdDelegate の AdLimeRewardedVideo:didFailToReceiveAdWithError: が呼び出されます。 その際に adError.getCode、adError.description から、エラーコード、エラー情報が取得できます。

AdLimeAdErrorCode エラーコード一覧
|定義                           |説明    |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | リクエストが無効 |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットワークエラー |
|ADLIME_ADERROR_NO_FILL         | 配信できる広告がない    |
|ADLIME_ADERROR_TIMEOUT         | リクエスト タイムアウト |

エラーは AdUnit 、ネットワーク、ラインアイテムの各情報が含まれています。

```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

### リワード情報

下記は RewardedVideoAd.RewardItem クラスのリワード情報メソッド一覧です。

|メソッド名  |型          | 説明        |
|----------|------------|-------------|
|getType   | String     |リワードタイプ |
|getAmount | int        | リワード数    |

## 動画リワード広告を再読み込みする

動画リワード広告を一度表示した後に、別の動画リワード広告をリクエストする適切なタイミングは、 AdLimeRewardedVideoAdDelegate の adLimeRewardedVideoDidClose のメソッド内になります。このメソッドでは、表示していた動画リワード広告を閉じると同時に、次の動画リワード広告の読み込みを開始することができます。

```objectivec
- (void)adLimeRewardedVideoDidClose:(AdLimeRewardedVideoAd *)rewardedVideoAd {
    [self.rewardedVideoAd loadAd];
}
```