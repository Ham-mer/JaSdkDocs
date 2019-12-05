# インタースティシャル広告
インタースティシャル広告は、ホストアプリのインターフェースを覆うようにフルスクリーンで表示される広告です。通常は、ゲームのレベルが変わる際のポーズ画面など、アプリの画面が切り替わる自然なタイミングで表示されます。アプリにインタースティシャル広告が表示されると、ユーザーは広告をタップしてリンク先 URL に移動するか、広告を閉じてアプリに戻るかを選択することになります。

このガイドでは、インタースティシャル広告を Unity アプリに実装する方法について説明します。

## 前提条件
- [スタートガイド](./begin.md) の手順を完了し、 AdLime Unity プラグインがインポート済みであること
- [初期化](./init.md) の手順が完了済みであること

## インタースティシャル広告を作成する
インタースティシャルを表示するための最初のステップは、GameObject に追加されたスクリプトに InterstitialAd オブジェクトを作成することです。
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private InterstitialAd interstitialAd;
    ...
    public void Start()
    {
        ...
        this.RequestInterstitial();
    }

    private void RequestInterstitial()
    {
        #if UNITY_ANDROID
            string adUnitId = "Android AdUnit ID";
        #elif UNITY_IPHONE
            string adUnitId = "iOS AdUnit ID";
        #else
            string adUnitId = "unexpected_platform";
        #endif

        // InterstitialAd の生成
        interstitialAd = new InterstitialAd(adUnitId);
    }
}
```

※ 注意 : プラットフォームに応じた、広告ユニット ID を設定してください。Android の端末からリクエストを出す場合には、 Android 広告ユニット ID を使用します。iOS の場合は iOS 広告ユニット IDを使用します。

## 広告の読み込み
InterstitialAd を生成したら、次に広告を読み込みます。 InterstitialAd クラスの loadAd() メソッドを実行します。

以下は広告を読み込むサンプルコードです。
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private InterstitialAd interstitialAd;
    ...
    public void Start()
    {
        ...
        this.RequestInterstitial();
    }

    private void RequestInterstitial()
    {
        ...
        // 広告を読み込み
        interstitialAd.LoadAd();
    }
}
```

## 広告を表示する
インタースティシャル広告は、アプリの流れが一時的に中断する自然なタイミングで表示される必要があります。ゲームのレベルが切り替わる合間やタスクが完了した直後などが良い例です。インタースティシャルを表示するには、 isLoaded()  メソッドを使用して読み込みが完了したことを確認してから、 show()  を呼び出します。

以下のサンプルコードでは、ゲームが終了した時に、インタースティシャル広告が表示されます。

```csharp
private void GameOver()
{
    if (this.interstitialAd.IsReady()) {
        this.interstitialAd.Show();
    }
}
```

## 広告イベント
広告の動作をより細かくカスタマイズするには、広告のライフサイクルで生じるさまざまなイベント（読み込み、開始、終了など）を考慮します。以下に示すように、適切な EventHandler にデリゲートを登録して、これらのイベントを受け取ります。
```csharp
...
using AdLime.Api;
...
public class AdLimeDemoScript : MonoBehaviour
{
    private InterstitialAd interstitialAd;
    ...
    public void Start()
    {
        ...
        this.RequestInterstitial();
    }

    private void RequestInterstitial()
    {
        ...

        // 広告のロード完了
        interstitialAd.OnAdLoaded += HandleOnAdLoaded;
        // 広告の読み込み失敗
        interstitialAd.OnAdFailedToLoad += HandleOnAdFailedToLoad;
        // 広告の表示
        interstitialAd.OnAdShown += HandleOnAdShown;
        // 広告をクリック
        interstitialAd.OnAdClicked += HandleOnAdClicked;
        // 広告を閉じる
        interstitialAd.OnAdClosed += HandleOnAdClosed;

        // 広告の読み込み
        interstitialAd.LoadAd();
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

|広告イベント           |説明                          |
|:-                |:-                           |
|OnAdLoaded        |広告の読み込みが完了したときに実行されます。|
|OnAdFailedToLoad  |広告の読み込みが失敗したときに実行されます。 AdError クラスで、発生したエラーの情報を取得できます。|
|OnAdShown         |広告が表示されたときに実行されます。|
|OnAdClicked       |ユーザーが広告をクリックしたときに実行されます。このイベントで、クリック数などの分析を行うには最適なタイミングです。|
|OnAdClosed        |ユーザーが広告のリンク先 URL にアクセスした後、アプリに戻ったときに実行されます。|

### エラー情報
広告の読み込に失敗した場合は、 OnAdFailedToLoad イベントが呼び出されます。 その際に AdFailedToLoadEventArgs.AdError からエラー情報が取得できます。

```csharp
public void HandleOnAdFailedToLoad(object sender, AdFailedToLoadEventArgs args)
{
    MonoBehaviour.print("Interstitial failed to load: " + args.AdError);
    // Handle the ad failed to load event.
};
```

AdError.GetCode()、AdError.GetMessage()から、エラーコード、エラー情報が取得できます。

 AdLime.Api.AdError エラーコード一覧
| 定義                       |説明     |
|:---------------------------|:--------|
|ERROR_CODE_INTERNAL_ERROR   | 内部エラー |
|ERROR_CODE_INVALID_REQUEST  | リクエストが無効 |
|ERROR_CODE_NETWORK_ERROR    | ネットワークエラー |
|ERROR_CODE_NO_FILL          | 配信できる広告がない   |
|ERROR_CODE_TIMEOUT          | リクエスト　タイムアウト |

エラーは、 AdUnit、ネットワーク、ラインアイテムの各情報が含まれています。

```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## インタースティシャル広告のクリーンアップ
InterstitialAd を消去する場合は、必ず Destroy() メソッドを呼び出してから参照を削除するようにしてください。

```
interstitialAd.Destroy();
```

これにより、オブジェクトが消去され、占有されていたメモリが解放し、再利用できることがプラグインに通知されます。このメソッドを呼び出さないとメモリリークが発生します。

## 推奨事項
### インタースティシャル広告がアプリに適しているかどうかをよく見極めましょう

インタースティシャル広告は、自然な移行ポイント（画面の切り替わりなど）があるアプリに適しています。画像の共有やゲームレベルのクリアなど、アプリ内で特定のタスクが完了したタイミングがこうした移行ポイントになります。ユーザーも流れの中断を想定しているため、インタースティシャル広告を表示しても操作性を損ないません。アプリ内のどの時点でインタースティシャル広告を表示し、ユーザーがそれにどう反応すると考えられるかを考慮しましょう。

### インタースティシャル広告を表示する際には、必ずアクションを一時停止しましょう。

インタースティシャル広告には、テキスト、イメージ、動画などのさまざまな種類があります。インタースティシャル広告を表示する際は、広告で使用されるリソースを考慮し、アプリの一部のリソースを一時停止させることが重要です。たとえばインタースティシャル広告を呼び出して表示する際は、アプリの音声出力を一時停止します。音声出力はイベント  OnAdClosed で再開できます。このハンドラはユーザーが広告に対する操作を完了すると呼び出されます。この広告の表示中は、複雑な計算処理（ゲームループなど）も一時停止することをおすすめします。こうすると、画像の読み込みが遅くなったり停止したり、動画が頻繁に途切れたりする恐れがなくなります。

### 十分な読み込み時間を確保しましょう。

インタースティシャル広告を適切なタイミングで表示することも大事ですが、それと同様に読み込みの待ち時間を短くすることも重要です。 showFromViewController の呼び出しの前に loadAd で広告を読み込んでください。そうすると表示前の段階でインタースティシャル広告の読み込みを完了させることができます。

### ユーザーに広告を表示しすぎることを避けよう

インタースティシャルの表示頻度を増やすことで収益の向上が見込めますが、それが原因でが損なわれ、クリック率の低下につながる可能性もあります。ユーザーがアプリでの体験を楽しめるように、適度な広告表示頻度に調節しましょう。

### OnAdLoaded イベントで広告を表示しないでください。

このイベントを使用すると、ユーザーエクスペリエンスの低下につながる場合があります。代わりに、表示が必要になる前にあらかじめ広告を読み込み、AdLimeInterstitialAd の isReady メソッドをチェックし、表示の準備ができているかどうかを確認してください。
