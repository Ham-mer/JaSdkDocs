# DFP ドキュメント
- [DFP Webサイト](https://developers.google.com/ad-manager/)
- [DFP 開発者ガイド](https://developers.google.com/ad-manager/mobile-ads-sdk/)

## 前提条件
- Android
    - Android API レベル 14 以上
- iOS
    - ターゲットバージョン iOS 8.0 以上

## SDKの導入
AdLime SDK で DFP を使うために、AdMob SDK と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
Dependencies.xml に、下記の依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- DFP -->
        <androidPackage spec="com.access_company.adlime:mediation_admob:19.1.0.0">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.google.android.gms:play-services-ads:19.1.0">
            <repositories>
                <repository>https://maven.google.com/</repository>
            </repositories>
        </androidPackage>

    </androidPackages>
</dependencies>
```

- iOS
    - Dependencies.xml の設置（推奨）
    ```csharp
    <dependencies>

        <!-- iOS -->
        <iosPods>
        
            <!-- DFP -->
            <iosPod name="AdLimeMediation_GoogleAds" version="~> 7.55.0.1">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```

    - 手動ダウンロード

    iOS プロジェクトで、 CocoaPods から SDK が ダウンロードできない場合は、 SDK を直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。また、下記のフレームワークを Assets/Plugins/iOS に入れてください。
    
    [Google-Mobile-Ads-SDK.framework](https://developers.google.com/ad-manager/mobile-ads-sdk/ios/download)<br>
    GoogleAppMeasurement.framework<br>
    GoogleUtilities.framework<br>
    nanopb.framework<br>
    [AdLimeMediation_GoogleAds.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_GoogleAds/7.64.0.0.zip)

### 依存関係の設定
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、依存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。

- iOS

   AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

## DFP GADIsAdManagerApp の設定
- Android

    SDKは導入済みなので、設定の必要はありません。

- iOS

    アプリのInfo.plistファイルにおいて，ブール値はYESのGADApplicationIdentifierキーを追加してください。そうするとあなたのアプリはAd Managerアプリであることを声明することができます。プログラミングで上記の操作を行うことができます：

    ```objectivec
    <key>GADIsAdManagerApp</key>
    <true/>
    ```

    プロパティリストエディタにてそれを変更することもできます：

    <img src="./../images/ios/mediation_dfp_app_id_plist.png" height="80"/>

    **Google Mobile Ads SDK 7.42.0 以降のバージョンにおいて、このプロシージャを実行する必要があります。 Info.plist ファイルに GADApplicationIdentifier キーがない場合、アプリがクラッシュする可能性があります。その際、下記のメッセージが表示されます："The Google Mobile Ads SDK was initialized incorrectly."**

## 利用可能なフォーマット

### 広告フォーマット
|ネットワーク|バナー   |インタースティシャル         |動画リワード |
|:-----:|:----:|:----------:|:------:|
|DFP    |Y     | Y          |Y       |

### バナーサイズ
|ネットワーク  |320×50  |300×250   |320×100  |468×60  |728×90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|DFP      |Y       |Y         |Y        |Y       |Y       |Y        |

## 広告枠の配置
AdLime を使って DFP の広告枠を配置する前に、DFP の管理画面上で広告枠を作成し、その広告枠の情報を設定する必要があります。
- App ID  
- AdUnit ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 DFP を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 DFP 広告を表示する広告枠で、「広告のソース追加」をクリックし、 DFP 広告を追加してください。

## バージョン情報

### リリースバージョン
- Android
    | DFP バージョン     | アダプター バージョン|
    |:-----------------|:------------------|
    |18.3.0            |18.3.0.0           |
    |17.2.1            |17.2.1.6           |
    |17.1.2            |17.1.2.12          |
    |15.0.1            |15.0.1.10          |

- iOS
    | DFP バージョン     | アダプター バージョン|
    |7.55.0            |7.55.0.1         |
    |7.52.0            |7.52.0.2         |
    |7.50.0            |7.50.0.0         |
    |7.42.2            |7.42.2.6         |

### バージョン履歴
- Android
    | アダプター バージョン| 日付       | 内容                              |
    |------------------|------------|----------------------------------|
    | 18.3.0.0   | 2020/2/7   |AdMob SDK 18.3.0 に対応，AndroidXに移します。|
    | 17.2.1.6   | 2019-11-26 |内部ロジックを改善|
    | 17.2.1.5   | 2019-10-31 |ネイティブ広告とフィードリスト広告では、InteractiveAreは設置される場合にMediaViewLayoutを追加されないと画像が展示されないという問題を解決する|
    | 17.2.1.2   | 2019-10-2  |ネイティブ広告はクリックエリアのカスタムをサポート|
    | 17.2.1.0   | 2019-7-18  |AdMob SDK 17.2.1 に対応。複数のリワード広告の読み込みに対応|
    | 17.1.2.12  | 2019-11-26 |内部ロジックを改善|
    | 17.1.2.11  | 2019-10-31 |ネイティブ広告とフィードリスト広告では、InteractiveAreは設置される場合にMediaViewLayoutを追加されないと画像が展示されないという問題を解決する|
    | 17.1.2.7   | 2019-7-16  |動画リワード広告のクリックイベントが通知されない問題を修正|
    | 17.1.2.4   | 2019-6-12  |ネイティブ広告のクリックイベントの改善|
    | 15.0.1.10  | 2019-11-26 |内部ロジックを改善|
    | 15.0.1.9   | 2019-10-31 |ネイティブ広告とフィードリスト広告では、InteractiveAreは設置される場合にMediaViewLayoutを追加されないと画像が展示されないという問題を解決する|

- iOS
    | アダプター バージョン| 日付      | 内容                              |
    |-----------------|------------|----------------------------------|
    |7.55.0.1         |2020/2/14   |- AdMob SDK 7.55.0 に対応<br>- 新たな動画リワードAPIでパラレロードをサポートします |
    |7.52.0.2         |2020/2/3    |画面が縦から横になると、広告のサイズは自動調整できない問題を解決します  |
    |7.52.0.0         |2019-11-7   |AdMob SDK 7.52.0 に対応 |
    |7.50.0.0         |2019-10-14  |DFP SDK 7.50.0 に対応 |
    |7.42.2.6         |2019-8-4    |NativeAdLayout インタラクティブエリアのカスタマイズに対応|
    |7.42.2.1         |2019-7-4    |広告イベントの最適化 |
    |7.42.2.0         |2019-6-30   |DFP SDK 7.42.2 に対応|
