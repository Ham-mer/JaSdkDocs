# インタースティシャル広告

インタースティシャル広告とは、アプリ上にオーバーレイで表示されるフルスクリーン広告です。一般的にアプリの画面が切り替わるタイミング（アクティビティが切り替わるタイミングやゲームのステージが変わる合間）で表示されます。アプリにインタースティシャル広告が表示される場合、ユーザーは広告をタップしてリンク先 URL に移動するか、広告を閉じてアプリに戻るかを選ぶことができます。

このガイドは、インタースティシャル広告をiOSアプリに実装する方法について説明します。

## 前提条件
- AdLime SDK が導入済みであること

## インタースティシャル広告オブジェクトの作成
インタースティシャル広告は、 AdLimeInterstitialAd オブジェクトによってリクエストし、表示されます。このオブジェクトを使用するために、まず AdLimeInterstitialAd をインスタンス化し、広告ユニットIDを設定してください。以下のサンプルコードでは、 UIViewController の viewDidLoad メソッドで AdLimeInterstitialAd を作成する方法を記載します。

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

## 広告を読み込む
インタースティシャル広告を読み込むには、AdLimeInterstitialAd オブジェクトの loadAd: メソッドを実行します。

```objectivec
@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    [self.interstitialAd loadAd];
}

@end
```

## 広告を表示する
インタースティシャル広告は、アプリの流れが一時的に中断する自然なタイミング（ゲームのステージが変わる合間や一つのミッションが完了になった直後など）で表示することが相応しい形です。インタースティシャル広告を表示するには、 AdLimeInterstitialAd の isReady メソッドで読み込みが完了したかどうかを確認し、 showFromViewController: を呼び出してください。以下のサンプルでは、
UIViewController のメソッドでこの操作を行う仕方について説明します。

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

## 広告イベント
AdLimeInterstitialAdDelegate によって、広告を閉じたとき、またユーザーがアプリから離れたときなど、広告のライフサイクルイベントを受け取ることができます。

### インタースティシャル広告イベントの登録
インタースティシャル広告イベントを登録するには、 AdLimeInterstitialAd の AdLimeInterstitialAdDelegate プロパティを設定します。 通常、インタースティシャル広告を実装するクラスが、デリゲート クラスとしての役割を担うので、 delegate プロパティを self に設定します。

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

### インタースティシャル広告イベントを実装する
AdLimeInterstitialAdDelegate の各メソッドは必須ではないため、必要なメソッドだけを実装するかたちで問題はありません。以下のサンプルでは、各メソッドを実装し、コンソールにログを出力します。

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

### エラーの情報
広告の読み込みに失敗した場合は、 AdLimeInterstitialAdDelegate の adLimeInterstitial:didFailToReceiveAdWithError: が呼び出されます。 その際に adError.getCode 、 adError.description から、エラーコード、エラー情報が取得できます。

AdLimeAdErrorCode  エラーコード一覧
|定義                           |説明    |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | リクエストが無効 |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットワークエラー |
|ADLIME_ADERROR_NO_FILL         | 配信できる広告がない    |
|ADLIME_ADERROR_TIMEOUT         | リクエスト　タイムアウト |

エラーは AdUnit、ネットワーク、ラインアイテムの各情報が含まれています。

```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## インタースティシャル広告を再読み込みする
インタースティシャル広告を一度表示した後に、別のインタースティシャル広告をリクエストする適切なタイミングは、 AdLimeInterstitialAdDelegate の adLimeInterstitialDidDismissScreen メソッド内で行います。このメソッドでは、表示していたインタースティシャル広告を閉じると同時に、次のインタースティシャル広告の読み込みを開始することができます。

```objectivec
- (void)adLimeInterstitialDidDismissScreen:(AdLimeInterstitialAd *)interstitialAd {
    [self.interstitialAd loadAd];
}
```

## 推奨事項
### インタースティシャル広告がアプリに適しているかどうか確認してください。

インタースティシャル広告は、画面の切り替わりがあるアプリに適しています。
このような移行ポイントは、画像の共有やゲームステージのクリアなど、アプリで特定のタスクが完了した際に発生します。ユーザーはこのタイミングで中断が入ることを想定しているので、インタースティシャル広告を表示してもユーザーエクスペリエンスに悪影響を及ぼすことはありません。アプリケーション・プロセスの、どの時点でインタースティシャル広告を表示するか、またユーザーがそれにどう反応するかを共に考慮に入れてください。


### インタースティシャル広告を表示する際には、必ず操作を一時停止してください。

インタースティシャル広告には、テキスト・イメージ・動画など様々な種類があります。インタースティシャル広告を表示する際に、アプリのリソースを一時停止させることが極重要です。たとえば、インタースティシャル広告を呼び出した後、アプリの音声出力を一時停止させてください。音声出力は、イベントハンドラ adLimeInterstitialDidDismissScreen によって再開できます。このハンドラは、ユーザーが広告に対する操作を完了した後に呼び出されます。また、広告を表示している間は、複雑な計算処理（ゲームループなど）も一時停止させてください。こうすることで、画像の読み込みが遅くなり、あるいは反応しなくなったり、動画が頻繁に途切れたりするリスクが低くなります。

### 十分な読み込み時間を確保してください。

インタースティシャル広告を適切なタイミングで表示することも大事ですが、それと同様に読み込みの待ち時間を短くすることも重要です。 showFromViewController を呼び出す前に、 loadAd を実行してください。こうすることで表示前の段階で、インタースティシャル広告の読み込みを完了させることができます。

### 過度に広告を表示しないように注意してください。

インタースティシャル広告の表示頻度を増やすことで収益の向上が見込めますが、それが原因でユーザーの体験が損なわれ、クリック率の低下につながる可能性もあります。ユーザーがアプリでの体験を楽しめるように、適度な広告表示頻度に調節しましょう。

### adLimeInterstitialDidReceiveAd イベントを使用して、インタースティシャル広告を表示しないでください。

このイベントを使用すると、ユーザーエクスペリエンスの低下につながる場合があります。代わりに、表示が必要になる前にあらかじめ広告を読み込み、 AdLimeInterstitialAd の isReady メソッドをチェックし、表示の準備ができているかどうかを確認してください。
