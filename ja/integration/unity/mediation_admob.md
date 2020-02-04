# AdMob ドキュメント
- [AdMob Webサイト](https://developers.google.com/admob/)
- [AdMob 開発者ガイド](https://developers.google.com/admob/unity/start)

## 前提条件
- Android
    - Android API レベル 14 以上
- iOS
    - ターゲットバージョンを iOS 8.0 以上に設定していること

## SDKの導入
AdLime SDK で AdMoB 広告ネットワークを使うために、AdMob SDK と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
Dependencies.xml に、下記の依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- AdMob -->
        <androidPackage spec="com.access_company.adlime:mediation_admob:15.0.1.10">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.google.android.gms:play-services-ads:15.0.1">
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
        
            <!-- AdMob -->
            <iosPod name="AdLimeMediation_GoogleAds" version="~> 7.52.0.2">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```

    - 手動ダウンロード

    iOS プロジェクトで、 CocoaPods から SDK が ダウンロードできない場合は、 SDK を直接ダウンロードして解凍し、フレームワークを Xcode プロジェクトにインポートしてください。また、下記のフレームワークを Assets/Plugins/iOS に入れてください。
    
    [Google-Mobile-Ads-SDK.framework](https://developers.google.cn/admob/ios/download)<br>
    GoogleAppMeasurement.framework<br>
    GoogleUtilities.framework<br>
    nanopb.framework<br>
    [AdLimeMediation_GoogleAds.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_GoogleAds/7.52.0.2.zip)

### 依存関係の設定
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、依存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。

- iOS

    AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

##  AdMob App ID の設置
- Android

   下記の `<meta-data>` に、AdMob の アプリ ID を AndroidManifest.xml に追加します。 AdMoB の管理画面で アプリ ID を確認します。
    ```java
    <manifest>
        <application>
            <meta-data
                android:name="com.google.android.gms.ads.APPLICATION_ID"
                android:value="ADMOB_APP_ID"/>
        </application>
    </manifest>
    ```
    **Google Mobile Ads SDK 7.42.0 以降のバージョンにおいて、このプロシージャを実行する必要があります。 `<meta-data>` がない場合、アプリがクラッシュする可能性があります。その際、下記のメッセージが表示されます："The Google Mobile Ads SDK was initialized incorrectly."**
- iOS

    Info.plist ファイルに、 GADApplicationIdentifier キーと、 AdMob の管理画面で登録したアプリの ID を追加してください。

    Info.plist を ソースコードとして開いて編集します。
    ```objectivec
    <key>GADApplicationIdentifier</key>
    <string>Your AdMob APP_ID</string>
    ```

    もしくは、プロパティリストエディタ で編集できます。

    <img src="./../images/ios/mediation_admob_app_id_plist.png" height="80"/>

    **Google Mobile Ads SDK 7.42.0 以降のバージョンにおいて、このプロシージャを実行する必要があります。 Info.plist ファイルに GADApplicationIdentifier キーがない場合、アプリがクラッシュする可能性があります。その際、下記のメッセージが表示されます："The Google Mobile Ads SDK was initialized incorrectly."**

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー   |インタラクション         |動画リワード |
|:-----:|:----:|:----------:|:------:|
|AdMob  |Y     | Y          |Y       |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|AdMob    |Y       |Y         |Y        |Y       |Y       |Y        |

## 広告枠の設置
AdLime を使って Admob の広告枠を設置する前に、AdMob の管理画面上で広告枠を作成し、その広告枠の情報を設定する必要があります。

- App ID  
- AdUnit ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、AdMob を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、AdMob を表示する広告枠で、「広告のソース追加」をクリックし、AdMob を追加してください。

## バージョン情報

### リリースバージョン
- Android
    | AdMob バージョン   | アダプタ バージョン |
    |:-----------------|:-----------------|
    |17.2.1            |17.2.1.6          |
    |17.1.2            |17.1.2.12         |
    |15.0.1            |15.0.1.10         |

- iOS
    | AdMob バージョン   | アダプタ バージョン|
    |:-----------------|:----------------|
    |7.52.0            |7.52.0.2         |
    |7.50.0            |7.50.0.0         |
    |7.42.2            |7.42.2.6         |

### 更新履歴
- Android
    | アダプタ バージョン| 日付       | 更新内容                              |
    |-----------------|------------|----------------------------------|
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
    | アダプタ バージョン| 日付       | 更新内容                              |
    |-----------------|------------|----------------------------------|
    |7.52.0.2         |2020/2/3    |画面が縦から横になると、広告のサイズは自動調整できない問題を解決します  |
    |7.52.0.0         |2019-11-7   |AdMob SDK 7.52.0 に対応 |
    |7.50.0.0         |2019-10-14  |AdMob SDK 7.50.0 に対応 |
    |7.42.2.6         |2019-8-4    |NativeAdLayout インタラクティブエリアのカスタマイズに対応 |
    |7.42.2.1         |2019-7-4    |広告イベントの最適化 |
    |7.42.2.0         |2019-6-30   |AdMob SDK 7.42.2 に対応 |
