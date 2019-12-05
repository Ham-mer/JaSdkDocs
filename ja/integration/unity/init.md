# 初期化

広告を読み込む前に、 AdLimeSdk.Init() を呼び出し（AdLime 管理画面で登録したアプリ ID で）、アプリの AdLime SDK を初期化します。この処理は1回だけ実行します。(アプリの起動時に実行することが望ましい)
GameObject スクリプトに添付される Start() メソッドで Init() を呼び出す方法は下記通りです。

## コードの例
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    public void Start()
    {
        #if UNITY_ANDROID
            string appId = "Android App ID";
        #elif UNITY_IPHONE
            string appId = "iOS App ID";
        #else
            string appId = "unexpected_platform";
        #endif

        // GDPRの設定
        AdLimeSdk.SetGdprConsent(true);
        // 初期化
        AdLimeSdk.Init(appId);
    }
}
```

※ 注意 : プラットフォームに応じた 広告ユニット ID を使用してください。Android の端末からリクエストを出す場合には、 Android 広告ユニット ID を使用してください。iOS の場合は iOS 広告ユニット IDを使用してください。

## テスト用の広告枠
Android と iOS の各広告フォーマットのテスト用広告ユニット ID は、以下の通りです。

- Android

    テストアプリ ID : 14fac732-0853-4f1e-83a4-77db7915fc62

    | 広告フォーマット          | テスト広告ユニット ID                 |
    |:---------------------- |:------------------------------------- |
    |バナー                   |e302ae32-d770-4635-9b2f-97fd024e059e   |
    |インタースティシャル       |ecc5a7d7-872b-4c6c-a042-6b0b311ccc04   |
    |ネイティブ                |444dd66b-af52-4fd1-9260-5559e7488432   |
    |動画リワード              |cca19625-d829-4902-8164-1e75a0e5e6f5   |

- iOS

    テストアプリ ID : 1e68d89e-ee81-47bc-ab4b-f79c09e5c561

    | 広告フォーマット          | テスト広告ユニット ID                 |
    |:---------------------- |:------------------------------------- |
    |バナー                   |57be18f5-7030-4a46-8fc9-49b4abbd2438   |
    |インタースティシャル       |875f429e-19a3-49d3-ae90-79f55bf81ef8   |
    |ネイティブ               |3f733527-5202-4869-b148-73962fadbb88   |
    |動画リワード              |f5f0cdb5-b18f-4e56-82f4-00d5238b31b0   |