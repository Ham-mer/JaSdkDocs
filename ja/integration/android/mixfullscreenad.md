#  MixFullScreenAd
MixFullScreenAd はフルスクリーンで表示することができるインタースティシャル広告を拡張した機能です。また、インタースティシャル広告を表示するだけではなく、バナー広告やネイティブ広告なども同じ広告枠にフルスクリーン表示することができます。各ネットワークの提供する広告は、個別のフォーマットで独立した広告が提供されていました。この機能を実装することにより、1つの広告枠で表示できる広告の種類と数を増やし、より高い効率で収益を増やすことができます。

MixFullScreenAd は[バナー広告](./banner.md)と[ネイティブ広告](./native.md)と[インタースティシャル広告](./Interstitial.md)をサポートしています。このガイドでは、MixFullScreenAd を Android のアプリに実装する方法を紹介します。

## 前提条件
- AdLime SDK が導入済みであること

## MixFullScreenAd の作成 
`MixFullScreenAd` オブジェクトとして 広告ユニット ID を設定し、オブジェクトを作成します。

:::: tabs

::: tab Java

```java
MixFullScreenAd mMixFullScreenAd = new MixFullScreenAd(context);
mMixFullScreenAd.setAdUnitId("AdUnit_ID");
```

:::

::: tab Kotlin

```kotlin
val mMixFullScreenAd = MixFullScreenAd(this)
mMixFullScreenAd.setAdUnitId("AdUnit_ID")
```

:::

::::

::: tip
広告枠に Flurry / Unity Ads のバナー広告がある場合は、コンストラクタの引数として Activity を設定する必要があります。<br>
広告枠に AdColony / Flurry / Unity Ads のインタースティシャル広告がある場合は、コンストラクタの引数として Activity 設定する必要があります。
:::


## ネイティブ広告のレイアウト
`MixFullScreenAd` オブジェクトを生成したら、広告をロードする前にネイティブ広告のレイアウトを設定しておきましょう。ネイティブ広告のレイアウトは AdLime SDK の`AdLimeNativeAdLayout`によって管理します。また、ネイティブ広告のレイアウトはカスタムで設定できます<br>。

:::: tabs

::: tab Java

```java
mMixFullScreenAd.setNativeAdLayout(NativeAdLayout.getFullLayout1());
```

:::

::: tab Kotlin

```kotlin
mMixFullScreenAd.setNativeAdLayout(NativeAdLayout.getFullLayout1())
```

:::

::::

** `NativeAdLayout` については、[NativeAdLayout](https://www.adlime.net/docs/ja/integration/android/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90) で確認できます。**

## 広告のロード
広告をロードするためには、MixFullScreenAd オブジェクトの loadAd() を使用します。

:::: tabs

::: tab Java

```java
mMixFullScreenAd.loadAd();
```
:::

::: tab Kotlin

```kotlin
mMixFullScreenAd.loadAd()
```

:::

::::

## 広告の表示
広告をロードしたら広告を表示してみましょう。広告を表示する前に、広告がロード済みであるかを isReady で確認し show で表示します。

:::: tabs

::: tab Java

```java
if (mMixFullScreenAd.isReady()) {
    // 引数に true を設定すると、バックキーで広告を閉じる。
    // 引数を設定しない場合は、バックキーで広告は閉じない。
    mMixFullScreenAd.show(true);
}
```

:::

::: tab Kotlin

```kotlin
if (mMixFullScreenAd.isReady) {
    // 引数に true を設定すると、バックキーで広告を閉じる。
    // 引数を設定しない場合は、バックキーで広告は閉じない。
    mMixFullScreenAd.show(true)
}
```

:::

::::

## 広告イベント
AdListener を用いて、広告のロード完了のタイミングや、ユーザーがアプリを閉じたタイミングなどの、広告のライフサイクルで発生する様々なイベントを取得することができます。

### MixFullScreenAd イベントを登録する
MixFullScreenAd のイベントを取得するには、`SimpleAdListener` クラスの各デリゲートを定義し、`setAdListener()` で登録します。

:::: tabs

::: tab Java

```java
mMixFullScreenAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        // 広告のロード完了
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 広告の読み込み失敗、エラー詳細は adError から取得
        Log.d(TAG, "onAdFailedToLoad: " + adError.toString());
    }

    @Override
    public void onAdShown() {
        // 広告を表示
    }

    @Override
    public void onAdClicked() {
        // 広告をクリック
    }

    @Override
    public void onAdClosed() {
        // 広告を閉じる
    }
});

mMixFullScreenAd.loadAd();
```

:::

::: tab Kotlin

```kotlin
mMixFullScreenAd.setAdListener(object: SimpleAdListener() {
    override fun onAdLoaded() {
        // 広告のロード完了
    }

    override fun onAdFailedToLoad(adError: AdError?) {
        //  広告の読み込み失敗、エラー詳細は adError から取得
        print("onAdFailedToLoad: " + adError.toString())
    }

    override fun onAdShown() {
        //  広告を表示
    }

    override fun onAdClicked() {
        //  広告をクリック
    }

    override fun onAdClosed() {
        //  広告を閉じる
    }
})

mMixFullScreenAd.loadAd()
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