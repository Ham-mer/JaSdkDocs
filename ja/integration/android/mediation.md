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


AdLime で利用可能なアドネットワーク一覧

**各ネットワークの広告フォーマット欄に ◯ の記載がある場合に、その広告フォーマットを使用可能**

| 番号 | ネットワーク | バナー  | インタースティシャル | リワード | ネイティブ | 最新バージョン | 
|:---:| :--------------------------------------: | :----: | :----------: | :------: | :----: |:-------------: |
| 1   | [AdColony](./mediation_adcolony.md)      |        | ◯            | ◯        |        | 3.3.7          | 
| 2   | [AdGeneration](./mediation_adgeneration.md)| ◯    | ◯            |          | ◯      | 2.15.1         | 
| 3   | [AdMob](./mediation_admob.md)            | ◯      | ◯            | ◯        | ◯      | 18.3.0         | 
| 4   | [Amazon](./mediation_amazon.md)          | ◯      | ◯            |          |        | 5.9.0          | 
| 5   | [AppLovin](./mediation_applovin.md)      | ◯      | ◯            | ◯        | ◯      | 9.11.2         | 
| 6   | [Chartboost](./mediation_chartboost.md)  |        | ◯            | ◯        |        | 7.3.1          |
| 7   | [Criteo](./mediation_criteo.md)          | ◯      | ◯            |          |        | 3.1.0          |
| 8   | [DFP](./mediation_dfp.md)                | ◯      | ◯            | ◯        | ◯      | 18.3.0         |
| 9   | [Display.IO](./mediation_display_io.md)  | ◯      | ◯            |          |        | 2.0.1.0        | 
| 10  | [DU Ad Platform](./mediation_du_ad_platform.md) | ◯  | ◯         |          | ◯      | 1.2.2          | 
| 11  | [Facebook](./mediation_facebook.md)      | ◯      | ◯            | ◯        | ◯      | 5.7.1          | 
| 12  | [Five](./mediation_five.md)              | ◯      | ◯            | ◯        |        | 20191029       |
| 13  | [Flurry](./mediation_flurry.md)          | ◯      | ◯            | ◯        | ◯      | 11.4.0         | 
| 14  | [Fyber](./mediation_fyber.md)            | ◯      | ◯            |          | ◯      | 7.2.1          | 
| 15  | [i-mobile](./mediation_imobile.md)       | ◯      | ◯            |          | ◯      | 2.0.20         | 
| 16  | [InMobi](./mediation_inmobi.md)          | ◯      | ◯            | ◯        | ◯      | 7.2.2          |
| 17  | [IronSource](./mediation_ironsource.md)  | ◯      | ◯            | ◯        |        | 6.8.0.1        |
| 18  | [Maio](./mediation_maio.md)              |        | ◯            | ◯        |        | 1.1.10         | 
| 19  | [MoPub](./mediation_mopub.md)            | ◯      | ◯            | ◯        | ◯      | 5.11.0         |
| 20  | [Nend](./mediation_nend.md)              | ◯      | ◯            | ◯        | ◯      | 5.4.1          | 
| 21  | [Pangle](./mediation_pangle.md)          |        | ◯            | ◯        |        | 2.1.5.0        |
| 22  | [Tapjoy](./mediation_tapjoy.md)          |        | ◯            | ◯        |        | 12.2.0         | 
| 23  | [Unity Ads](./mediation_unity_ads.md)    | ◯      | ◯            | ◯        |        | 3.0.0          | 
| 24  | [Vungle](./mediation_vungle.md)          | ◯      | ◯            | ◯        |        | 6.3.24         |


## 次へのステップ
- 必要な SDK を導入したら、[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、Android アプリに実装しましょう。