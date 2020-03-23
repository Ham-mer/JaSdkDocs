# 動画リワード広告

動画リワード広告とは、ユーザーが動画を最後まで視聴することと引き換えに、アプリ内で報酬を獲得できる動画広告です。このガイドは、動画リワード広告を AdLime から Android アプリに導入する方法について説明します。

## 前提条件
- AdLime SDK が導入済みであること

## 動画リワード広告オブジェクトを作成する

動画リワード広告は、`RewardedVideoAd` オブジェクトによってリクエストし、表示されます。まず `RewardedVideoAd` をインスタンス化し、その広告ユニット ID を設定してください。

:::: tabs

::: tab Java

```java
// 広告ユニット ID の定義
String rewardId = "5400f178-bffb-47bf-bb4d-54faad99adfd"
// RewardedVideoAd を生成
RewardedVideoAd mRewardedVideoAd = new RewardedVideoAd(context);
mRewardedVideoAd.setAdUnitId(rewardId);
```

:::

::: tab Kotlin

```kotlin
// 広告ユニット ID の定義
val rewardId = "5400f178-bffb-47bf-bb4d-54faad99adfd"
// RewardedVideoAd を生成
val mRewardedVideoAd = RewardedVideoAd(this)
mMixFullScreenAd.setAdUnitId(rewardId)
```

:::

::::

## 動画の読み込み

動画を読み込むには、`RewardedVideoAd` オブジェクトの `loadAd()` メソッド を実行します。

:::: tabs

::: tab Java

```java
// 動画の読み込み
mRewardedVideoAd.loadAd();
```

:::

::: tab Kotlin

```kotlin
// 動画の読み込み
mRewardedVideoAd.loadAd()
```

:::

::::

## 動画を表示する

動画リワード広告を表示する前に、広告のコンテンツを視聴して報酬を受け取るかどうか、明確な選択肢をユーザーに提示する必要があります。動画リワード広告は、必ずユーザーの許可を受けてから表示しなければなりません。

動画を表示するには、RewardedVideoAd オブジェクトの `isReady()` メソッド で広告の読み込みが完了したかどうかを確認して、`show()` メソッドを呼び出します。展示する前に、getRewardItem() でリワードの内容を取ってユーザーさんにお知らせします。参考コードは下記通りです。

:::: tabs

::: tab Java

```java
if (mRewardedVideoAd.isReady()) {
    // 広告を展示する前に、Dialogでリワードの内容をユーザーさんにお知らせることができます
    // RewardedVideoAd.RewardItem rewardItem = mRewardedVideoAd.getRewardItem();
    // LogUtil.d(TAG, "RewardItem: " + rewardItem);
    // 広告を表示
    mRewardedVideoAd.show(activity);
}
```
:::

::: tab Kotlin

```kotlin
if (mRewardedVideoAd.isReady()) {
    // 広告を展示する前に、Dialogでリワードの内容をユーザーさんにお知らせることができます
    // RewardedVideoAd.RewardItem rewardItem = mRewardedVideoAd.getRewardItem()
    // LogUtil.d(TAG, "RewardItem: " + rewardItem)
    // 広告を表示
    mRewardedVideoAd.show(activity)
}
```

:::

::::

## 広告イベント

広告の動作をより細かくカスタマイズするには、広告のライフサイクルで発生する様々なイベント（読み込み、開始、終了など）を追加することができ、 RewardedVideoAdListener クラスを使い、これらのイベントを受け取ることができます。

RewardedVideoAd のイベントを取得するには、 `RewardedVideoAdListener` クラスの各デリゲートを定義し、`setAdListener()` で登録します。

:::: tabs

::: tab Java

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

:::

::: tab Kotlin

```kotlin
mRewardedVideoAd.setAdListener(object : SimpleAdListener() {
            override fun onAdLoaded() {
                // 動画のロード完了
                print("onAdLoaded")
            }

            override fun onAdShown() {
                //  広告を表示
                print("onAdShown")
            }

            override fun onAdClicked() {
                //  広告をクリック
                print("onAdClicked")
            }

            override fun onAdClosed() {
                //  広告を閉じる
            }

            override fun onAdFailedToLoad(adError: AdError) {
                //  広告の読み込み失敗、エラー詳細は adError から取得
                print("onAdFailedToLoad: " + adError.toString())
            }

            override fun onVideoStarted() {
                // 動画の再生開始
                print("onVideoStarted")
            }

            override fun onVideoCompleted() {
                // 動画の再生完了
                print("onVideoCompleted")
            }

            override fun onRewarded(RewardedVideoAd.RewardItem rewardItem) {
                // リワードを獲得
                print("onRewarded, " + rewardItem)
            }

            override fun onRewardFailed() {
                // リワード獲得失敗
                print("onRewardFailed")
            }
        }
```

:::

::::

### 広告のロードエラーについて
広告の読み込に失敗した場合は、RewardedVideoAdListener の `onAdFailedToLoad(AdError adError)` が呼び出されます。その際に `adError.getCode()` 、 `adError.toString()` から、エラーコード、エラー情報が取得できます。

#### エラーコードとエラーメッセージについて

[エラー情報](./error.md#エラーコードとエラーメッセージ)を確認してください。

### リワード情報

下記は RewardedVideoAd.RewardItem クラスのリワード情報メソッド一覧です。

|メソッド名 |  型  | 説明 | 
|------ |----------|-----|
|getType| String  |リワードタイプ|
|getAmount | int | リワード数   |

## プリロードとキャッシュ
事前に広告をロードをして、表示までの待ち時間を極力抑えましょう。<br>
また広告をプリロードする・しないに関わらず、広告をキャッシュすることをおすすめします。広告枠では、各広告ネットワークの広告がロードされますが、広告枠の1つのインスタンスを繰り返し使用することで、高いインプレッションを得られ、不要なリクエストも抑えることができます。これらは、[AdLimeLoader](./adloader.md)で実現が可能です。

## 次のステップ
- 他の広告フォーマットを追加で利用したい場合は[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、Android アプリに実装しましょう。
- 広告が正しく表示できるか確認したい場合は、[広告表示テスト](./test.md)に従い アプリ ID と各広告ネットワークに対応する広告枠 ID を設定して、広告を表示してみましょう。