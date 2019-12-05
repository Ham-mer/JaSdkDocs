#  MixFullScreenAd
インタースティシャル広告の場合に、普通のNetworkはインタースティシャル広告しか使えない。広告のfill率は低い場合に、広告は展示されない。MixFullScreenAdで広告をリクエストする時に、インタースティシャルだけではなく、バナー、ネイティブ、フィードリストもリクエストできる そうすると、広告容器のfill率とマネタイズ能力を高める。

MixFullScreenAdは今バナー、ネイティブ、フィードリスト、インタースティシャルをサポートする。MixFullScreenAdでフィードリストは一回しかリクエストしない。

本ガイドは MixFullScreenAd広告をAndroid アプリに組み込むについて紹介する。

## 前提条件
- AdLime SDKの導入

## 创建 MixFullScreenAd
MixFullScreenAd はMixFullScreenAdのオブジェクトでリクエストと展示され 。まずはMixFullScreenAdを実例化してAdunit IDを設置する。

```java
MixFullScreenAd mMixFullScreenAd = new MixFullScreenAd(context);
mMixFullScreenAd.setAdUnitId("AdUnit_ID");
```

::: tip
もし広告枠にFlurry/Unity Adsのバナー広告がある場合にコンストラクタにActivityを送る必要がある。<br>
もし広告枠にAdColony/Flurry/Unity Ads のインタースティシャル広告がある場合にコンストラクタにActivityを送る必要がある。。
:::

## 広告タイプの設置
広告をロードする前に、ネイティブ、、フィードリストのレイアウトを設置する。。

```java
mMixFullScreenAd.setNativeAdLayout(NativeAdLayout.getFullLayout1());
```

**NativeAdLayoutについて[NativeAdLayout](https://www.adlime.net/docs/ja/integration/android/native.html#%E5%BA%83%E5%91%8A%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)で確認できる。**

## 広告ロード　
MixFullScreenAd をロードするために， MixFullScreenAd のオブジェクトの loadAd() 方法を使ってください

```java
mMixFullScreenAd.loadAd();
```

## 広告展示
 MixFullScreenAdを展示するために，isReady() で広告のロードを確認して方 show()を調達する。

```java
if (mMixFullScreenAd.isReady()) {
    // パラメーターはbackボタンで広告を閉じることを許すかどうかを表する。
    // true は許すと表する。
    mMixFullScreenAd.show(true);

    // パラメーターを送らないと許さないと表する。
    // mMixFullScreenAd.show();
}
```

## 広告イベント
さらに広告行為を定義するために、広告のライフサイクルに各イベントを追加できる。例えばロード、開く、閉じるなど。 AdListenerでモニターできる。

 MixViewAdでAdListenerを使うために， setAdListener() 方法を使ってください：

```java
mMixFullScreenAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        // ロード成功
    }

    @Override
    public void onAdFailedToLoad(AdError adError) {
        // ロード失敗，adError はエラー情報
        Log.d(TAG, "onAdFailedToLoad: " + adError.toString());
    }

    @Override
    public void onAdShown() {
        // 広告展示
    }

    @Override
    public void onAdClicked() {
        // 広告クリック
    }

    @Override
    public void onAdClosed() {
        // 広告閉じる
    }
});

mMixFullScreenAd.loadAd();
```

### エラー情報
広告ロード失敗の時に、 AdListener の onAdFailedToLoad(AdError adError)はコールバックされる 。 adError.getCode()、adError.toString()でエラーコードとエラー情報を取得できる。

エラーコードの定義は AdErrorにある：
|定義                        |説明     |
|:--------------------------|:--------|
|ERROR_CODE_INTERNAL_ERROR  | 内部エラー |
|ERROR_CODE_INVALID_REQUEST | 無効リクエスト |
|ERROR_CODE_NETWORK_ERROR   | 网ネットエラー |
|ERROR_CODE_NO_FILL         | no fill   |
|ERROR_CODE_TIMEOUT         | リクエスト　タイムアウト |

エラー情報は AdUnit 、Network、LineItem の情報を含める、例は下記通り：
```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## プリロードとキャッシュ
プリロードで広告を事前に用意できて展示までの時間を短くする。<br>
プリロードに問わず、広告をキャッシュすることはお勧め。りゆうとして、一つのAdUnitにいくつかのLineitemはロード成功される。同じ広告オブジェクトを重複しようすると展示率を高めて必要ではない広告リクエストも減らせる。
自分の方法で広告をキャッシュできるし、 [AdLimeLoader](./adloader.md)で広告をキャッシュできる。