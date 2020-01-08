# バナー広告
バナー広告とは、アプリのレイアウトにおいて特定の位置を占める矩形のイメージまたはテキスト広告です。バナー広告は、一定時間が経過すると自動的に広告を更新することが特徴の一つです。モバイル広告を初めて掲載する場合は、まずバナー広告から始めてみましょう。

このガイドでは バナー広告 を iOS のアプリに実装する方法を説明します

## 前提条件
- AdLime SDK が導入済みであること

## AdLimeBannerView の作成
バナー広告は `AdLimeBannerView` オブジェクト内に表示されます。バナー広告を表示するためにまずUIViewに `AdLimeBannerView` を追加してください。この追加方法は Interface Builder もしくはコードによって組み込むことができます。


### Interface Builder で作成する
一般的なクラシックビューと同様に、 AdLimeBannerView をストーリーボードと xib ファイルに追加することができます。このメソッドを使用する場合、表示する広告のサイズに合わせて幅と高さの制限を設ける必要があります。例えば、320 x 50 のバナー広告を表示する場合、 320 ポイントの幅制約と 50 ポイントの高さ制約を設けてください。

### コードで作成する
AdLimeBannerView を直接インスタンス化することもできます。以下のサンプルでは、AdLimeBannerView を生成して、画面に追加する例を示します。


:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;

@interface ViewController ()

@property(nonatomic, strong) AdLimeBannerView *bannerView;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    // Instantiate the banner with AdUnitId and ViewController
    self.bannerView = [[AdLimeBannerView alloc] initWithAdUnitId:@"AdUnit_ID" rootViewController:self];

    [self.view addSubview:self.bannerView];
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
import UIKit

class ViewController: UIViewController {
    var bannerView: AdLimeBannerView!

    override func viewDidLoad() {
        super.viewDidLoad()
        self.bannerView = AdLimeBannerView.init(adUnitId: "AdUnit_ID")
    }
}
```

:::

::::


## 広告のロード
`AdLimeBannerView` オブジェクトを生成したら次に広告をロードしてみましょう。 `AdLimeBannerView` クラス の `loadAd` を実行してださい。

:::: tabs

::: tab Objective-C

```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    [self.bannerView loadAd];
}
```

:::

::: tab Swift

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    ...
    self.bannerView.loadAd()
}
```

:::

::::


## 広告イベント
`AdLimeBannerViewDelegate` を設定することで、広告のロード完了のタイミングやユーザーがアプリを閉じたタイミングなどの広告のライフサイクルイベントを取得することができます。

### バナー広告イベントを登録する
バナー広告のライフサイクルイベントを取得するためには `AdLimeBannerViewDelegate` を継承します。通常、`AdLimeBannerView`を実装するクラスがデリゲートクラスとなる場合が多いので、本ガイドでは `delegate` プロパティを `self` に設定します。

:::: tabs

::: tab Objective-C

```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeBannerViewDelegate>

@property(nonatomic, strong) AdLimeBannerView *bannerView;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    self.bannerView.delegate = self;
}

@end
```

:::

::: tab Swift

```swift
import AdLimeSdk
class ViewController: UIViewController, AdLimeBannerViewDelegate {
   var bannerView: AdLimeBannerView! 

    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        self.bannerView.delegate = self
    }
}
```

:::

::::


### バナー広告イベントを実装する
広告のイベントの制御は `AdLimeBannerViewDelegate` を用いて実現できます。以下のサンプルでは、各メソッドを実装し、コンソールにログを出力します。

:::: tabs

::: tab Objective-C

```objectivec
/// Tells the delegate an ad request loaded an ad.
- (void)adLimeBannerDidReceiveAd:(AdLimeBannerView *)bannerView {
    NSLog(@"adLimeBannerDidReceiveAd");
}

/// Tells the delegate an ad request failed.
- (void)adLimeBanner:(AdLimeBannerView *)bannerView didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"adLimeBanner:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@",
            adError.getCode, adError.description);
}

/// Tells the delegate that a full-screen view will be presented in response to the user clicking on an ad.
- (void)adLimeBannerWillPresentScreen:(AdLimeBannerView *)bannerView {
    NSLog(@"adLimeBannerWillPresentScreen");
}

/// Tells the delegate that a user click will open another app (such as the App Store), backgrounding the current app.
- (void)adLimeBannerWillLeaveApplication:(AdLimeBannerView *)bannerView {
    NSLog(@"adLimeBannerWillLeaveApplication");
}

/// Tells the delegate that the full-screen view has been dismissed.
- (void)adLimeBannerDidDismissScreen:(AdLimeBannerView *)bannerView {
    NSLog(@"adLimeBannerDidDismissScreen");
}
```

:::

::: tab Swift

```swift
// MARK: Banner広告に関するメソッド
/// Tells the delegate an ad request loaded an ad.
func adLimeBannerDidReceiveAd(_ bannerView: AdLimeBannerView!) {
    print("adLimeBannerDidReceiveAd")
}

/// Tells the delegate an ad request failed.
func adLimeBanner(_ bannerView: AdLimeBannerView!, didFailToReceiveAdWithError adError: AdLimeAdError!) {
    print("adLimeBanner:didFailToReceiveAdWithError, errorCode is \(adError.getCode().rawValue), errorMessage is \(adError.description)")
}

/// Tells the delegate that a full-screen view will be presented in response to the user clicking on an ad.
func adLimeBannerWillPresentScreen(_ bannerView: AdLimeBannerView!) {
    print("adLimeBannerWillPresentScreen")
}

func adLimeBannerWillLeaveApplication(_ bannerView: AdLimeBannerView!) {
    print("adLimeBannerWillLeaveApplication")
}

/// Tells the delegate that the full-screen view has been dismissed.
func adLimeBannerDidDismissScreen(_ bannerView: AdLimeBannerView!) {
    print("adLimeBannerDidDismissScreen")
}
```

:::

::::

### エラー情報
広告のロードに失敗した場合は、`AdLimeBannerViewDelegate` の  `adLimeBanner:didFailToReceiveAdWithError` が呼び出されます。`adError.getCode` 、`adError.description` を用いてエラーコードとエラー情報を取得できます。

AdLimeAdErrorCode エラーコード一覧
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

## バナーのサイズ

### バナーのサイズ設定
バナー広告の広告枠を作成する時に、サイズを設定することができます。以下はサイズ一覧になります。

サイズ（ポイント) |説明               |対応端末    |
|:-------------|:-----------------|:----------|
|320 x 50        |バナー      　      |スマートフォン・タブレット |
|320 x 100       |バナー（大）        |スマートフォン・タブレット |
|300 x 250       |IABレクタングル（中）|スマートフォン・タブレット |
|468 x 60        |IAB フルサイズバナー |タブレット |
|728 x 90        |IAB ビッグバナー    |タブレット |
|smart         |スマートバナー       |スマートフォン・タブレット |

### スマートバナー
スマートバナーは、画面のサイズや向きにかかわらず、横幅いっぱいに広告が表示されます。現在は一部の広告プラットフォームのみに対応しています。

**注意：広告を配置するコンテナのサイズは、バナーのサイズと同じにする必要があります。**