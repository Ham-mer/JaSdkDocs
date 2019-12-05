# 動画リワード広告を導入する

動画リワード広告とは、ユーザーが動画を最後まで視聴することと引き換えに、アプリ内で報酬を獲得できる動画広告です。このガイドは、動画リワード広告を AdLime から Android アプリに導入する方法について説明します。

## 前提条件
- AdLime SDK が導入済みであること

## 動画リワード広告オブジェクトを作成する

動画リワード広告は、RewardedVideoAd オブジェクトによってリクエストし、表示されます。まず RewardedVideoAd をインスタンス化し、その広告ユニットIDを設定してください。

```java
// 広告ユニットID の定義
String rewardId = "5400f178-bffb-47bf-bb4d-54faad99adfd"
// RewardedVideoAd を生成
RewardedVideoAd mRewardedVideoAd = new RewardedVideoAd(context);
mRewardedVideoAd.setAdUnitId(rewardId);
```
## 動画の読み込み

動画を読み込むには、RewardedVideoAd オブジェクトの loadAd() メソッド を実行します。

```java
// 動画の読み込み
mRewardedVideoAd.loadAd();
```

## 動画を表示する

動画リワード広告を表示する前に、広告のコンテンツを視聴して報酬を受け取るかどうか、明確な選択肢をユーザーに提示する必要があります。動画リワード広告は、必ずユーザーの許可を受けてから表示しなければなりません。

動画を表示するには、RewardedVideoAd オブジェクトの isReady() メソッド で広告の読み込みが完了したかどうかを確認して、show() メソッドを呼び出します。

```java
if (mRewardedVideoAd.isReady()) {
    // 広告を表示
    mRewardedVideoAd.show();
}
```

## 広告イベント

広告の動作をより細かくカスタマイズするには、広告のライフサイクルで発生する様々なイベント（読み込み、開始、終了など）を追加することができ、 RewardedVideoAdListener クラスを使い、これらのイベントを受け取ることができます。

RewardedVideoAd オブジェクトで RewardedVideoAdListener を利用するには、 setAdListener() メソッドを呼び出してください。

```java
mRewardedVideoAd.setAdListener(new SimpleRewardedVideoAdListener() {
    @Override
    public void onAdLoaded() {
        // 動画のロード完了
        LogUtil.d(TAG, "onAdLoaded");        
    }

    @Override
    public void onAdShown() {
        // 動画を表示
        LogUtil.d(TAG, "onAdShown");
    }

    @Override
    public void onAdClicked() {
        // 動画をクリック
        LogUtil.d(TAG, "onAdClicked");
    }

    @Override
    public void onAdClosed() {
        // 動画を閉じる
        LogUtil.d(TAG, "onAdClosed");
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 動画の読み込み失敗
        LogUtil.d(TAG, "onAdFailedToLoad, " + adError);
    }

    @Override
    public void onVideoStarted() {
        // 動画の再生開始
        LogUtil.d(TAG, "onVideoStarted");
    }

    @Override
    public void onVideoCompleted() {
        // 動画の再生完了
        LogUtil.d(TAG, "onVideoCompleted");
    }

    @Override
    public void onRewarded(RewardedVideoAd.RewardItem rewardItem) {
        // リワードを獲得
        LogUtil.d(TAG, "onRewarded, " + rewardItem);
    }

    @Override
    public void onRewardFailed() {
        // リワード獲得失敗
        LogUtil.d(TAG, "onRewardFailed");
    }
});
```

### エラーの情報
広告の読み込に失敗した場合は、RewardedVideoAdListener の onAdFailedToLoad(AdError adError) が呼び出されます。その際に adError.getCode() 、 adError.toString() から、エラーコード、エラー情報が取得できます。

 AdError エラーコード一覧
|定義                        |説明     |
|:--------------------------|:--------|
|ERROR_CODE_INTERNAL_ERROR  | 内部エラー |
|ERROR_CODE_INVALID_REQUEST | 無効リクエスト |
|ERROR_CODE_NETWORK_ERROR   | ネットワークエラー |
|ERROR_CODE_NO_FILL         | フィルなし   |
|ERROR_CODE_TIMEOUT         | リクエスト　タイムアウト |

エラーは AdUnit、ネットワーク、ラインアイテムの各情報が含まれています。

```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

### リワード情報

下記は RewardedVideoAd.RewardItem クラスのリワード情報メソッド一覧です。

|メソッド名 |  型  | 説明 | 
|------ |----------|-----|
|getType| String  |リワードタイプ|
|getAmount | int | リワード数   |

## プリロードとキャッシュ
プリロードで事前に広告を用意して展示するまでの時間を短くする<br>
広告をプリロードするかどうかにもかかわらず、広告をキャッシュすることはお勧め。理由としては一つのAdUnitに各LineItemはロードされるはずで、一つの広告インスタンスを繰り返して使うと、展示率を高めて必要ではないリクエストも減らせる。
自ら広告キャッシュを実現できるし、[AdLimeLoader](./adloader.md)でも実現できる。