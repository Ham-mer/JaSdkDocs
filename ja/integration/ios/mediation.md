# メディエーション
メディエーションとは、複数広告ネットワークを管理し、各ネットワークの中から広告収益を最大化する広告をアプリに配信する仕組みです。メディエーション機能を使用することで複数広告ネットワークに広告リクエストを送信し、配信可能かつ独自アルゴリズムにより最適化された広告を特定、掲載することができます。

このガイドでは AdLime から iOS アプリにメディエーションを導入する方法について説明します。

##  前提条件

メディエーション機能導入前に、導入予定の広告フォーマットが検討済みであること

- [バナー広告の導入](./banner.md)
- [インタースティシャル広告の導入](./Interstitial.md)
- [ネイティブ広告の導入](./native.md)
- [動画リワード広告の導入](./rewarded.md)
- [MixViewAd 広告の導入](./mixviewad.md)
- [MixFullScreenAd 広告の導入](./mixfullscreenad.md)

## 広告ネットワークを選択する

AdLime は、さまざまな広告ネットワークに対応しています。ここでは対応している広告ネットワークとその導入手順を説明します。まず導入予定の広告ネットワークについて以下の手順に従ってください。

 1. 導入予定の各広告ネットワークのコンソール上で、アプリと広告枠を登録します。
 2. AdLime コンソールのアカウントを取得し、アプリと広告枠を登録します。そして、AdLime の 広告枠に各広告ネットワークの広告枠の情報を関連付けします。
 3. 各広告ネットワークの SDK とそれに対応したメディエーション SDK を追加します。

AdLime で利用可能な広告ネットワーク一覧

**各ネットワークの広告フォーマット欄に ◯ の記載がある場合に、その広告フォーマットを使用可能**

| No  |  ネットワーク                 | バナー | インターステーシャル  | 動画リワード | ネイティブ | 最新バージョン |
|:---:|:-------------------------------------:|:------:|:----:|:--------:|:------:|:--------:|
| 1   | [AdColony](./mediation_adcolony.md)        | ◯      | ◯    | ◯        |        | 4.1.2    |
| 2   | [AdGeneration](./mediation_adgeneration.md)| ◯      | ◯    |          | ◯      | 2.16.4   |
| 3   | [AdMob](./mediation_admob.md)              | ◯      | ◯    | ◯        | ◯      | 7.52.0   |
| 4   | [Amazon](./mediation_amazon.md)            | ◯      | ◯    |          |        | 2.2.17   |
| 5   | [AppLovin](./mediation_applovin.md)        | ◯      | ◯    | ◯        |     ◯  | 6.11.4   |
| 6   | [Chartboost](./mediation_chartboost.md)    | ◯      | ◯    | ◯        |        | 8.0.3    |
| 7   | [Criteo](./mediation_criteo.md)            | ◯      | ◯    |          |        | 3.2.0    |
| 8   | [DFP](./mediation_dfp.md)                  | ◯      | ◯    | ◯        | ◯      | 7.52.0   |
| 9   | [Display.IO](./mediation_display_io.md)    | ◯      | ◯    |    ◯     |        | 2.8.0    |
| 10  | [DU Ad Platform](./mediation_du_ad_platform.md) | ◯ | ◯    |          | ◯      | 1.1.4    |
| 11  | [Facebook](./mediation_facebook.md)        | ◯      | ◯    | ◯        | ◯      | 5.6.0    |
| 12  | [Five](./mediation_five.md)                | ◯      | ◯    | ◯        |        | 20191223 |
| 13  | [Flurry](./mediation_flurry.md)            | ◯      | ◯    | ◯        | ◯      | 10.0.2   |
| 14  | [Fyber](./mediation_fyber.md)              | ◯      | ◯    | ◯        |        | 7.4.1    |
| 15  | [i-mobile](./mediation_imobile.md)         | ◯      | ◯    |          | ◯      | 2.0.31   |
| 16  | [IronSource](./mediation_ironsource.md)    | ◯      | ◯    | ◯        |        | 6.10.0.0 |
| 17  | [Maio](./mediation_maio.md)                |        | ◯    | ◯        |        | 1.5.3    |
| 18  | [MoPub](./mediation_mopub.md)              | ◯      | ◯    | ◯        | ◯      | 5.11.0   |
| 19  | [Nend](./mediation_nend.md)                | ◯      | ◯    | ◯        | ◯      | 5.4.0    |
| 20  | [Tapjoy](./mediation_tapjoy.md)            |        | ◯    | ◯        |        | 12.3.4   |
| 21  | [TikTok](./mediation_tiktok.md)            |        | ◯    | ◯        | ◯      | 2.8.0.1  |
| 22  | [Unity Ads](./mediation_unity_ads.md)      | ◯      | ◯    | ◯        |        | 3.3.0    |
| 23  | [Vungle](./mediation_vungle.md)            | ◯      | ◯    | ◯        | ◯      | 6.4.5    |


## 次のステップ
- 必要な SDK を導入したら、[広告フォーマットの選択](./adformat.md)に従い、ご希望の広告フォーマットを選択し、iOSアプリに実装しましょう

