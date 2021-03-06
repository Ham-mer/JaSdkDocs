# インタースティシャル広告

インタースティシャル広告とは、アプリ上を覆うようにポップアップで表示されるフルスクリーン広告です。一般的にアプリの画面が切り替わるタイミング（アクティビティが切り替わるタイミングやゲームのステージが変わる合間）で用いられます。

このガイドは、インタースティシャル広告を Android アプリに実装する方法について説明します。

**<u>複合型広告枠を用いることでより効果的に広告収益を高めることができます。詳細は [MixFullScreenAd](./mixfullscreenad.md) をご確認ください。</u>**


## 前提条件

- AdLime SDK が導入済みであること

## インタースティシャル広告オブジェクトを作成する

インタースティシャル広告は、InterstitialAd オブジェクトによってリクエストし、表示されます。まず InterstitialAd をインスタンス化し、その広告ユニットIDを設定してください。

:::: tabs

::: tab Java

```java
import com.access_company.adlime.core.api.ad.InterstitialAd;

public class MainActivity extends AppCompatActivity {
    InterstitialAd mInterstitialAd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 広告ユニット ID の定義
        String interstitialId = "46dca932-2a10-4702-89fc-e5e87e00b09c";
        // InterstitialAd を作成
        mInterstitialAd = new InterstitialAd(context);
        mInterstitialAd.setAdUnitId(interstitialId);
    }
}
```

:::

::: tab Kotlin

```kotlin
import com.access_company.adlime.core.api.ad.InterstitialAd

class MainActivity : AppCompatActivity() {
    lateinit var mInterstitialAd: InterstitialAd

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // 広告ユニット ID の定義
        val interstitialId = "46dca932-2a10-4702-89fc-e5e87e00b09c"
        // InterstitialAd を作成
        mInterstitialAd = InterstitialAd(this)
        mInterstitialAd.adUnitId = interstitialId
    }
}
```

:::

::::

## 広告の読み込み

インタースティシャル広告を読み込むには、 InterstitialAd オブジェクトの loadAd() メソッドを実行します。

:::: tabs

::: tab Java

```java
// 広告の読み込み
mInterstitialAd.loadAd();
```

:::

::: tab Kotlin

```kotlin
// 広告の読み込み
mInterstitialAd.loadAd()
```

:::

::::

## 広告を表示する

インタースティシャル広告は、アプリの流れが一時的に中断する自然なタイミング（ゲームのステージが変わる合間や一つのミッションが完了になった直後など）で表示することが相応しい形です。インタースティシャル広告を表示するには、 isReady() メソッドで読み込みが完了したかどうかを確認し、 show() を呼び出してください。

:::: tabs

::: tab Java

```java
if (mInterstitialAd.isReady()) {
    // 広告の表示
    mInterstitialAd.show(activity);
}
```

:::

::: tab Kotlin

```kotlin
if (mInterstitialAd.isReady) {
    // 広告の表示
    mInterstitialAd.show(activity)
}
```

:::

::::

## 広告イベント
広告の動作をより細かくカスタマイズするには、広告のライフサイクルで発生するイベント（読み込み、開始、終了など）を追加することができ、 AdListener クラスを使い、これらのイベントを受け取ることができます。

### InterstitialAd イベントを登録する
InterstitialAd のイベントを取得するには、`SimpleAdListener` インスタンスを作成し、`setAdListener()` で登録します。

:::: tabs

::: tab Java

```java
mInterstitialAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        // 広告のロード完了
        Log.d(TAG, "on InterstitialAd Loaded");
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 広告の読み込み失敗、エラー詳細は adError から取得
        Log.d(TAG, "on InterstitialAd FailedToLoad err:" + adError.toString());
    }

    @Override
    public void onAdShown() {
        // 広告を表示
        Log.d(TAG, "on InterstitialAd Shown");
    }

    @Override
    public void onAdClicked() {
        // 広告をクリック
        Log.d(TAG, "on InterstitialAd Clicked");
    }

    @Override
    public void onAdClosed() {
        // 広告を閉じる
        Log.d(TAG, "on InterstitialAd Closed");
    }
});
```

:::

::: tab Kotlin

```kotlin
mInterstitialAd.adListener = object: SimpleAdListener() {
    override fun onAdLoaded() {
        // 広告のロード完了
        println("on InterstitialAd Loaded")
    }

    override fun onAdFailedToLoad(adError: AdError?) {
        //  広告の読み込み失敗、エラー詳細は adError から取得
        println("onAdFailedToLoad: " + adError.toString())
    }

    override fun onAdShown() {
        //  広告を表示
        println("on InterstitialAd Shown")
    }

    override fun onAdClicked() {
        //  広告をクリック
        println("on InterstitialAd Clicked")
    }

    override fun onAdClosed() {
        //  広告を閉じる
        println("on InterstitialAd Closed")
    }
}
```

:::

::::

### 広告のロードエラーについて
広告の読み込に失敗した場合は、AdListener の `onAdFailedToLoad(AdError adError)` が呼び出されます。その際に `adError.getCode()`、`adError.toString()` から、エラーコード、エラー情報が取得できます。

#### エラーコードとエラーメッセージについて

[エラー情報](./error.md#エラーコードとエラーメッセージ)を確認してください。

## プリロードとキャッシュ
事前に広告をロードをして、表示までの待ち時間を極力抑えましょう。<br>
また広告をプリロードする・しないに関わらず、広告をキャッシュすることをおすすめします。広告枠では、各広告ネットワークの広告がロードされますが、広告枠の1つのインスタンスを繰り返し使用することで、高いインプレッションを得られ、不要なリクエストも抑えることができます。これらは、[AdLimeLoader](./adloader.md)で実現が可能です。

## 推奨事項

### インタースティシャル広告がアプリに適しているかどうか確認してください。

インタースティシャル広告は、画面の切り替わりがあるアプリに適しています。
このような移行ポイントは、画像の共有やゲームステージのクリアなど、アプリで特定のタスクが完了した際に発生します。ユーザーはこのタイミングで中断が入ることを想定しているので、インタースティシャル広告を表示してもユーザーエクスペリエンスに悪影響を及ぼすことはありません。アプリケーション・プロセスの、どの時点でインタースティシャル広告を表示するか、またユーザーがそれにどう反応するかを共に考慮に入れてください。


### インタースティシャル広告を表示する際には、必ず操作を一時停止してください。

インタースティシャル広告には、テキスト・イメージ・動画など様々な種類があります。インタースティシャル広告を表示する際に、アプリのリソースを一時停止させることが重要です。たとえば、インタースティシャル広告を呼び出した後、アプリの音声出力を一時停止させてください。音声出力は、イベントハンドラ onAdClosed() によって再開できます。このハンドラは、ユーザーが広告に対する操作を完了した後に呼び出されます。また広告を表示している間は、複雑な計算処理（ゲームループなど）も一時停止させてください。こうすることで、画像の読み込みが遅くなり、あるいは反応しなくなったり、動画が頻繁に途切れたりするリスクが低くなります。


### 十分な読み込み時間を確保してください。

インタースティシャル広告を適切なタイミングで表示することも大事ですが、それと同様に読み込みの待ち時間を短くすることも重要です。 show() を呼び出す前に、 loadAd() を実行してください。こうすることで表示前の段階で、インタースティシャル広告の読み込みを完了させることができます。

### 過度に広告を表示しないように注意してください。

インタースティシャル広告の表示頻度を増やすことで収益の向上が見込めますが、それが原因でユーザー体験が損なわれ、クリック率の低下につながる可能性もあります。ユーザーがアプリでの体験を楽しめるように、適度な広告表示頻度に調節しましょう。

## 次のステップ
- 他の広告フォーマットを追加で利用したい場合は[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、Android アプリに実装しましょう。
- 広告が正しく表示できるか確認したい場合は、[広告表示テスト](./test.md)に従い アプリ ID と各広告ネットワークに対応する広告枠 ID を設定して、広告を表示してみましょう。