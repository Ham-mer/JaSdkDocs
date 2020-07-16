# テストモードとデバッグモードの設定

AdLimeのメディエーション機能を用いることで数多くの広告ネットワークを組み込んで運用することが可能です。多くの広告ネットワークの運用には多くの問題を抱えることになるでしょう。テストモードとデバッグモードはこのような問題をサポートします。

テストモードは各広告ネットワークでテスト広告を表示するために必要な初期化を自動で設定します。テスト広告を表示する際にはテストモードを設定しましょう。

デバッグモードは各広告ネットワークで広告を初期化・ロード・表示等で実行される詳細なログを抽出することが可能です。特定のアドネットワークで広告のロードや表示に問題が発生した場合にはデバッグモードを設定し、ログを抽出・問題の調査をしましょう。

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


AdLime は一部の広告ネットワークで、テストモードとデバッグモードをサポートします。下記のリストではテストモードとデバッグモードをサポートしている広告ネットワークを示しています。

テストモードをサポートしない広告ネットワークを使用する場合、設定は必要はありません。[テスト広告枠](./test.md)の アプリ ID と 広告枠 ID を設定することで、テスト広告を表示することが可能です。

| 序号 | ネットワーク                                 | テストモード | デバッグモード|
|:---:|:------------------------------------------:|:-------:|:-------:|
| 1   | [AdGeneration](./mediation_adgeneration.md)| ◯       |         |
| 2   | [AdMob](./mediation_admob.md)              |         |         |
| 3   | [AppLovin](./mediation_applovin.md)        | 管理画面により設定可能 | ◯ |
| 4   | [Criteo](./mediation_criteo.md)            |         |         |
| 5   | [DFP](./mediation_dfp.md)                  |         |         |
| 6   | [Facebook](./mediation_facebook.md)        | ◯       | ◯       |
| 7   | [Five](./mediation_five.md)                | ◯       |         |
| 8   | [i-mobile](./mediation_imobile.md)         |         |         |
| 9   | [Maio](./mediation_maio.md)                | ◯       |         |
| 10  | [MoPub](./mediation_mopub.md)              |         | ◯       |
| 11  | [Nend](./mediation_nend.md)                |         | ◯       |
| 12  | [Pangle](./mediation_pangle.md)            |         | ◯       |