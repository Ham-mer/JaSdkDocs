#  MixFullScreenAd
インタースティシャル広告の場合に、普通のNetworkはインタースティシャル広告しか使えない。広告のfill率は低い場合に、広告は展示されない。MixFullScreenAdで広告をリクエストする時に、インタースティシャルだけではなく、バナー、ネイティブ、フィードリストもリクエストできる そうすると、広告容器のfill率とマネタイズ能力を高める。

MixFullScreenAdは今バナー、ネイティブ、インタースティシャルをサポートする。

本ガイドは MixFullScreenAd広告をIOS アプリに組み込むについて紹介する。

## 前提条件
- AdLime SDKの導入

## MixFullScreenAdの作成
MixFullScreenAd はMixFullScreenAdのオブジェクトでリクエストと展示され 。まずはMixFullScreenAdを実例化してAdunit IDを設置する。

```objectivec
@import AdLimeSdk;

@interface ViewController ()

@property(nonatomic, strong) AdLimeMixFullScreenAd *mixFullScreenAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    self.mixFullScreenAd = [[AdLimeMixFullScreenAd alloc] initWithAdUnitId:@"AdUnit_ID"];
}

@end
```

## 広告タイプの設置
広告をロードする前に、ネイティブ、、フィードリストのレイアウトを設置する。

```java
AdLimeNativeAdLayout *layout = [AdLimeNativeAdLayout getFullLayout1];
[self.mMixFullScreenAd setNativeAdLayout:layout];
```

**NativeAdLayoutについて [AdLimeNativeAdLayout](https://www.adlime.net/docs/ja/integration/ios/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できる。**

## 広告ロード
MixFullScreenAd をロードするために， MixFullScreenAd のオブジェクトの loadAd() 方法を使ってください

```objectivec
[self.mixFullScreenAd loadAd];
```

## 広告展示
MixFullScreenAdを展示するために，isReady() で広告のロードを確認して方 show()を調達する。
```objectivec
if([self.mixFullScreenAd isReady]) {
    [self.mixFullScreenAd showFromViewController:self];
}
```

## 広告イベント
AdLimeMixFullScreenAdDelegateで広告のライフサイクルをモニターできる。例えば：広告のロードタイミング、ユーザがいつアプリを閉じるなど。

### MixFullScreen広告イベントのログイン
ネイティブ広告イベントをログインするために、 AdLimeMixFullScreenAd の delegateをAdLimeMixFullScreenAdDelegate協議のオブジェクトに設定する。 一般的には、AdLimeMixFullScreenAdを実現できるclassは代理classと認められる。この場合に、delegateをselfに設定する。

```objectivec
@import AdLimeSdk;

@interface ViewController () <AdLimeMixFullScreenAdDelegate>

@property(nonatomic, strong) AdLimeMixFullScreenAd *mixFullScreenAd;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    ...

    self.mixFullScreenAd.delegate = self;
}

@end
```

### MixFullScreen広告イベントの実現
AdLimeMixFullScreenAdDelegateでの方法は選ばれる。実現したい方法を選んで結構だ。 下記の例で各方法を実現してまたは情報をコンソールに記録される：

```objectivec
/// A MixFullScreen ad has loaded, and can be displayed.
- (void)adLimeMixFullScreenAdDidReceiveAd:(AdLimeMixFullScreenAd *)mixFullScreenAd {
    NSLog(@"AdLimeMixFullScreenAdDidReceiveAd");
}

/// The MixFullScreen ad request failed, and a new request can be sent.
- (void)adLimeMixFullScreenAd:(AdLimeMixFullScreenAd *)mixFullScreenAd didFailToReceiveAdWithError:(AdLimeAdError *)adError {
    NSLog(@"AdLimeMixFullScreenAd:didFailToReceiveAdWithError, errorCode is %d, errorMessage is %@",
            adError.getCode, adError.description);
}

/// The MixFullScreen ad was shown.
- (void)adLimeMixFullScreenAdWillPresentScreen:(AdLimeMixFullScreenAd *)mixFullScreenAd {
    NSLog(@"AdLimeMixFullScreenAdWillPresentScreen");
}

/// The MixFullScreen ad will cause the application to become inactive and open a new application.
- (void)adLimeMixFullScreenAdWillLeaveApplication:(AdLimeMixFullScreenAd *)mixFullScreenAd {
    NSLog(@"AdLimeMixFullScreenAdWillLeaveApplication");
}

/// The MixView ad did dismiss a full screen view.
- (void)adLimeMixFullScreenAdDidDismissScreen:(AdLimeMixFullScreenAd *)mixFullScreenAd {
    NSLog(@"AdLimeMixFullScreenAdDidDismissScreen");
}
```

### エラー情報
当広告ロード失敗の時に时，AdLimeMixFullScreenAdDelegateの AdLimeMixFullScreenAd:didFailToReceiveAdWithError: をコールバックする。 adError.getCode、adError.descriptionを使ってエラーコードとエラ情報を取れる。

エラーコードは AdLimeAdErrorCodeに定義される ：
|定義                           |説明     |
|:-----------------------------|:--------|
|ADLIME_ADERROR_INTERNAL_ERROR  | 内部エラー |
|ADLIME_ADERROR_INVALID_REQUEST | 無効リクエスト |
|ADLIME_ADERROR_NETWORK_ERROR   | ネットエラー |
|ADLIME_ADERROR_NO_FILL         | no fill   |
|ADLIME_ADERROR_TIMEOUT         | タイムアウト |

エラー情報は AdUnit 、Network 、LineItem を含める，例は下記通り：
```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```