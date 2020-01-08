# メディエーション

メディエーションは、アプリに配信される全ての広告ソースを1か所で管理できる AdLime の機能です。メディエーションによって複数の広告ネットワークに広告をリクエストし、最適な広告ソースをみつけ掲載することができます。これにより収益を最大化することができます。

このガイドでは AdLime から iOS アプリにメディエーションを導入する方法について説明します。

##  前提条件

メディエーション導入前に、適切な広告フォーマットが導入済みであること

- [バナー広告の導入](./banner.md)
- [インタースティシャル広告の導入](./Interstitial.md)
- [ネイティブ広告の導入](./native.md)
- [動画リワード広告の導入](./rewarded.md)
- [MixViewAd 広告の導入](./mixviewad.md)
- [MixFullScreenAd 広告の導入](./mixfullscreenad.md)

## 広告ネットワークを選択する

AdLime は、さまざまな広告ネットワークに対応しています。メディエーションを導入する手順は下記の通りです。

 1. メディエーションをする広告ネットワークで、アプリと広告枠を登録します。
 2. AdLime コンソールのアカウントを取得し、アプリと広告枠を登録します。そして、AdLime の 広告枠に、メディエーションをする広告ネットワークの広告枠の情報を関連付けします。
 3. メディエーションする広告ネットワークの SDK を導入し、それらに対応した、 AdLime SDK を追加します。

AdLime で利用可能な広告ネットワーク一覧

| No  |  ネットワーク                 | バナー | インターステーシャル  | 動画リワード | ネティブ | 最新バージョン |
|:---:|:-------------------------------------:|:------:|:----:|:--------:|:------:|:--------:|
| 1   | [AdColony](./mediation_adcolony.md)        | ◯      | ◯    | ◯        | ◯      | 4.1.2    |
| 2   | [AdGeneration](./mediation_adgeneration.md)| ◯      | ◯    | ◯        | ◯      | 2.16.4   |
| 3   | [AdMob](./mediation_admob.md)              | ◯      | ◯    | ◯        | ◯      | 7.52.0   |
| 4   | [Amazon](./mediation_amazon.md)            | ◯      | ◯    |          |        | 2.2.17   |
| 5   | [AppLovin](./mediation_applovin.md)        | ◯      | ◯    | ◯        |        | 6.9.4    |
| 6   | [Chartboost](./mediation_chartboost.md)    | ◯      | ◯    | ◯        |        | 8.0.3    |
| 7   | [Criteo](./mediation_criteo.md)            | ◯      | ◯    |          |        | 3.2.0    |
| 8   | [DFP](./mediation_dfp.md)                  | ◯      | ◯    | ◯        | ◯      | 7.52.0   |
| 9   | [Display.IO](./mediation_display_io.md)    | ◯      | ◯    |          |        | 2.8.0    |
| 10  | [DU Ad Platform](./mediation_du_ad_platform.md) | ◯ | ◯    | ◯        |        | 1.1.4    |
| 11  | [Facebook](./mediation_facebook.md)        | ◯      | ◯    | ◯        | ◯      | 5.6.0    |
| 12  | [Five](./mediation_five.md)                | ◯      | ◯    | ◯        |        | 20191016 |
| 13  | [Flurry](./mediation_flurry.md)            | ◯      | ◯    | ◯        | ◯      | 10.0.2   |
| 14  | [Fyber](./mediation_fyber.md)              | ◯      | ◯    | ◯        |        | 7.4.1    |
| 15  | [i-mobile](./mediation_imobile.md)         | ◯      | ◯    |          | ◯       | 2.0.31 |
| 16  | [IronSource](./mediation_ironsource.md)    | ◯      | ◯    | ◯        |        | 6.10.0.0 |
| 17  | [Maio](./mediation_maio.md)                |        | ◯    | ◯        |        | 1.4.8    |
| 18  | [MoPub](./mediation_mopub.md)              | ◯      | ◯    | ◯        | ◯      | 5.10.0   |
| 19  | [Nend](./mediation_nend.md)                | ◯      | ◯    | ◯        | ◯      | 5.3.0    |
| 20  | [Tapjoy](./mediation_tapjoy.md)            |        | ◯    | ◯        |        | 12.3.4   |
| 21  | [TikTok](./mediation_tiktok.md)            | ◯      | ◯    | ◯        | ◯      | 2.5.1.5  |
| 22  | [Unity Ads](./mediation_unity_ads.md)      | ◯      | ◯    | ◯        |        | 3.3.0    |
| 23  | [Vungle](./mediation_vungle.md)            | ◯      | ◯    | ◯        | ◯      | 6.4.5    |