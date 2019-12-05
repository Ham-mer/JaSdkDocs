# バナー
バナー広告は、アプリのレイアウト内の一部分を使用する長方形の画像かテキストの広告です。ユーザーがアプリを操作している間は画面に残り、一定の時間が経過すると自動的に更新されます。モバイル広告を初めて掲載する場合は、まずこの広告から始めるのが最適です。

このガイドでは、AdLime のバナー広告を Unity に組み込む方法について説明します。コード スニペットと設定方法のほか、バナーのサイズに関する情報も紹介します。

## 前提条件
- [スタートガイド](./begin.md)の手順を完了し、 AdLime Unity プラグインがインポート済みであること。
- [初期化](./init.md)の手順が完了済みであること

## バナーの作成
バナーを表示するための最初のステップは、 GameObject のスクリプトで BannerAd オブジェクトを作成します。 
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private BannerAd bannerAd;
    ...
    public void Start()
    {
        ...
        this.RequestBanner();
    }

    private void RequestBanner()
    {
        #if UNITY_ANDROID
            string adUnitId = "Android AdUnit ID";
        #elif UNITY_IPHONE
            string adUnitId = "iOS AdUnit ID";
        #else
            string adUnitId = "unexpected_platform";
        #endif

        // BannerAd作成
        bannerAd = new BannerAd(adUnitId);
        // 広告の座標設定
        bannerAd.SetPosition(BannerAdPosition.Top);
    }
}
```

※ 注意 : プラットフォームに応じた、広告ユニット ID を設定してください。Android の端末からリクエストを出す場合には、 Android 広告ユニット ID を使用します。iOS の場合は iOS 広告ユニット IDを使用します。


### 広告枠のカスタマイズ（非必須）

スクリーン上で BannerAd の配置する位置は SetPosition(int x, int y) を使って、X 、Y 座標を設定します。

```csharp
bannerAd.SetPosition(0, 50);
```
指定されたX、Y座標に BannerAd が配置されます。原点はスクリーンの左上になります。 


## 広告を読み込む
BannerAd の生成したら、次に広告を読み込みます。ここで BannerAd クラスの LoadAd()  メソッドを実行します。

以下は広告を読み込むサンプルコードです。
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private BannerAd bannerAd;
    ...
    public void Start()
    {
        ...
        this.RequestBanner();
    }

    private void RequestBanner()
    {
        ...
        // 広告の読み込み
        bannerAd.LoadAd();
    }
}
```
これで、AdLimeのバナー広告を表示できるようになりました。

## 広告イベント
広告の動作を細かくカスタマイズするために、広告のライフサイクルにによって発生するさまざまなイベント(読み込み、開く、閉じる)で広告を制御をします。 EventHandler にデリゲートを登録して、必要なイベントを監視します。
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private BannerAd bannerAd;
    ...
    public void Start()
    {
        ...
        this.RequestBanner();
    }

    private void RequestBanner()
    {
        ...

        // 広告のロード完了
        bannerAd.OnAdLoaded += HandleOnAdLoaded;
        // 広告の読み込み失敗
        bannerAd.OnAdFailedToLoad += HandleOnAdFailedToLoad;
        // 広告を表示
        bannerAd.OnAdShown += HandleOnAdShown;
        // 広告をクリック
        bannerAd.OnAdClicked += HandleOnAdClicked;
        // 広告を閉じる
        bannerAd.OnAdClosed += HandleOnAdClosed;

        // 広告の読み込み
        bannerAd.LoadAd();
    }

    public void HandleOnAdLoaded(object sender, EventArgs args)
    {
        MonoBehaviour.print("HandleOnAdLoaded event received");
    }

    public void HandleOnAdFailedToLoad(object sender, AdFailedToLoadEventArgs args)
    {
        MonoBehaviour.print("HandleOnAdFailedToLoad event received with error: "
                            + args.AdError);
    }

    public void HandleOnAdShown(object sender, EventArgs args)
    {
        MonoBehaviour.print("HandleOnAdShown event received");
    }

    public void HandleOnAdClicked(object sender, EventArgs args)
    {
        MonoBehaviour.print("HandleOnAdClicked event received");
    }

    public void HandleOnAdClosed(object sender, EventArgs args)
    {
        MonoBehaviour.print("HandleOnAdClosed event received");
    }
}
```

|広告イベント           |説明                         |
|:-                |:-                           |
|OnAdLoaded        |広告の読み込みが完了したときに実行されます。|
|OnAdFailedToLoad  |広告の読み込みが失敗したときに実行されます。 AdError クラスで、発生した問題の情報を取得できます。|
|OnAdShown         |広告が表示された時に実行されます。|
|OnAdClicked       |ユーザーが広告をクリックしたときに実行されます。このイベントで、クリック数などの分析を行うには最適なタイミングです。|
|OnAdClosed        |ユーザーが広告のリンク先 URL にアクセスした後、アプリに戻ったときに実行されます。|

### エラー情報
広告の読み込に失敗した場合は、 OnAdFailedToLoad イベントが呼び出されます。 その際に AdFailedToLoadEventArgs.AdError から エラー情報が取得できます。

```csharp
public void HandleOnAdFailedToLoad(object sender, AdFailedToLoadEventArgs args)
{
    MonoBehaviour.print("Banner failed to load: " + args.AdError);
    // Handle the ad failed to load event.  
};
```

AdError.GetCode()、AdError.GetMessage() から、エラーコード、エラー情報が取得できます。

 AdLime.Api.AdError エラーコード一覧
| 定義                       |説明     |
|:---------------------------|:--------|
|ERROR_CODE_INTERNAL_ERROR   | 内部エラー |
|ERROR_CODE_INVALID_REQUEST  | リクエストが無効 |
|ERROR_CODE_NETWORK_ERROR    | ネットワークエラー |
|ERROR_CODE_NO_FILL          | 配信できる広告がない   |
|ERROR_CODE_TIMEOUT          | リクエスト　タイムアウト |

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

|サイズ（dp）|説明         |使用範囲      |
|:-                      |:-            |:-          |
|320x50                  |バナー広告       |スマホンとタブレット |
|320x100                 |大幅バナー広告       |スマホンとタブレット |
|300x250                 |IAB 中矩形     |スマホンとタブレット |
|468x60                  |IAB フルサイズバナー |タブレット      |
|728x90                  |IAB ページ上端  |タブレット      |
|smart                   |スマートバナー       |スマホンとタブレット |

### スマートバナー
スマートバナーは、画面のサイズや向きにかかわらず、横幅いっぱいに広告が表示されます。表示する際に余白が生じる場合は、画像が中央寄せになり、両側のスペースは塗りつぶされます。現在は一部の広告プラットフォームのみに対応しています。

**ヒント：バナーの広告枠と広告のサイズは基本同じサイズです。広告枠の方が大きい場合は、広告が小さく表示されます。**  

## バナー広告を消去する
BannerAd を消去する場合は、必ず Destroy() メソッドを呼び出してから参照を削除するようにしてください。

```
bannerAd.Destroy();
```

これにより、オブジェクトが消去され、占有されていたメモリが解放し、再利用できることがプラグインに通知されます。このメソッドを呼び出さないと、メモリリークが発生します。