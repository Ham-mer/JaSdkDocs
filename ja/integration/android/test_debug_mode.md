# テストモードとデバッグモードの設定

AdLimeのメディエーション機能を用いることで数多くの広告ネットワークを組み込んで運用することが可能です。多くの広告ネットワークの運用には多くの問題を抱えることになるでしょう。テストモードとデバッグモードはこのような問題をサポートします。

テストモードは各広告ネットワークでテスト広告を表示するために必要な初期化を自動で設定します。テスト広告を表示する際にはテストモードを設定しましょう。

デバッグモードは各広告ネットワークで広告を初期化・ロード・表示等で実行される詳細なログを抽出することが可能です。広告表示に問題があった場合、どのような問題が発生したかを確認する場合にはデバッグモードを設定しましょう。

テストモードとデバッグモードの設定方法は[初期化](./init.md)のsetNetworkTestMode と setNetworkDebugMode を参考してください。

:::: tabs

::: tab Java

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    ...
    AdLime.getDefault().init(this, "YOUR APP ID");
    ...

    // Network テストモード、アプリ公開時にはfalse にする必要があります
    // AdLime.getDefault().setNetworkTestMode(true);
    // Network デバッグモード
    // AdLime.getDefault().setNetworkDebugMode(true);

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

    // Network テストモード、アプリ公開時にはfalse にする必要があります
    // AdLime.getDefault().setNetworkTestMode(true)
    // Network デバッグモード
    // AdLime.getDefault().setNetworkDebugMode(true)
    ...
```

:::

::::


AdLime はすべてのアドネットワークのテストモードとデバッグモードをサポートしていません。下記のリストではテストモードとデバッグモードをサポートしている広告ネットワークを示しています。

テストモードをサポートしない広告ネットワークを使いたい場合、何も設定する必要はありません。[テスト広告枠](./test.md)の アプリ ID と 広告枠 ID を設定することで、テスト広告を表示することが可能です。

| 序号 | ネットワーク                                 | テストモード | デバッグモード|
|:---:|:------------------------------------------:|:-------:|:-------:|
| 1   | [AdColony](./mediation_adcolony.md)        | ◯        |         |
| 2   | [AdGeneration](./mediation_adgeneration.md)| ◯        |         |
| 3   | [AdMob](./mediation_admob.md)              |         |         |
| 4   | [Amazon](./mediation_amazon.md)            | ◯       |         |
| 5   | [AppLovin](./mediation_applovin.md)        | 管理画面により設定可能       | ◯ |
| 6   | [Chartboost](./mediation_chartboost.md)    |         | ◯       |
| 7   | [Criteo](./mediation_criteo.md)            |         |         |
| 8   | [DFP](./mediation_dfp.md)                  |         |         |
| 9   | [Display.IO](./mediation_display_io.md)    |         |         |
| 10  | [DU Ad Platform](./mediation_du_ad_platform.md) | ◯       |         |
| 11  | [Facebook](./mediation_facebook.md)        | ◯       | ◯       |
| 12  | [Five](./mediation_five.md)                | ◯       |         |
| 13  | [Flurry](./mediation_flurry.md)            |         | ◯        |
| 14  | [Fyber](./mediation_fyber.md)              |         | ◯        |
| 15  | [i-mobile](./mediation_imobile.md)         |         |         |
| 16  | [InMobi](./mediation_inmobi.md)            |         | ◯        |
| 17  | [IronSource](./mediation_ironsource.md)    |         |         |
| 18  | [Maio](./mediation_maio.md)                | ◯        |         |
| 19  | [MoPub](./mediation_mopub.md)              |         | ◯        |
| 20  | [Nend](./mediation_nend.md)                |         | ◯        |
| 21  | [Pangle](./mediation_pangle.md)            |         | ◯        |
| 22  | [Tapjoy](./mediation_tapjoy.md)            |         | ◯        |
| 23  | [Unity Ads](./mediation_unity_ads.md)      | ◯       | ◯       |
| 24  | [Vungle](./mediation_vungle.md)            |         |         |
