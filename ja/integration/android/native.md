# ネイティブ広告

ネイティブ広告は、プラットフォームに備わっている UI コンポーネントを通じて、ユーザーに表示される広告のクリエイティブです。作成済みのレイアウトに溶け込むように表示され、アプリの視覚デザインに合わせるフォーマットになり、ユーザーエクスペリエンスへの影響を最小限に抑えることができます。コーディングの観点からすれば、ネイティブ広告を読み込む時に広告のクリエイティブを含む NativeAd オブジェクトをアプリが受け取り、（SDKではなく）アプリ自身で広告を表示する仕組みになります。

## 前提条件
- AdLime SDK が導入済みであること

## ネイティブ広告の作成

ネイティブ広告は、NativeAd クラスによって読み込みされます。まず NativeAd をインスタンス化し、その広告ユニットIDを設定してください。

```java
// 広告ユニットID の定義
String native_test = "4202d9c4-c08c-4cc9-9810-678a1ae52811";
// NativeAd を生成
NativeAd mNativeAd = new NativeAd(context);
mNativeAd.setAdUnitId(native_test);
```

## 広告レイアウトの作成

NativeAd で広告を受け取った後、各要素に割り当てます。 AdLime SDKでは、ネイティブ広告要素のレイアウトをコーディングによって行うか、 SDK に含まれる各広告フォーマットを使用するか選択することができます。

### NativeAdLayout.Builder

ネイティブ広告の要素は、 NativeAdLayout.Builder によって 広告ページ と ネイティブ広告の要素をバインディングすることができます。

### NativeAdLayout.Builder メソッド一覧

| メソッド               | ビュータイプ | 詳細                                  | 操作                                      |
| -------------------- | --------- | -------------------------------------- | ---------------------------------------------- |
| setLayoutId          | ViewGroup | 親レイアウト                              | M                                              |
| setMediaViewLayoutId | ViewGroup | メディアレイアウト                       | MediaViewLayout もしくは IconLayout どちらか1つ以上 |
| setMediaImageScaleType| ScaleType| メディアの画像スケールタイプ            | O, デフォルトは ScaleType.FIT_CENTER        |
| setIconLayoutId      | ViewGroup | ロゴの URL / アプリのロゴ                    | MediaViewLayout もしくは IconLayout どちらか1つ以上 |
| setIconScaleType     | ScaleType | ロゴのスケールタイプ                      | O, デフォルトは ScaleType.FIT_CENTER        |
| setAdChoicesLayoutId | ViewGroup | 広告選択レイアウト                             | M                                              |
| setTitleId           | TextView  | タイトル                                 | M                                              |
| setCallToActionId    | TextView  | アクションボタン                         | M                                              |
| setAdvertiserId      | TextView  | 広告主 / オフィシャルサイト           | O                                              |
| setSubTitleId        | TextView  | サブタイトル                           | O                                              |
| setBodyId            | TextView  | 本文                                   | O                                              |
| setRatingBarId       | RatingBar | 評価レーティングバー                               | O                                              |
| setRatingTextViewId  | TextView  | アプリストアでの評価レート（例：4.5）                    | O                                              |
| setStoreId           | TextView  | アプリストア（例：Google Play）          | O                                              |
| setPriceId           | TextView  | アプリストアの価格（例：無料）                 | O                                              |  
### レイアウトをカストマイズする

NativeAdLayaout メソッドを使用して、各要素の設定を行い、ビューグループをカスタマイズすることが可能です。
以下のコードを参考にしてください。

```java
// Sample one：customize
NativeAdLayout layout = new NativeAdLayout.Builder()
    // User customized control ID
    .setLayoutId(R.layout.layout_nativead)
    .setTitleId(R.id.textview_title)
    ......
    .build();
mNativeAd.setNativeAdLayout(layout);
```
### AdLime のビルトイン レイアウトを使用する

AdLime のビルトイン レイアウトで 広告を表示することもできます。

```java
mNativeAd.setNativeAdLayout(NativeAdLayout.getLargeLayout1());
```
### 切替可能なレイアウトを使用する

AdLime SDK は ケースに応じてレイアウトを変更できるインターフェイスを提供します。以下のコードを参考にしてください。

```java
// 方法 1
mNativeAd.setNativeAdLayout(new INativeAdLayoutPolicy() {
    @Override
    public NativeAdLayout getNativeAdLayout(ILineItem lineItem) {
        // lineItem に指定するレイアウトによってカスタマイズが可能
        return null;
    }
});

// 方法 2
// 順番に表示されるレイアウト
mNativeAd.setNativeAdLayout(new SequenceNativeAdLayoutPolicy.Builder()
    .add(layout)
    .add(NativeAdLayout.getMediumLayout())
    .build());
// ランダムに表示されるレイアウト
mNativeAd.setNativeAdLayout(new RandomNativeAdLayoutPolicy.Builder()
    .add(layout)
    .add(NativeAdLayout.getSmallLayout())
    .build());
```

### 広告インタラクティブエリアを設定する
広告のインタラクティブエリアを設定することにより、ネイティブ広告の各要素のクリック可否が設定できます。設定しない場合は、すべての要素をクリックが可能です。<br>
以下は、 NativeAdLayout オブジェクトの InteractiveArea を設定するサンプルコードです。
```
NativeAdLayout layout = NativeAdLayout.Builder()
    ......
    .setInteractiveArea(
        InteractiveArea.Builder()
                .addTitle()
                .addBody()
                .addCallToAction()
                .addIconLayout()
                .addMediaViewLayout()
                .build()
    )
    .build();
```
上記の例では，指定した要素がインタラクティブエリアに含まれます
- タイトル・本文・アクションボタン・メディア・アイコン
.addXxx(Xxxは要素名) をコードに追加することで、インタラクティブエリアに要素を追加することになります。

## レイアウトの読み込み
loadAd() メソッドで広告を読みます。

```java
mNativeAd.loadAd();
```

## 広告イベント

広告の動作をより細かくカスタマイズするには、広告のライフサイクルで発生する様々なイベント（読み込み、開始、終了など）を追加することができ、AdListener クラスを使い、これらのイベントを受け取ることができます。

NativeAd オブジェクトで AdListener を利用するには、 setAdListener() メソッドを呼び出してください。

```java
mNativeAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdFailedToLoad(AdError adError) {
        // 広告の読み込み失敗
        Log.d(TAG, "on BannerAd FailedToLoad err:" + adError.toString());
    }

    @Override
    public void onAdLoaded() {
        // 広告のロード完了
    }

    @Override
    public void onAdClosed() {
        // 広告を閉じる
        Log.d(TAG, "on BannerAd Closed");
    }

    @Override
    public void onAdClicked() {
        // 広告をクリック
        Log.d(TAG, "on BannerAd Clicked");
    }

    @Override
    public void onAdShown() {
        // 広告を表示
        Log.d(TAG, "on BannerAd Shown");
    }
});
```

### エラーの情報
広告の読み込に失敗した場合は、AdListener の onAdFailedToLoad(AdError adError) が呼び出されます。その際に adError.getCode()、 adError.toString() から、エラーコード、エラー情報が取得できます。

 AdError エラーコード一覧
|定義                        |説明     |
|:--------------------------|:--------|
|ERROR_CODE_INTERNAL_ERROR  | 内部エラー |
|ERROR_CODE_INVALID_REQUEST | リクエストが無効 |
|ERROR_CODE_NETWORK_ERROR   | ネットワークエラー |
|ERROR_CODE_NO_FILL         | 配信できる広告がない   |
|ERROR_CODE_TIMEOUT         | リクエスト　タイムアウト |

エラーは AdUnit、ネットワーク、ラインアイテムの各情報が含まれています。
```
ErrorCode is [3], Message is [No Fill]
AdUnit is ...
Network is ...
LineItem is ...
```

## ディスプレイ広告
広告が読み込まれると、適切な場所に表示できます。

```java
mNativeAd.setAdListener(new SimpleAdListener() {
    @Override
    public void onAdLoaded() {
        View view = mNativeAd.getAdView();
        if(view != null) {
            mNativeAdContainer.removeAllViews();
            mNativeAdContainer.addView(view);
        }
    }
});

mNativeAd.loadAd();
```

## ビルトイン ネイティブ広告レイアウト

AdLime SDK には様々な NativeAd レイアウトが用意されています。最適なレイアウトを活用し、開発の効率を上げることができます。

### 一般的な ネイティブ広告レイアウト

- カード小：`NativeAdLayout.getSmallLayout()`

レイアウト：`R.layout.adlime_nativead_small`

<img src="./../images/android/native_style/1-1.jpg" width="360" align=center />

- カード中：`NativeAdLayout.getMediumLayout()`

レイアウト：`R.layout.adlime_nativead_medium`

<img src="./../images/android/native_style/1-2.jpg" width="360" align=center />

- カード大 1：`NativeAdLayout.getLargeLayout1()`

レイアウト：`R.layout.adlime_nativead_large_1`

<img src="./../images/android/native_style/1-3-1.jpg" width="360" align=center />


- カード大 2：`NativeAdLayout.getLargeLayout2()`

レイアウト：`R.layout.adlime_nativead_large_2`

<img src="./../images/android/native_style/1-3-2.jpg" width="360" align=center />


- カード大 3：`NativeAdLayout.getLargeLayout3()`

レイアウト：`R.layout.adlime_nativead_large_3`

<img src="./../images/android/native_style/1-3-3.jpg" width="360" align=center />

- カード大 4：`NativeAdLayout.getLargeLayout4()`

レイアウト：`R.layout.adlime_nativead_large_4`

<img src="./../images/android/native_style/1-3-4.jpg" width="360" align=center />


#### フルスクリーン ネイティブ広告レイアウト

- スタイル 1：`NativeAdLayout.getFullLayout1()`

レイアウト：R.layout.adlime_nativead_full_1

<img src="./../images/android/native_style/2-1.jpg" width="270" align=center />


- スタイル 2：`NativeAdLayout.getFullLayout2()`

レイアウト：R.layout.adlime_nativead_full_2

<img src="./../images/android/native_style/3-1.jpg" width="270" align=center />


- スタイル 3：`NativeAdLayout.getFullLayout3()`

レイアウト：R.layout.adlime_nativead_full_3

<img src="./../images/android/native_style/4-1.png" width="270" align=center />

- スタイル 4：`NativeAdLayout.getFullLayout4()`

レイアウト：R.layout.adlime_nativead_full_4

<img src="./../images/android/native_style/5-1.png" width="270" align=center />

## プリロードとキャッシュ
プリロードで事前に広告を用意して展示するまでの時間を短くする<br>
広告をプリロードするかどうかにもかかわらず、広告をキャッシュすることはお勧め。理由としては一つのAdUnitに各LineItemはロードされるはずで、一つの広告インスタンスを繰り返して使うと、展示率を高めて必要ではないリクエストも減らせる。
自ら広告キャッシュを実現できるし、[AdLimeLoader](./adloader.md)でも実現できる。