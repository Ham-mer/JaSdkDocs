#  MixViewAd
MixViewAdは名前通り、単一の容器で違うタイプの広告を組み合わせて使う，例えば、もともとバナー広告しかリクエストできない容器は MixViewAdを使うとバナー広告だけではなく、ネイティブ広告もリクエストできる。 そうすると、この広告容器のフィルレートとマネタイズ能力は高めらる。


今ではMixViewAd はバナー、ネイティブをサポートする。

本ガイドではMixViewAdをIOSのアプリに組み込む方法を紹介する。

## 前提条件
- AdlimeのSDKの導入

## MixViewAdの作成
MixViewAd はMixViewAdの対象でリクエストと展示。まずはMixViewAdを実例化してAdunit IDを設置する。

```objectivec
@import AdLimeSdk;
@import UIKit;

@interface ViewController ()

@property(nonatomic, strong) AdLimeMixViewAd *mixViewAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.mixViewAd = [[AdLimeMixViewAd alloc] initWithAdUnitId:@"AdUnit_ID" rootViewController:self];
}

@end
```

## 広告のロード
MixViewAdをロードするために， MixViewAdのオブジェクトの loadAd() 方法を使ってください。

```objectivec
[self.mixViewAd loadAd];
```

## 広告イベント
AdLimeMixFullScreenAdDelegateで広告のライフサイクルをモニターできる。例えば：広告のロードタイミング、ユーザがいつアプリを閉じるなど。

### MixFullScreen広告イベントのログイン
ネイティブ広告イベントをログインするために、 AdLimeMixFullScreenAd の delegateをAdLimeMixFullScreenAdDelegate協議のオブジェクトに設定する。一般的には、AdLimeMixFullScreenAdを実現できるclassは代理classと認められる。この場合に、delegateをselfに設定する。

```objectivec
@import AdLimeSdk;

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

### MixFullScreen広告イベントの実現
AdLimeMixFullScreenAdDelegateでの方法は選ばれる。実現したい方法を選んで結構だ。 下記の例で各方法を実現してまたは情報をコンソールに記録される：

```objectivec
/// A MixView ad has loaded, and can be displayed.
- (void)adLimeMixViewAdDidReceiveAd:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdDidReceiveAd");
}

/// The MixView ad request failed, and a new request can be sent.
- (void)adLimeMixViewAd:(AdLimeMixViewAd *)mixViewAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"AdLimeMixViewAd:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@",
            adError.getCode, adError.description);
}

/// The MixView ad was shown.
- (void)adLimeMixViewAdWillPresentScreen:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdWillPresentScreen");
}

/// The MixView ad will cause the application to become inactive and open a new application.
- (void)adLimeMixViewAdWillLeaveApplication:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdWillLeaveApplication");
}

/// The MixView ad did dismiss a full screen view.
- (void)adLimeMixViewAdDidDismissScreen:(AdLimeMixViewAd *)mixViewAd {
    NSLog(@"AdLimeMixViewAdDidDismissScreen");
}
```

### エラー情報
当広告ロード失敗の時に时，AdLimeMixFullScreenAdDelegateの AdLimeMixFullScreenAd:didFailToReceiveAdWithError: をコールバックする。adError.getCode、adError.descriptionを使ってエラーコードとエラ情報を取れる。

エラーコードは AdLimeAdErrorCodeに定義される：
|定義                           |説明     |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | 無効リクエスト |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットエラー |
|ADLIME_ADERROR_NO_FILL         | no fill      |
|ADLIME_ADERROR_TIMEOUT         | タイムアウト |


エラー情報は AdUnit 、Network 、LineItem を含める，例は下記通り：
```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## 広告の展示
広告ロードされてユーザさんに展示されることしかない。<br>
MixViewAd のネイティブ広告とフィードリスト広告の外観は開発者のカスタムで設定できる。AdLime で提供される NativeAdLayoutで広告のレイアウトを管理できる、ネイティブ広告の UIView を含める。<br>
AdLimeMixViewAd の getAdViewで: すでにフィルされる広告のクリエイティブのUIViewを取れる。UIViewの外観は AdLimeNativeAdLayoutの要素と同じ。<br>
このUIViewをページの適当なところに追加してアプリはMixView広告を展示できる。 
**AdLimeNativeAdLayout の情報について[AdLimeNativeAdLayout](https://www.adlime.net/docs/ja/integration/ios/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できる。**

```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeMixViewAdDelegate>

@property(nonatomic, strong) AdLimeNativeAdLayout *layout;

@end

@implementation ViewController

- (void)adLimeMixViewAdDidReceiveAd:(AdLimeMixViewAd *)mixViewAd {
    AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getLargeLayout1WithWidth:360];
    UIView *adView = [mixViewAd getAdView:layout];
    [self.view addSubview:adView];
}

@end
```

作成されるAdLimeNativeAdLayoutをAdLimeMixViewAdに設定する，そうすると、AdLimeMixViewAdのgetAdView:を調達する時にlayoutのパラメーターは送れない。

```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeMixViewAdDelegate>

@property(nonatomic, strong) AdLimeMixViewAd *mixViewAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getLargeLayout1WithWidth:360];
    [self.mixViewAd setNativeAdLayout:layout];
}

- (void)adLimeMixViewAdDidReceiveAd:(AdLimeMixViewAd *)mixViewAd {
    UIView *adView = [mixViewAd getAdView];
    [self.view addSubview:adView];
}

@end
```