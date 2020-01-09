# 初期化

広告のロード前に、`AdLime` の `initWithAppId` メソッドを呼び出し、 AdLime SDK の初期化を行ってください。この処理はアプリ起動後できるだけ早く実行する必要があり、アプリ起動時に実行することを強く推奨します。またこの処理は1回だけ実行してください。

## テスト環境での実行方法
テスト広告を利用する場合は `AdLime` の `setTestMode` を `YES` に設定してください。またAdLime SDK のデバッグログを確認する場合は `AdLime` の `setLogEnable` を `YES` に設定してください。広告のロードに失敗した場合、広告の詳細なエラーがデバッグログに出力されます。

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

## サンプルコード
AppDelegated の initWithAppId メソッドを呼び出す方法を下記に示します。

:::: tabs

::: tab Objective-C

```objectivec

@import AdLimeSdk;
// Facebookをテスト環境で利用する場合
// @import FBAudienceNetwork;

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [AdLime initWithAppId:@"YOUR APP ID"];

    // テスト環境で用いる場合は以下をテストモードを設定してください 
    [AdLime setTestMode: YES];
     // デバッグログを表示する場合は以下を設定してください
    [AdLime setLogEnable: YES];

    // Facebookをテスト環境で利用する場合は以下を設定してください
    // [FBAdSettings addTestDevice: [FBAdSettings testDeviceHash]];

    return YES;
}

@end
```

:::

::: tab Swift

```swift

import AdLimeSdk
// Facebookをテスト環境で利用する場合
// import FBAudienceNetwork

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        ...
        AdLime.initWithAppId("YOUR APP ID")

        // テスト環境で用いる場合は以下をテストモードを設定してください
        AdLime.setTestMode(true)
        // デバッグログを表示する場合は以下を設定してください
        AdLime.setLogEnable(true)

        // Facebookをテスト環境で利用する場合は以下を設定してください
        // FBAdSettings.addTestDevice(FBAdSettings.testDeviceHash())

        return true
    }
    ...

}

```

:::

:::: 

## テスト用の広告枠
iOS の各広告フォーマットのテスト用広告ユニット ID は、以下の通りです。

テストアプリ ID: 1e68d89e-ee81-47bc-ab4b-f79c09e5c561

| 広告フォーマット          | テスト広告ユニット ID                 |
|:---------------------- |:------------------------------------- |
|バナー                   |57be18f5-7030-4a46-8fc9-49b4abbd2438   |
|インタースティシャル       |875f429e-19a3-49d3-ae90-79f55bf81ef8   |
|ネイティブ                |3f733527-5202-4869-b148-73962fadbb88   |
|動画リワード              |f5f0cdb5-b18f-4e56-82f4-00d5238b31b0   |


## SDK の例
各広告の実装について、[SDKの例](https://github.com/Ham-mer/AdLime-iOS-Demo)をご覧ください 。