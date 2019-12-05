# バナー広告
バナー広告とは、アプリのレイアウトにおいて特定の位置を占める矩形のイメージまたはテキスト広告です。この種の広告は、ユーザーがアプリを操作している間にスマホ画面に残り、一定の時間が経過すると自動的に更新することが特徴です。モバイル広告を初めて掲載する場合は、まずバナー広告から始めることが最適です。

このガイドは、AdLime バナー広告を iOS アプリに実装する方法について説明します。コードスニペットと設定方法のほか、バナー広告のサイズに関する情報も紹介します。

## 前提条件
- AdLime SDK が導入済みであること

## AdLimeBannerView の作成
バナー広告は AdLimeBannerView オブジェクトに表示されるため、バナー広告を取り組ませるために、まずビューに AdLimeBannerView を追加してください。この操作は、一般的にインターフェス ビルダーかプログラミングなどの方法によって行われます。

### Interface Builder で作成する
一般的なクラシックビューと同様に、 AdLimeBannerView をストーリーボードと xib ファイルに追加することができます。このメソッドを使用する場合、表示する広告のサイズに合わせて幅と高さの制限を設ける必要があります。例えば、320 x 50 のバナー広告を表示する場合、 320 ポイントの幅制約と 50 ポイントの高さ制約を設けてください。

### コードで作成する
AdLimeBannerView を直接インスタンス化することもできます。以下のサンプルでは、AdLimeBannerView を生成して、画面に追加する例を示します。

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

## 広告を読み込む
AdLimeBannerView を作成したら、次に広告を読み込みます。 AdLimeBannerView クラス の loadAd を実行してださい。

```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    [self.bannerView loadAd];
}
```
これでアプリにバナー広告を表示できるようになりました。

## 広告イベント
AdLimeBannerViewDelegate によって、広告が閉じられたとき、またユーザーがいつアプリから離れたときなどのライフサイクルイベントを受け取ることができます。

### バナー広告イベントを登録する
バナー広告イベントを登録するには、AdLimeBannerView の AdLimeBannerViewDelegate プロパティを設定します。通常、バナー広告を実装するクラスがデリゲート クラスとしての役割を果たすので、 delegate プロパティを self に設定します。

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

### バナー広告イベントを実装する
AdLimeBannerViewDelegate メソッドを実装します。以下のサンプルでは、各メソッドでコンソールにメッセージを出力します。

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

### エラー
広告の読み込みに失敗した場合は、AdLimeBannerViewDelegate の adLimeBanner:didFailToReceiveAdWithError: がコールされます。 その際に adError.getCode、adError.description から、エラーコード、エラー情報が取得できます。

AdLimeAdErrorCode エラーコード一覧
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

**注意：広告を配置するコンテナのサイズは、バナーのサイズと同じか、それ以上の大きさにする必要があります。コンテナにパディングがある場合は、それだけバナーを表示できるコンテナの領域が小さくなります。**