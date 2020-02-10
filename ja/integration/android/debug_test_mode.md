# ネットワークを調整、テストモードに設定
AdLimeのメディエーション機能で、簡単に数多くのネットワークを組み込まれます。テストする時に、調整モードとテストモードに設定できます。問題が発生する時に、簡単に見つかれます。

設置方法は[初期化](./init.md)のsetNetworkDebugMode と setNetworkTestModeを参考してください。

:::: tabs

::: tab Java

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    ...
    AdLime.getDefault().init(this, "YOUR APP ID");
    ...

    // Network 調整モード
    // AdLime.getDefault().setNetworkDebugMode(true);
    // Network テストモード，公開時に閉じる必要があります
    // AdLime.getDefault().setNetworkTestMode(true);
    ...
}
...

```

:::

::: tab Kotlin

```kotlin
    ...
    AdLime.getDefault().init(applicationContext, "YOUR APP ID")
    ...

    // Network 調整モード
    // AdLime.getDefault().setNetworkDebugMode(true)
    // Network テストモード，公開時に閉じる必要があります
    // AdLime.getDefault().setNetworkTestMode(true)
    ...
```

:::

::::

すべてのネットワークはテストモードをサポートするわけはないです。下記のリストではAdlimeがネットワークごとにどこまでサポートできるかを説明します。

テストモードをサポートしないネットワークは[テスト広告枠](./test.md)でテストできます。

| 序号 | ネットワーク                                 |調整モード|テストモード|
|:---:|:------------------------------------------:|:-------:|:-------:|
| 1   | [AdColony](./mediation_adcolony.md)        |         | ◯       |
| 2   | [AdGeneration](./mediation_adgeneration.md)|         | ◯       |
| 3   | [AdMob](./mediation_admob.md)              |         |         |
| 4   | [Amazon](./mediation_amazon.md)            |         | ◯       |
| 5   | [AppLovin](./mediation_applovin.md)        | ◯       | Applovinの管理画面で設定できるのは|
| 6   | [Chartboost](./mediation_chartboost.md)    | ◯       |         |
| 7   | [Criteo](./mediation_criteo.md)            |         |         |
| 8   | [DFP](./mediation_dfp.md)                  |         |         |
| 9   | [Display.IO](./mediation_display_io.md)    |         |         |
| 10  | [DU Ad Platform](./mediation_du_ad_platform.md) |    | ◯       |
| 11  | [Facebook](./mediation_facebook.md)        | ◯       | ◯       |
| 12  | [Five](./mediation_five.md)                |         | ◯       |
| 13  | [Flurry](./mediation_flurry.md)            | ◯       |         |
| 14  | [Fyber](./mediation_fyber.md)              | ◯       |         |
| 15  | [i-mobile](./mediation_imobile.md)         |         |         |
| 16  | [InMobi](./mediation_inmobi.md)            | ◯       |         |
| 17  | [IronSource](./mediation_ironsource.md)    |         |         |
| 18  | [Maio](./mediation_maio.md)                |         | ◯       |
| 19  | [MoPub](./mediation_mopub.md)              | ◯       |         |
| 20  | [Nend](./mediation_nend.md)                | ◯       |         |
| 21  | [Pangle](./mediation_pangle.md)            | ◯       |         |
| 22  | [Tapjoy](./mediation_tapjoy.md)            | ◯       |         |
| 23  | [Unity Ads](./mediation_unity_ads.md)      | ◯       | ◯       |
| 24  | [Vungle](./mediation_vungle.md)            |         |         |
