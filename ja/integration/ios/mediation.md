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
| 1   | [AdColony](./mediation_adcolony.md)        | Y      | Y    | Y        | Y      | 4.1.2    |
| 2   | [AdGeneration](./mediation_adgeneration.md)| Y      | Y    | Y        | Y      | 2.16.4   |
| 3   | [AdMob](./mediation_admob.md)              | Y      | Y    | Y        | Y      | 7.52.0   |
| 4   | [Amazon](./mediation_amazon.md)            | Y      | Y    |          |        | 2.2.17   |
| 5   | [AppLovin](./mediation_applovin.md)        | Y      | Y    | Y        |        | 6.9.4    |
| 6   | [Chartboost](./mediation_chartboost.md)    | Y      | Y    | Y        |        | 8.0.3    |
| 7   | [Criteo](./mediation_criteo.md)            | Y      | Y    |          |        | 3.2.0    |
| 8   | [DFP](./mediation_dfp.md)                  | Y      | Y    | Y        | Y      | 7.52.0   |
| 9   | [Display.IO](./mediation_display_io.md)    | Y      | Y    |          |        | 2.8.0    |
| 10  | [DU Ad Platform](./mediation_du_ad_platform.md) | Y | Y    | Y        |        | 1.1.4    |
| 11  | [Facebook](./mediation_facebook.md)        | Y      | Y    | Y        | Y      | 5.6.0    |
| 12  | [Five](./mediation_five.md)                | Y      | Y    | Y        |        | 20191016 |
| 13  | [Flurry](./mediation_flurry.md)            | Y      | Y    | Y        | Y      | 10.0.2   |
| 14  | [Fyber](./mediation_fyber.md)              | Y      | Y    | Y        |        | 7.4.1    |
| 15  | [IronSource](./mediation_ironsource.md)    | Y      | Y    | Y        |        | 6.10.0.0 |
| 16  | [Maio](./mediation_maio.md)                |        | Y    | Y        |        | 1.4.8    |
| 17  | [MoPub](./mediation_mopub.md)              | Y      | Y    | Y        | Y      | 5.10.0   |
| 18  | [Nend](./mediation_nend.md)                | Y      | Y    | Y        | Y      | 5.3.0    |
| 19  | [Tapjoy](./mediation_tapjoy.md)            |        | Y    | Y        |        | 12.3.4   |
| 20  | [TikTok](./mediation_tiktok.md)            | Y      | Y    | Y        | Y      | 2.5.1.2  |
| 21  | [Unity Ads](./mediation_unity_ads.md)      | Y      | Y    | Y        |        | 3.3.0    |
| 22  | [Vungle](./mediation_vungle.md)            | Y      | Y    | Y        | Y      | 6.4.5    |