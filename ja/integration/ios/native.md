# ネイティブ広告
ネイティブ広告は、プラットフォームに備わっている UI コンポーネントを通じて、ユーザーに表示される広告アセットです。ストーリーボードですでに使用しているクラスと同じクラスで表示され、アプリの視覚デザインに合わせて形式が調整されることがあります。広告が読み込まれる際は、アプリがその広告のアセットを含むオブジェクトを受け取り、（SDK ではなく）アプリがそのアセットの表示処理を実行します。他の広告フォーマットとは異なり、お客様ご自身が広告のデザインをカスタマイズすることはできません。
このガイドでは、AdLime SDK を使用して iOS アプリにネイティブ広告を実装する方法と、その過程で考慮すべき重要なポイントについて説明します。

## 前提条件
- AdLime SDK が導入済みであること

## ネイティブ広告の作成
ネイティブ広告は AdLimeNativeAd オブジェクトによってリクエストし、表示されます。まず AdLimeNativeAd をインスタンス化し、その広告ユニット ID を設定してください。
以下は UIViewController の viewDidLoad メソッドで AdLimeNativeAd を生成する方法を説明します。

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController ()

@property(nonatomic, strong) AdLimeNativeAd *nativeAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    nativeAd = [[AdLimeNativeAd alloc] initWithAdUnitId:@"AdUnit_ID"];
}

@end
```

## 広告レイアウトの作成
ネイティブ広告のデザインのカスタマイズやレイアウトは、コーディングによって行います。 AdLime SDK の AdLimeNativeAdLayout を使用し、レイアウトを行います。
以下のリストのように、 AdLimeNativeAdLayout は ネイティブ広告のための各 UIView が内包されています。

### AdLimeNativeAdLayout 要素一覧
| 要素               | タイプ     | 説明                           | 必須                         |
| ----------------- | --------- | ------------------------------ | --------------------------- |
| rootView          | UIView    | ルートビュー                     | 必須                         |
| titleLabel        | UILabel   | タイトル                        | 必須                          |
| subTitleLabel     | UILabel   | サブタイトル                     | 非必須                        |
| bodyLabel         | UILabel   | 本文                            | 非必須                       |
| advertiserLabel   | UILabel   | 広告主                          | 非必須                        |
| callToActionView  | UILabel   | アクションボタン                       | 必須                         |
| mediaView         | UIView    | 画像 / 動画                       | mediaView もしくは iconView どちらか1つ以上 |
| iconView          | UIView    | サイト/アプリのロゴ            | mediaView もしくは iconView どちらか1つ以上 |
| adChoicesView     | UIView    | 広告選択ビュー                        | 必須                          |
| ratingLabel       | UILabel   | アプリストアでの評価レート（例：4.5）   |非必須                         |
| priceLabel        | UILabel   | アプリストアの価格 （例：無料）    | 非必須                         |
| storeLabel        | UILabel   | アプリストアラベル                     | 非必須                         |
| ratingCallback    | callback  | 評価レートのカスタムコールバック     |非必須                         |

ratingCallback は、アプリストアでのアプリ評価レビューのカスタマイズを行えます。

```objectivec
typedef void (^ratingCallback)(double rating);
```

### UIView の生成
 レイアウトを作成する最初のステップとして、 UIView を生成します。

- Interface Builder で、任意の xib ファイル に UIView の追加を行う
- もしくは、UIView のサブクラスをカスタマイズし生成する

// xib ファイル の場合
```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    NSArray *nibViewArray = [[NSBundle mainBundle] loadNibNamed:@"XibNativeAdView" owner:nil options:nil];
    XibNativeAdView *nativeAdView = nibViewArray.firstObject;
}
```

// UIView のサブクラスをカスタマイズで生成する場合
```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    CustomNativeAdView *nativeAdView = [[CustomNativeAdView alloc] init];
}
```

### AdLimeNativeAdLayout の生成
UIView の生成したら、AdLimeNativeAdLayout を生成し、要素となる各 UIView の生成と設定を行います。 AdLimeNativeAdLayout を AdLimeNativeAd の NativeAdLayout として設定します。

```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    AdLimeNativeAdLayout *layout = [[AdLimeNativeAdLayout alloc] init];
    layout.rootView = nativeAdView;
    layout.titleLabel = nativeAdView.titleLabel;
    layout.bodyLabel = nativeAdView.bodyLabel;
    layout.advertiserLabel = nativeAdView.advertiserLabel;
    layout.callToActionView = nativeAdView.callToActionLabel;
    layout.mediaView = nativeAdView.mediaView;
    layout.iconView = nativeAdView.iconView;
    layout.adChoicesView = nativeAdView.adChoicesView;
    layout.ratingLabel = nativeAdView.ratingLabel;
    layout.ratingCallback = ^(double rating) {
        if (rating > 0) {
            // display the rating through stars
        } else {
            // don't display the rating
        }
    };
    
    [self.nativeAd setNativeAdLayout:layout];
}
```

### 広告インタラクティブエリアを設定する
広告のインタラクティブエリアを設定することにより、ネイティブ広告の各要素のクリック可否が設定できます。設定しない場合は、すべての要素をクリックが可能です。<br>
以下は、 AdLimeNativeAdLayout オブジェクトの AdLimeInteractiveArea を設定するサンプルコードです。

```
AdLimeNativeAdLayout *layout = [[AdLimeNativeAdLayout alloc] init];
...
layout.interactiveArea = AdLimeInteractiveArea.builder.addTitle.addBody.addCallToAction.addMediaView.addIcon;
...
```
上記の例では，指定した要素がインタラクティブエリアに含まれます
- タイトル・本文・アクションボタン・メディア・アイコン
.addXxx(Xxxは要素名) をコードに追加することで、インタラクティブエリアに要素を追加することになります。

## 広告を読み込む
AdLimeNativeAd を作成し、 AdLimeNativeAdLayout の設定が完了したら、ネイティブ広告の読み込みが可能です。
ネイティブ広告を読み込むには、 AdLimeNativeAd オブジェクトの loadAd メソッドを実行します。

```objectivec
@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    [self.nativeAd loadAd];
}

@end
```

## ネイティブ広告のイベント

広告のライフサイクルで発生する様々なイベント（読み込み、開始、終了など）を追加することができ、
AdLimeNativeAdDelegate クラスを使って、これらのイベントを受け取ることができます。

### ネイティブ広告イベントを登録する
ネイティブ広告イベントを登録するには、AdLimeNativeAd クラスの AdLimeNativeAdDelegate プロパティを設定します。通常、ネイティブ広告を実装するクラスが、デリゲート クラスとしての役割も担うので、delegate プロパティを self に設定します。


```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeNativeAdDelegate>

@property(nonatomic, strong) AdLimeNativeAd *nativeAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    self.nativeAd.delegate = self;
}

@end
```

### ネイティブ広告イベントを実装する

AdLimeNativeAdDelegate の各メソッドは必須ではないため、必要なメソッドだけを実装するかたちで問題はありません。以下のサンプルでは、各メソッドを実装し、コンソールにログを出力します。

```objectivec
/// A native ad has loaded, and can be displayed.
- (void)adLimeNativeAdDidReceiveAd:(AdLimeNativeAd *)nativeAd {
    NSLog(@"adLimeNativeAdDidReceiveAd");
}

/// The native ad request failed, and a new request can be sent.
- (void)adLimeNativeAd:(AdLimeNativeAd *)nativeAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"adLimeNativeAd:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@",
            adError.getCode, adError.description);
}

/// The native ad was shown.
- (void)adLimeNativeAdWillPresentScreen:(AdLimeNativeAd *)nativeAd {
    NSLog(@"adLimeNativeAdWillPresentScreen");
}

/// The native ad will cause the application to become inactive and open a new application.
- (void)adLimeNativeAdWillLeaveApplication:(AdLimeNativeAd *)nativeAd {
    NSLog(@"adLimeNativeAdWillLeaveApplication");
}

/// The native ad did dismiss a full screen view.
- (void)adLimeNativeAdDidDismissScreen:(AdLimeNativeAd *)nativeAd {
    NSLog(@"adLimeNativeAdDidDismissScreen");
}
```

### エラーの情報
広告の読み込に失敗した場合は、AdLimeNativeAdDelegate の adLimeNativeAd:didFailToReceiveAdWithError: が呼び出されます。 adError.getCode、 adError.description から、エラーコード、エラー情報が取得できます。

AdLimeAdErrorCode エラーコード一覧
|定義                           |説明    |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | リクエストが無効 |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットワークエラー |
|ADLIME_ADERROR_NO_FILL         | 配信できる広告がない    |
|ADLIME_ADERROR_TIMEOUT         | リクエスト　タイムアウト |

エラーには、AdUnit 、ネットワーク、ラインアイテムの各情報が含まれています。
```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## 広告を表示する
広告を読み込みが完了すれば、あとは表示をするだけです。
AdLimeNativeAd の getAdView メソッドで、カスタマイズした UIView が取得できます。 この UIView の各要素と AdLimeNativeAdLayout の要素は同じオブジェクトになります。
この UIView を適切な場所に追加することで、ネイティブ広告を表示することができます。

```objectivec
- (void)adLimeNativeAdDidReceiveAd:(AdLimeNativeAd *)nativeAd {
    UIView *adView = nativeAd.getAdView;
    [self.view addSubview:adView];
}
```

## 広告レイアウト作成の遅延
ネイティブ広告を読み込む前に AdLimeNativeAdLayout を作成するのではなく、ネイティブ広告の読み込み完了後に、AdLimeNativeAdLayout を作成することも可能です。

AdLimeNativeAd の getAdView: メソッドは、UIView を取得するとともに AdLimeNativeAdLayout を設定できます。なので AdLimeNativeAdLayout をあらかじめ生成する必要がありません。
以下はサンプルコードです。

```objectivec
- (void)adLimeNativeAdDidReceiveAd:(AdLimeNativeAd *)nativeAd {
    AdLimeNativeAdLayout *layout = [[AdLimeNativeAdLayout alloc] init];
    layout.rootView = nativeAdView;
    layout.titleLabel = nativeAdView.titleLabel;
    layout.bodyLabel = nativeAdView.bodyLabel;
    layout.advertiserLabel = nativeAdView.advertiserLabel;
    layout.callToActionView = nativeAdView.callToActionLabel;
    layout.mediaView = nativeAdView.mediaView;
    layout.iconView = nativeAdView.iconView;
    layout.adChoicesView = nativeAdView.adChoicesView;
    layout.ratingLabel = nativeAdView.ratingLabel;
    layout.ratingCallback = ^(double rating) {
        if (rating > 0) {
            // display the rating through stars
        } else {
            // don't display the rating
        }
    };

    UIView *adView = [nativeAd getAdView:layout];;
    
    [self.view addSubview:adView];
}
```

## ビルトイン ネイティブ広告レイアウト

AdLime SDK には様々な NativeAd レイアウトが用意されています。最適なレイアウトを活用し、開発の効率を上げることができます。

### 一般的な ネイティブ広告レイアウト

- カード小：`[AdLimeNativeAdLayout getSmallLayoutWithWidth:(CGFloat) frameWidth]`
rootViewの高さ：80

<img src="./../images/ios/native_style/1-1.png" width="360" align=center />

- カード中：`[AdLimeNativeAdLayout getMediumLayoutWithWidth:(CGFloat) frameWidth]`
rootViewの高さ：120

<img src="./../images/ios/native_style/1-2.png" width="360" align=center />

- カード大 1：`[AdLimeNativeAdLayout getLargeLayout1WithWidth:(CGFloat) frameWidth]`
rootViewの高さ：340

<img src="./../images/ios/native_style/1-3-1.png" width="360" align=center />

- カード大 2：`[AdLimeNativeAdLayout getLargeLayout2WithWidth:(CGFloat) frameWidth]`
rootViewの高さ：400

<img src="./../images/ios/native_style/1-3-2.png" width="360" align=center />


- カード大 3：`[AdLimeNativeAdLayout getLargeLayout3WithWidth:(CGFloat) frameWidth]`
rootViewの高さ：430

<img src="./../images/ios/native_style/1-3-3.png" width="360" align=center />

- カード大 4：`[AdLimeNativeAdLayout getLargeLayout4WithWidth:(CGFloat) frameWidth]`
rootViewの高さ：430

<img src="./../images/ios/native_style/1-3-4.png" width="360" align=center />


#### フルスクリーン ネイティブ広告レイアウト

- スタイル 1：`[AdLimeNativeAdLayout getFullLayout1]`

<img src="./../images/ios/native_style/2-1.png" width="270" align=center />


- スタイル 2：`[AdLimeNativeAdLayout getFullLayout2]`

<img src="./../images/ios/native_style/3-1.png" width="270" align=center />


- スタイル 3：`[AdLimeNativeAdLayout getFullLayout3]`

<img src="./../images/ios/native_style/4-1.png" width="270" align=center />

- スタイル 4：`[AdLimeNativeAdLayout getFullLayout4]`

<img src="./../images/ios/native_style/5-1.png" width="270" align=center />