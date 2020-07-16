# 動画リワード広告

動画リワード広告とは、アプリ内で使用可能な報酬をユーザーに付与する代わりに、動画広告を最後までフルスクリーン表示する広告です。ネイティブ広告やインタースティシャル広告など自動で再生する動画広告とは異なり、視聴を希望したユーザーにのみ動画広告を再生します。他の広告フォーマットに比べ広告効果が高いため、広告単価が高く、効果的に収益を得ることが可能です。


このガイドでは 動画リワード広告 を Android のアプリに実装する方法を説明します。

## 前提条件
- AdLime SDK が導入済みであること

## 動画リワード広告オブジェクトを作成する

動画リワード広告は、`RewardedVideoAd` オブジェクトによってリクエストし、表示されます。まず `RewardedVideoAd` をインスタンス化し、その広告ユニット ID を設定してください。

:::: tabs

::: tab Java

```java
import com.access_company.adlime.core.api.ad.RewardedVideoAd;

public class MainActivity extends AppCompatActivity {
    RewardedVideoAd mRewardedVideoAd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 広告ユニット ID の定義
        String rewardId = "5400f178-bffb-47bf-bb4d-54faad99adfd"
        // RewardedVideoAd を生成
        mRewardedVideoAd = new RewardedVideoAd(context);
        mRewardedVideoAd.setAdUnitId(rewardId);
    }
}
```

:::

::: tab Kotlin

```kotlin
import com.access_company.adlime.core.api.ad.RewardedVideoAd

class MainActivity : AppCompatActivity() {
    lateinit var mRewardedVideoAd: RewardedVideoAd

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // 広告ユニット ID の定義
        val rewardId = "5400f178-bffb-47bf-bb4d-54faad99adfd"
        // RewardedVideoAd を生成
        mRewardedVideoAd = RewardedVideoAd(this)
        mRewardedVideoAd.adUnitId = rewardId
    }
}
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

RewardedVideoAd のイベントを取得するには、 `RewardedVideoAdListener` インスタンスを作成し、`setAdListener()` で登録します。

:::: tabs

::: tab Java

```java
mRewardedVideoAd.setAdListener(new SimpleRewardedVideoAdListener() {
    @Override
    public void onAdLoaded() {
        // 動画のロード完了
        Log.d(TAG, "onAdLoaded");
    }

    @Override
    public void onAdShown() {
        // 動画を表示
        Log.d(TAG, "onAdShown");
    }

    @Override
    public void onAdClicked() {
        // 動画をクリック
        Log.d(TAG, "onAdClicked");
    }

    @Override
    public void onAdClosed() {
        // 動画を閉じる
        Log.d(TAG, "onAdClosed");
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 動画の読み込み失敗
        Log.d(TAG, "onAdFailedToLoad, " + adError);
    }

    @Override
    public void onVideoStarted() {
        // 動画の再生開始
        Log.d(TAG, "onVideoStarted");
    }

    @Override
    public void onVideoCompleted() {
        // 動画の再生完了
        Log.d(TAG, "onVideoCompleted");
    }

    @Override
    public void onRewarded(RewardedVideoAd.RewardItem rewardItem) {
        // リワードを獲得
        Log.d(TAG, "onRewarded, " + rewardItem);
    }

    @Override
    public void onRewardFailed() {
        // リワード獲得失敗
        Log.d(TAG, "onRewardFailed");
    }
});
```

:::

::: tab Kotlin

```kotlin
mRewardedVideoAd.adListener = object : SimpleRewardedVideoAdListener() {
    override fun onAdLoaded() {
        // 動画のロード完了
        println("onAdLoaded")
        mRewardedVideoAd.show(context)
    }

    override fun onAdShown() {
        //  広告を表示
        println("onAdShown")
    }

    override fun onAdClicked() {
        //  広告をクリック
        println("onAdClicked")
    }

    override fun onAdClosed() {
        //  広告を閉じる
    }

    override fun onAdFailedToLoad(adError: AdError) {
        //  広告の読み込み失敗、エラー詳細は adError から取得
        println("onAdFailedToLoad: " + adError.toString())
    }

    override fun onVideoStarted() {
        // 動画の再生開始
        println("onVideoStarted")
    }

    override fun onVideoCompleted() {
        // 動画の再生完了
        println("onVideoCompleted")
    }

    override fun onRewarded(rewardItem: RewardedVideoAd.RewardItem?) {
        println("onRewarded, " + rewardItem.toString())
    }

    override fun onRewardFailed() {
        // リワード獲得失敗
        println("onRewardFailed")
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