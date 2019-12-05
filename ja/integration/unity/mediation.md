# メディエーション

メディエーションは、アプリに配信される全ての広告ソースを1か所で管理できる AdLime の機能です。メディエーションによって複数の広告ネットワークに広告をリクエストし、最適な広告ソースをみつけ掲載することができます。これにより収益を最大化することができます。

このガイドでは AdLime から Unity アプリにメディエーションを導入する方法について説明します。

##  前提条件

メディエーション導入前に、適切な広告フォーマットが導入済みであること

- [バナー広告の導入](./banner.md)
- [インタースティシャル広告の導入](./Interstitial.md)
- [動画リワード広告の導入](./rewarded.md)

## 広告ネットワークを選択する

AdLimeは、様々な広告ネットワークを対応しています。メディエーションを導入する手順は下記の通りです。

 1. メディエーションをする広告ネットワークで、アプリと広告枠を登録します。
 2. AdLime コンソールのアカウントを取得し、アプリと広告枠を登録します。そして、AdLime の 広告枠に、メディエーションをする広告ネットワークの広告枠の情報を関連付けします。
 3. メディエーションする広告ネットワークの SDK を導入し、アプリを更新します。

AdLime で利用可能なアドネットワーク一覧

| No  | ネットワーク                               | バナー |インターステーシャル|動画リワード| Android 版 | iOS 版   |
|:---:|:-------------------------------------:|:------:|:----:|:--------:|:-----------:|:---------:|
| 1   | [AdMob](./mediation_admob.md)         | Y      | Y    | Y        | 17.2.1      | 7.52.0    |
| 2   | [Amazon](./mediation_amazon.md)       | Y      | Y    |          | 5.9.0       | 2.2.17    |
| 3   | [AppLovin](./mediation_applovin.md)   | Y      | Y    | Y        | 9.9.2       | 6.9.4     |
| 4   | [DFP](./mediation_dfp.md)             | Y      | Y    | Y        | 17.2.1      | 7.52.0    |
| 5   | [Facebook](./mediation_facebook.md)   | Y      | Y    | Y        | 5.6.0       | 5.6.0     |
| 6   | [Maio](./mediation_maio.md)           |        | Y    | Y        | 1.1.10      | 1.4.8     |
| 7   | [MoPub](./mediation_mopub.md)         | Y      | Y    | Y        | 5.8.0       | 5.10.0    |
| 8   | [Nend](./mediation_nend.md)           | Y      | Y    | Y        | 5.1.1       | 5.3.0     |
| 9   | [Tiktok](./mediation_tiktok.md)       | Y      | Y    | Y        | 2.5.2.6     | 2.5.1.2   |
| 10  | [Unity Ads](./mediation_unity_ads.md) | Y      | Y    | Y        | 3.0.0       | 3.3.0     |