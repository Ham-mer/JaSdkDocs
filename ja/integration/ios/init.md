# 初期化

広告を読み込む前に、AdLime の initWithAppId: メソッドを呼び出し、 AdLime SDK の初期化を行ってください。この処理は1回だけ実行します。アプリの起動時に実行することが望ましく、できるだけ早く呼び出す必要があります。

## サンプルコード
AppDelegated の initWithAppId: メソッドを呼び出す方法を下記に示します。

```objectivec
@import AdLimeSdk;

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [AdLime initWithAppId:@"YOUR APP ID"];

    return YES;
}

@end
```

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