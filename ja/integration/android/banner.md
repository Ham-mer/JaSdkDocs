# バナー広告

バナー広告とは、アプリのレイアウトにおいて特定の位置を占める矩形のイメージまたはテキスト広告です。アプリのレイアウトの一部に簡単に組み込むことが可能です。モバイル広告を初めて掲載する場合には、まずバナー広告から始めてみましょう。

このガイドでは バナー広告 を Android のアプリに実装する方法を説明します。

**<u>複合型広告枠を用いることでより効果的に広告収益を高めることができます。詳細は [MixViewAd](./mixviewad.md) をご確認ください。</u>**


## 前提条件
- AdLime SDK が導入済みであること

## レイアウトに BannerAdView を追加する

バナー広告を表示するには、まず広告を表示する Activity か Fragment のレイアウトに BannerAdView を追加する必要があります。該当するコンテナのレイアウトファイルにそれを追加することはお勧めの方法です。

:::: tabs

::: tab Java

```java
import com.access_company.adlime.core.api.ad.BannerAdView;

public class MainActivity extends AppCompatActivity {
    BannerAdView mBannerAdView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 広告ユニットID の定義
        String bannerId = "47033ec3-5bf9-4865-a5d7-d1fbb9f7fbc8";
        // BannerAdView を作成
        mBannerAdView = new BannerAdView(context);
        mBannerAdView.setAdUnitId(bannerId);
        // バナーのコンテナを取得
        ViewGroup container = findViewById(R.id.banner_container);
        // コンテナに BannerAdView を追加する
        container.addView(mBannerAdView);
    }
}
```
:::

::: tab Kotlin

```kotlin
import com.access_company.adlime.core.api.ad.BannerAdView

class MainActivity : AppCompatActivity() {
    lateinit var mBannerAdView: BannerAdView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // 広告ユニット ID の定義
        val bannerId = "47033ec3-5bf9-4865-a5d7-d1fbb9f7fbc8"
        // BannerAdView を生成
        mBannerAdView = BannerAdView(this)
        mBannerAdView.adUnitId = bannerId
        // バナーのコンテナを取得
        val container = findViewById(R.id.banner_container)
        // コンテナに BannerAdView を追加する
        container.addView(mBannerAdView)
    }
}
```
:::

::::


### バナーのサイズを設定します
AdLime管理画面ではバナー広告枠を新規登録する時にバナーのサイズを設定してください。BannerAdViewは設定されるサイズを使います。<br>もし、画面の横縦または端末の種類でバナーのサイズを設定したい場合に、BannerAdViewのsetAdSize(BannerAdSize adSize)でバナーのサイズを設定します。

:::: tabs

::: tab Java
- 画面の横縦でサイズを設定します
    ```java
    if (ScreenUtil.isScreenPortrait(this)) {
        mBannerAdView.setAdSize(BannerAdSize.BANNER_320_100);
    } else {
        mBannerAdView.setAdSize(BannerAdSize.BANNER_320_50);
    }
    ```

- 端末の種類でサイズを設定します
    ```java
    if (ScreenUtil.isTablet(this)) {
        mBannerAdView.setAdSize(BannerAdSize.BANNER_728_90);
    } else {
        mBannerAdView.setAdSize(BannerAdSize.BANNER_320_50);
    }
    ```
:::

::: tab Kotlin
- 画面の横縦でサイズを設定します
    ```kotlin
    if (ScreenUtil.isScreenPortrait(this)) {
        mBannerAdView.setAdSize(BannerAdSize.BANNER_320_100)
    } else {
        mBannerAdView.setAdSize(BannerAdSize.BANNER_320_50)
    }
    ```

- 端末の種類でサイズを設定します
    ```kotlin
    if (ScreenUtil.isTablet(this)) {
        mBannerAdView.setAdSize(BannerAdSize.BANNER_728_90)
    } else {
        mBannerAdView.setAdSize(BannerAdSize.BANNER_320_50)
    }
    ```
:::

::::

## NetworkConfigs の設置
**特定の広告ネットワークに対しての設定を行います。この NetworkConfig の設定は必須ではありません。<br>[メディエーション](./mediation.md)で使用する広告ネットワークに、どのような設定が可能か確認ができます。**

:::: tabs

::: tab Java

```java
mBannerAdView.setNetworkConfigs(NetworkConfigs.Builder()
                    .addConfig(AppLovinBannerConfig.Builder()
                            // 自動デストロイかどうかの設置
                            .setAutoDestroy(false)
                            .build())
                    .addConfig(...)
                .build());
```

:::

::: tab Kotlin

```kotlin
mBannerAdView.setNetworkConfigs(NetworkConfigs.Builder()
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

## 広告を読み込む

広告をロードするには、`BannerAdView` クラスの `loadAd()` を使用します。

:::: tabs

::: tab Java

```java
// 広告のロード
mBannerAdView.loadAd();
```

:::

::: tab Kotlin

```kotlin
// 広告のロード
mBannerAdView.loadAd()

```

:::

::::

これでアプリにバナー広告が表示できるようになりました。

## 広告イベント
広告の動作をより細かくカスタマイズするには、広告のライフサイクルで発生するイベント（読み込み、開始、終了など）を追加することができ、AdListener クラスを使い、これらのイベントを受け取ることができます。

### BannerAdView イベントを登録する
BannerAdView のイベントを取得するには、`SimpleAdListener` インスタンスを作成し、`setAdListener()` で登録します。

:::: tabs

::: tab Java

```java
mBannerAdView.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        // 広告のロード完了
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 広告の読み込み失敗、エラー詳細は adError から取得
        Log.d(TAG, "on BannerAd FailedToLoad err:" + adError.toString());
    }

    @Override
    public void onAdShown() {
        // 広告を表示
        Log.d(TAG, "on BannerAd Shown");
    }

    @Override
    public void onAdClicked() {
        // 広告をクリック
        Log.d(TAG, "on BannerAd Clicked");
    }

    @Override
    public void onAdClosed() {
        // 広告を閉じる
        Log.d(TAG, "on BannerAd Closed");
    }
});
```

:::

::: tab Kotlin

```kotlin
mBannerAdView.adListener = object: SimpleAdListener() {
    override fun onAdLoaded() {
        // 広告のロード完了
        print("on BannerAd Loaded")
    }

    override fun onAdFailedToLoad(adError: AdError?) {
        //  広告の読み込み失敗、エラー詳細は adError から取得
        print("onAdFailedToLoad: " + adError.toString())
    }

    override fun onAdShown() {
        //  広告を表示
        print("on BannerAd Shown")
    }

    override fun onAdClicked() {
        //  広告をクリック
        print("on BannerAd Clicked")
    }

    override fun onAdClosed() {
        //  広告を閉じる
        print("on BannerAd Closed")
    }
}
```

:::

::::

### 広告のロードのエラー
広告の読み込に失敗した場合は、AdListener の `onAdFailedToLoad(AdError adError)` が呼び出されます。その際に `adError.getCode()`、`adError.toString()` から、エラーコード、エラー情報が取得できます。

#### エラーコードとエラーメッセージについて

[エラー情報](./error.md#エラーコードとエラーメッセージ)を確認してください。

## バナーのサイズ

**注意：広告を配置するコンテナのサイズは、バナーのサイズと同じか、それ以上の大きさにする必要があります。コンテナにパディングがある場合は、それだけバナーを表示できるコンテナの領域が小さくなります。**  

標準のバナーサイズについて、下記の表をご参照ください。

サイズ（dp）|説明          |対応端末  
:-                         |:-            |:- 
|320 x 50                    |バナー      |スマートフォン・タブレット 
|320 x 100                   |バナー（大）      |スマートフォン・タブレット
|300 x 250                   |IABレクタングル（中）    |スマートフォン・タブレット
|468 x 60                    |IAB フルサイズバナー  |タブレット
|728 x 90                    |IAB ビッグバナー   |タブレット
|smart                     |スマートバナー        |スマートフォン・タブレット

### スマートバナー

スマートバナーは、画面のサイズや向きにかかわらず、横幅いっぱいに広告が表示されます。現在は一部の広告プラットフォームのみに対応しています。

## プリロードとキャッシュ
事前に広告をロードをして、表示までの待ち時間を極力抑えましょう。<br>
また広告をプリロードする・しないに関わらず、広告をキャッシュすることをおすすめします。広告枠では、各広告ネットワークの広告がロードされますが、広告枠の1つのインスタンスを繰り返し使用することで、高いインプレッションを得られ、不要なリクエストも抑えることができます。これらは、[AdLimeLoader](./adloader.md)で実現が可能です。


## 次へのステップ
- 他の広告フォーマットを追加で利用したい場合は[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、Android アプリに実装しましょう。
- 広告が正しく表示できるか確認したい場合は、[広告表示テスト](./test.md)に従い App ID と各広告ネットワークに対応する広告枠 ID を設定して、広告を表示してみましょう。