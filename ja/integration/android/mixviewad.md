#  MixViewAd
MixViewAd とはバナー広告やネイティブ広告などの別種の広告を単一の View で表示ができる機能です。各ネットワークの提供する広告は、個別のフォーマットで独立した広告が提供されていました。この機能を実装することにより、1つの広告枠で表示できる広告の種類と数を増やし、より高い効率で収益を増やすことができます。

MixViewAd は[バナー広告](./banner.md)と[ネイティブ広告](./native.md)をサポートしています。このガイドでは、MixViewAd を Android のアプリに実装する方法を紹介します。

## 前提条件
- AdLime SDK が導入済みであること

## MixViewAd の作成
広告ユニット ID を設定し、`MixViewAd` オブジェクトを作成します。

:::: tabs

::: tab Java

```java
import com.access_company.adlime.core.api.ad.MixViewAd;

public class MainActivity extends AppCompatActivity {
    MixViewAd mMixViewAd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        mMixViewAd = new MixViewAd(this);
        mMixViewAd.setAdUnitId("広告枠 ID");
    }
}
```

:::

::: tab Kotlin

```kotlin
import com.access_company.adlime.core.api.ad.MixViewAd

class MainActivity : AppCompatActivity() {
    private var mContainer: FrameLayout? = null
    lateinit var mMixViewAd: MixViewAd

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        mMixViewAd = MixViewAd(this)
        mMixViewAd.adUnitId = "広告枠 ID"
    }
}
```

:::

::::

::: tip
広告枠に Flurry / Unity Adsのバナー広告がある場合は、コンストラクタの引数として Activity を設定する必要があります。
:::

## NetworkConfigs の設定

**特定の広告ネットワークに対しての設定を行います。この NetworkConfig の設定は必須ではありません。<br>[メディエーション](./mediation.md)で使用する広告ネットワークに、どのような設定が可能か確認ができます。**

[初期化](./init.md)時に任意のネットワーク設定を行うことで、その広告ネットワークのオブジェクトに対して同じ設定が反映されます。下記は MixViewAd 生成時に AppLovin の AppLovinBannerConfig に対して設定しています。

:::: tabs

::: tab Java

```java
mMixViewAd.setNetworkConfigs(NetworkConfigs.Builder()
                .addConfig(AppLovinBannerConfig.Builder()
                            //  自動破棄の設定
                            .setAutoDestroy(false)
                            .build())
                //  その他の広告ネットワークの設定を追加する
                .addConfig(...)
            .build());
```
:::

::: tab Kotlin

```kotlin
mMixViewAd.setNetworkConfigs(NetworkConfigs.Builder()
                .addConfig(AppLovinBannerConfig.Builder()
                            //  自動破棄の設定
                            .setAutoDestroy(false)
                            .build())
                //  その他の広告ネットワークの設定を追加する
                .addConfig(...)
            .build())
```
:::

::::

## 広告のロード
広告をロードするためには、`MixViewAd` オブジェクトの `loadAd()` を使用します。

:::: tabs

::: tab Java

```java
mMixViewAd.loadAd();
```

:::

::: tab Kotlin

```kotlin
mMixViewAd.loadAd()
```

:::

::::

## 広告イベント
AdListener を用いて、広告のロード完了のタイミングや、ユーザーがアプリを閉じたタイミングなどの、広告のライフサイクルで発生する様々なイベントを取得することができます。

### MixViewAd イベントを登録する
MixViewAd のイベントのサイクルを取得するには、`SimpleAdListener` インスタンスを作成し、`setAdListener()` で登録します。

:::: tabs

::: tab Java

```java
mMixViewAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        // 広告のロード完了
        Log.d(TAG, "on MixViewAd Loaded");
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 広告の読み込み失敗、エラー詳細は adError から取得
        Log.d(TAG, "on MixViewAd FailedToLoad err: " + adError.toString());
    }

    @Override
    public void onAdShown() {
        // 広告を表示
        Log.d(TAG, "on MixViewAd Shown");
    }

    @Override
    public void onAdClicked() {
        // 広告をクリック
        Log.d(TAG, "on MixViewAd Clicked");
    }
});

mMixViewAd.loadAd();
```
:::

::: tab Kotlin

```kotlin
mMixViewAd.adListener = object: SimpleAdListener() {
    override fun onAdLoaded() {
        // 広告のロード完了
        println("on MixViewAd Loaded")
    }

    override fun onAdFailedToLoad(adError: AdError?) {
        //  広告の読み込み失敗、エラー詳細は adError から取得
        println("on MixViewAd FailedToLoad err: " + adError.toString())
    }

    override fun onAdShown() {
        //  広告を表示
        println("on MixViewAd Shown")
    }

    override fun onAdClicked() {
        //  広告をクリック
        println("on MixViewAd Clicked")
    }
}

mMixViewAd.loadAd()
```

:::

::::

### 広告のロードエラーについて
広告の読み込に失敗した場合は、AdListener の `onAdFailedToLoad(AdError adError)` が呼び出されます。その際に `adError.getCode()`、`adError.toString()` から、エラーコード、エラー情報が取得できます。

#### エラーコードとエラーメッセージについて

[エラー情報](./error.md#エラーコードとエラーメッセージ)を確認してください。

## 広告の表示
MixViewAd のネイティブ広告とフィードリスト広告のレイアウトはカスタマイズが可能です。
また、AdLime SDK には ネイティブ広告を表示するための、様々なレイアウトが用意されています。<br>
MixViewAd の `getAdView()` を使用して、広告の要素が配置された View を取得できます。View の構成は NativeAdLayout の各レイアウトと同じです。<br>
この View を適切な箇所に追加することで、ネイティブ広告が表示できます。

** `NativeAdLayout`については、[NativeAdLayout](./native.md#広告レイアウトの作成)で確認できます。**

:::: tabs

::: tab Java

```java
mMixViewAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        NativeAdLayout layout = NativeAdLayout.getLargeLayout1();
        View view = mMixViewAd.getAdView(layout);
        if(view != null) {
            mMixViewAdContainer.removeAllViews();
            mMixViewAdContainer.addView(view);
        }
    }
});

mMixViewAd.loadAd();
```

:::

::: tab Kotlin

```kotlin
mMixViewAd.adListener = object: SimpleAdListener() {
    override fun onAdLoaded() {
        val layout = NativeAdLayout.getLargeLayout1()
        val view = mMixViewAd.getAdView(layout)
        if(view != null) {
            mMixViewAdContainer.removeAllViews()
            mMixViewAdContainer.addView(view)
        }
    }
}

mMixViewAd.loadAd()
```

:::

::::

::: tip
MixViewAdを作成し、広告をロードする前にレイアウトを設定すると、`getAdView()` のみで、View を取得ができます。

:::: tabs

::: tab Java

```java
NativeAdLayout layout = NativeAdLayout.getLargeLayout1();
mMixViewAd.setNativeAdLayout(layout);

mMixViewAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        View view = mMixViewAd.getAdView();
        if(view != null) {
            mMixViewAdContainer.removeAllViews();
            mMixViewAdContainer.addView(view);
        }
    }
});

mMixViewAd.loadAd();
```

:::

::: tab Kotlin

```kotlin
val layout = NativeAdLayout.getLargeLayout1()
mMixViewAd.setNativeAdLayout(layout)

mMixViewAd.adListener = object : SimpleAdListener() {
    override fun onAdLoaded() {
        val view = mMixViewAd?.adView
        if (view != null) {
            mMixViewAdContainer.removeAllViews()
            mMixViewAdContainer.addView(view)
        }
    }
}

mMixViewAd.loadAd()
```

:::

::::

## プリロードとキャッシュ
事前に広告をロードをして、表示までの待ち時間を極力抑えましょう。<br>
また広告をプリロードする・しないに関わらず、広告をキャッシュすることをおすすめします。広告枠では、各広告ネットワークの広告がロードされますが、広告枠の1つのインスタンスを繰り返し使用することで、高いインプレッションを得られ、不要なリクエストも抑えることができます。これらは、[AdLimeLoader](./adloader.md)で実現が可能です。