# AdLime SDK の導入
"AdLimeSdk" を導入後は[メディエーション](./mediation.md)のガイドを参考にしてご希望の広告ネットワークを追加してください。 

## 前提条件
- Xcode 11.0 以上のバージョンを使用
- ターゲットバージョンを iOS 8.0 以上に設定
- AdLime アカウントを作成し、アプリが登録済み

## AdLimeSdk
### CocoaPods（推奨）
iOS プロジェクトに AdLime SDK を導入するための最も簡単な方法は CocoaPods を使用することです。プロジェクトの Podfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
pod 'AdLimeSdk'
```

コマンドラインから次のコマンドを実行してください:
```objectivec
pod install --repo-update
```

CocoaPods を初めてご利用の場合、 CocoaPods の[公式ドキュメント](https://guides.cocoapods.org/using/using-cocoapods)で Podfile の作成方法と使用方法をご確認ください。

### 手動ダウンロード
SDK フレームワークを直接ダウンロードして解凍し、下記のフレームワークを Xcode プロジェクトに導入してください。

- [AdLimeSdk.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeSdk/1.8.2.zip)
- AdLimeSdk.bundle

ドラッグ & ドロップ完了後、Build Phases > Copy Bundle Resources に AdLimeSdk.bundle が含まれていることを確認してください。

### Carthage
プロジェクトの Cartfile を開き、下記のコードをアプリのターゲットに追加してください。
```objectivec
github "Ham-mer/AdLimeSdk"
```

コマンドラインから次のコマンドを実行してください:
```sh
carthage update
```

Carthage フォルダを確認して、AdLimeSdk.frameworkとAdLimeSdk.bundleをXcodeプロジェクトに追加してください。ドラッグ & ドロップ完了後、Build Phases > Copy Bundle Resources に AdLimeSdk.bundle が含まれていることを確認してください。

## Linker Flags の追加
プロジェクトのBuild Settingsで、以下のように [Other Linker Flags] に -ObjC を追加します。

<img src="./../images/ios/begin_objc.png" height="140"/>

## App Transport Security
iOS 9 では、App Transport Security（ATS）というプライバシー機能が導入されました。この機能は新しいアプリでデフォルトで有効になり、安全な接続を要求します。

広告が ATS の影響を受けないようにするには、次の作業を行ってください：

NSAllowsArbitraryLoads の例外をアプリの Info.plist ファイルに追加して、ATS による制限を無効にします。

<img src="./../images/ios/begin_ats.png" height="60"/>

```objectivec
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```

## 初期化

広告のロード前に、AdLime の initWithAppId メソッドを呼び出し、 AdLime SDK の初期化を行います。この初期化の処理はできるだけ早く実行する必要があり、アプリ起動時に実行することを強く推奨します。また、この処理は1回だけ実行してください。

### テスト環境での実行方法
テスト広告を利用する場合は AdLime の setTestMode を YES に設定してください。また AdLime SDK のデバッグログを確認する場合は AdLime の setLogEnable を YES に設定してください。広告のロードに失敗した場合、広告の詳細なエラーがデバッグログに出力されます。

#### エラーメッセージとエラーコードについて

[エラー情報](./error.md#エラーコードとエラーメッセージ)を確認してください。


### サンプルコード
AppDelegated の initWithAppId メソッドを呼び出す方法を下記に示します。

:::: tabs

::: tab Objective-C

```objectivec

@import AdLimeSdk;

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [AdLime initWithAppId:@"YOUR APP ID"];

    // テスト環境で用いる場合はテストモードに設定してください 
    [AdLime setTestMode: YES];
     // デバッグログを表示する場合は以下を設定してください
    [AdLime setLogEnable: YES];

    // Network テストモード、アプリ公開時には false にする必要があります
    // [AdLime setNetworkTestMode:YES];
    // Network デバッグモード
    // [AdLime setNetworkDebugMode:YES];
    
    return YES;
}

@end
```

:::

::: tab Swift

```swift

import AdLimeSdk

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        ...
        AdLime.initWithAppId("YOUR APP ID")

        // テスト環境で用いる場合はテストモードに設定してください
        AdLime.setTestMode(true)
        // デバッグログを表示する場合は以下を設定してください
        AdLime.setLogEnable(true)

        // Network テストモード、アプリ公開時には false にする必要があります
        // AdLime.setNetworkTestMode(true)
        // Network デバッグモード
        // AdLime.setNetworkDebugMode(true)

        return true
    }
    ...

}

```

:::

::::


**各広告ネットワークがテストモードとデバッグモードをサポートするかは [テストモードとデバッグモードの設定](./test_debug_mode.md) で確認してください。**

## SDK の実装サンプル
各広告の実装サンプルについて、[デモアプリ](https://github.com/Ham-mer/AdLime-iOS-Demo)をご覧ください。

## 次のステップ
- 事前に導入予定の広告ネットワークが決定している場合は[メディエーション機能の導入](./mediation.md)を確認し、各広告ネットワークごとに必要な SDK の導入手順に従ってください。
- 広告ネットワークを選択せず、広告を表示したい場合は[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、iOS アプリに実装しましょう。


