# 動画リワード広告
動画リワード広告とは、ユーザーが動画を最後まで視聴することと引き換えに、アプリ内で報酬を獲得できる動画広告です。
このガイドでは、動画リワード広告を AdLime から Unity アプリに導入する方法について説明します。

## 前提条件
- [スタートガイド](./begin.md) の手順を完了し、 AdLime Unity プラグインがインポート済みであること
- [初期化](./init.md)の手順が完了済みであること

## 動画リワード広告の作成
動画リワード広告を表示するための最初のステップは、 GameObject のスクリプトで RewardedVideoAd オブジェクトを作成します。
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private RewardedVideoAd rewardedVideoAd;
    ...
    public void Start()
    {
        ...
        this.RequestrewardedVideo();
    }

    private void RequestrewardedVideo()
    {
        #if UNITY_ANDROID
            string adUnitId = "Android AdUnit ID";
        #elif UNITY_IPHONE
            string adUnitId = "iOS AdUnit ID";
        #else
            string adUnitId = "unexpected_platform";
        #endif

        // RewardedVideoAdの作成
        rewardedVideoAd = new RewardedVideoAd(adUnitId);
    }
}
```

※ 注意 : プラットフォームに応じた、広告ユニット ID を設定してください。Android の端末からリクエストを出す場合には、 Android 広告ユニット ID を使用します。iOS の場合は iOS 広告ユニット IDを使用します。

## 広告の読み込み

RewardedVideoAd を生成したら、次に広告を読み込みます。 RewardedVideoAd クラスの loadAd() メソッドを実行します。

以下は広告を読み込むサンプルコードです。
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private RewardedVideoAd rewardedVideoAd;
    ...
    public void Start()
    {
        ...
        this.RequestrewardedVideo();
    }

    private void RequestrewardedVideo()
    {
        ...
        // 広告の読み込み
        rewardedVideoAd.LoadAd();
    }
}
```

## 広告を表示する

動画リワード広告を表示する前に、広告のコンテンツを視聴して報酬を受け取るかどうか、明確な選択肢をユーザーに提示する必要があります。動画リワード広告は、必ずユーザーの許可を受けてから表示しなければなりません。

動画を表示するには、RewardedVideoAd クラスの isReady() メソッドで、広告の読み込みが完了したかどうかを確認して、 show() をメソッドを実行します。

```csharp
private void UserChoseToWatchAd()
{
    if (this.rewardedVideoAd.IsReady()) {
        this.rewardedVideoAd.Show();
    }
}
```

## 広告イベント
広告の動作をより細かくカスタマイズするには、広告のライフサイクルで生じるさまざまなイベント（読み込み、開始、終了など）を追加することができます。 以下のサンプルのように、デリゲートをイベントハンドラに登録して、イベントを受信します。

```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private RewardedVideoAd rewardedVideoAd;
    ...
    public void Start()
    {
        ...
        this.RequestrewardedVideo();
    }

    private void RequestrewardedVideo()
    {
        ...

        // 広告のロード完了
        rewardedVideoAd.OnAdLoaded += HandleOnAdLoaded;
        // 広告の読み込み失敗
        rewardedVideoAd.OnAdFailedToLoad += HandleOnAdFailedToLoad;
        // 広告の表示
        rewardedVideoAd.OnAdShown += HandleOnAdShown;
        // 広告をクリック
        rewardedVideoAd.OnAdClicked += HandleOnAdClicked;
        // 広告を閉じる
        rewardedVideoAd.OnAdClosed += HandleOnAdClosed;
        // 動画の再生開始
        rewardedVideoAd.OnVideoStarted += HandleOnVideoStarted;
        // 動画の再生完了
        rewardedVideoAd.OnVideoCompleted += HandleOnVideoCompleted;
        // リワードを獲得
        rewardedVideoAd.OnRewarded += HandleOnRewarded;
        // リワード獲得失敗
        rewardedVideoAd.OnRewardFailed += HandleOnRewardFailed;

        // 広告の読み込み
        rewardedVideoAd.LoadAd();
    }

    public void HandleOnAdLoaded(object sender, EventArgs args)
    {
        MonoBehaviour.print("HandleOnAdLoaded event received");
    }

    public void HandleOnAdFailedToLoad(object sender, AdFailedToLoadEventArgs args)
    {
        MonoBehaviour.print("HandleOnAdFailedToLoad event received with error: " + args.AdError);
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

    public void HandleOnVideoStarted(object sender, EventArgs args)
    {
        MonoBehaviour.print("HandleOnVideoStarted event received");
    }

    public void HandleOnVideoCompleted(object sender, EventArgs args)
    {
        MonoBehaviour.print("HandleOnVideoCompleted event received");
    }

    public void HandleOnRewarded(object sender, RewardedEventArgs args)
    {
        int amout = args.RewardItem.GetAmount();
        string type = args.RewardItem.GetRewardType();
        MonoBehaviour.print("HandleOnRewarded event received for: " + type + ", " + amount.ToString());
    }

    public void HandleOnRewardFailed(object sender, EventArgs args)
    {
        MonoBehaviour.print("HandleOnRewardFailed event received");
    }
}
```

|広告イベント       |説明                         |
|:-                |:-                           |
|OnAdLoaded        |広告の読み込みが完了したときに実行されます。|
|OnAdFailedToLoad  |広告の読み込みが失敗したときに実行されます。 AdError クラスで、発生したエラーの情報を取得できます。|
|OnAdShown         |広告が表示されたときに実行されます。|
|OnAdClicked       |ユーザーが広告をクリックしたときに実行されます。このイベントで、クリック数などの分析を行うには最適なタイミングです。|
|OnAdClosed        |ユーザーが広告のリンク先 URL にアクセスした後、アプリに戻ったときに実行されます。アプリの中断した処理を再開するタイミングとして適しています。|
|OnVideoStarted|動画の再生が開始したときに実行されます。|
|OnVideoCompleted|動画再生が完了すると実行されます。|
|OnRewarded|リワードを獲得すると実行されます。|
|OnRewardFailed|リワード獲得が失敗すると実行されます。|

### エラー
広告の読み込に失敗した場合は、 OnAdFailedToLoad イベントが呼び出されます。その際に AdFailedToLoadEventArgs.AdError からエラー情報が取得できます。

```csharp
public void HandleOnAdFailedToLoad(object sender, AdFailedToLoadEventArgs args)
{
    MonoBehaviour.print("RewardedVideo failed to load: " + args.AdError);
    // Handle the ad failed to load event.
};
```

AdError.GetCode()、AdError.GetMessage()を通じて、エラーコードとエラー情報は得られます。

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

### OnAdClosed を使用して、次の動画リワード広告をプリロードする

動画リワード広告を表示した後に、別の動画リワード広告を読み込むには、 OnAdClosed イベント を使用します。前の動画リワード広告を閉じると同時に、次の動画リワード広告の読み込みを開始することができます。

```csharp
public void HandleOnAdClosed(object sender, EventArgs args)
{
    this.rewardedVideoAd.LoadAd();
}
```

## 動画リワード広告の削除

RewardedVideoAd を削除する場合は、必ず Destroy() メソッドを呼び出してから参照を削除するようにしてください。

```
rewardedVideoAd.Destroy();
```

これにより、オブジェクトが消去され、占有されていたメモリが解放し、再利用できることがプラグインに通知されます。このメソッドを呼び出さないと、メモリリークが発生します。