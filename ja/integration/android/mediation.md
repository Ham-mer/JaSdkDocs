# メディエーション

メディエーションは、アプリに配信される全ての広告ソースを1か所で管理できる AdLime の機能です。メディエーションによって複数の広告ネットワークに広告をリクエストし、最適な広告ソースをみつけ掲載することができます。これにより収益を最大化することができます。

このガイドでは AdLime から Android アプリにメディエーションを導入する方法について説明します。

##  前提条件

メディエーション導入する前に、適切な広告フォーマットが導入済みであること

- [バナー広告を導入する](./banner.md)
- [インタースティシャル広告を導入する](./Interstitial.md)
- [ネイティブ広告を導入する](./native.md)
- [動画リワード広告を導入する](./rewarded.md)
- [MixViewAd 広告を導入する](./mixviewad.md)
- [MixFullScreenAd 広告を導入する](./mixfullscreenad.md)

## 広告ネットワークを選択する

 AdLime は、様々な広告ネットワークを対応しています。メディエーションを導入する手順は下記の通りです。

 1. メディエーションをする広告ネットワークで、アプリと広告枠を登録します。
 2. AdLime コンソールのアカウントを取得し、アプリと広告枠を登録します。そして、AdLime の 広告枠に、メディエーションをする広告ネットワークの広告枠の情報を関連付けします。
 3. メディエーションする広告ネットワークの SDK を導入し、アプリを更新します。

**下記の広告タイプで Y\* がNetworkConfigは設置できると指す**

AdLime で利用可能なアドネットワーク一覧
 
| 番号 | ネットワーク | バナー  | インタースティシャル | リワード | ネイティブ | 最新バージョン | 
|:---:| :--------------------------------------: | :----: | :----------: | :------: | :----: |:-------------: |
| 1   | [AdColony](./mediation_adcolony.md)      |        | Y            | Y        |        | 3.3.7          | 
| 2   | [AdGeneration](./mediation_adgeneration.md)| Y    | Y            |          | Y      | 2.15.1         | 
| 3   | [AdMob](./mediation_admob.md)            | Y      | Y            | Y        | Y      | 17.2.1         | 
| 4   | [Amazon](./mediation_amazon.md)          | Y      | Y            |          |        | 5.9.0          | 
| 5   | [AppLovin](./mediation_applovin.md)      | Y      | Y            | Y        | Y      | 9.9.2          | 
| 6   | [Chartboost](./mediation_chartboost.md)  |        | Y            | Y        |        | 7.3.1          |
| 7   | [Criteo](./mediation_criteo.md)          | Y      | Y            |          |        | 3.1.0          |
| 8   | [DFP](./mediation_dfp.md)                | Y      | Y            | Y        | Y      | 17.2.1         |
| 9   | [Display.IO](./mediation_display_io.md)  | Y      | Y            |          |        | 2.0.1.0        | 
| 10  | [DU Ad Platform](./mediation_du_ad_platform.md) | Y  | Y         |          | Y      | 1.2.2          | 
| 11  | [Facebook](./mediation_facebook.md)      | Y      | Y            | Y        | Y      | 5.6.0          | 
| 12  | [Five](./mediation_five.md)              | Y      | Y            | Y        |        | 20191029       |
| 13  | [Flurry](./mediation_flurry.md)          | Y      | Y            | Y        | Y      | 11.4.0         | 
| 14  | [Fyber](./mediation_fyber.md)            | Y      | Y            |          | Y      | 7.2.1          | 
| 15  | [InMobi](./mediation_inmobi.md)          | Y      | Y            | Y        | Y      | 7.2.2          | 
| 16  | [IronSource](./mediation_ironsource.md)  | Y      | Y            | Y        |        | 6.8.0.1        |
| 17  | [Maio](./mediation_maio.md)              |        | Y            | Y        |        | 1.1.10         | 
| 18  | [MoPub](./mediation_mopub.md)            | Y      | Y            | Y        | Y      | 5.8.0          |
| 19  | [Nend](./mediation_nend.md)              | Y      | Y            | Y        | Y      | 5.1.1          | 
| 20  | [Tapjoy](./mediation_tapjoy.md)          |        | Y            | Y        |        | 12.2.0         | 
| 21  | [TikTok](./mediation_tiktok.md)          | Y      | Y            | Y        | Y      | 2.5.2.6        |
| 22  | [Unity Ads](./mediation_unity_ads.md)    | Y      | Y            | Y        |        | 3.0.0          | 
| 23  | [Vungle](./mediation_vungle.md)          | Y      | Y            | Y        |        | 6.3.24         |
