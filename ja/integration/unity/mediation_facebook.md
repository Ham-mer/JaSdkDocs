# Facebook ドキュメント
- [Facebook ウェブサイト](https://business.facebook.com/pub/home)
- [Facebook 開発者ガイド](https://developers.facebook.com/docs/audience-network/unity)

## 前提条件
- Android
    - Android API レベル 14 以上
- iOS
    - ターゲットバージョン iOS 9.0 以上

## SDKの導入
AdLime SDK で Facebook Audience Network を使用するために、 Facebook Audience Network SDK と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
 Dependencies.xml に、下記の依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- Facebook -->
        <androidPackage spec="com.access_company.adlime:mediation_facebook:5.6.0.3.alpha">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.facebook.android:audience-network-sdk:5.6.0">
            <repositories>
                <repository>https://maven.google.com/</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.android.support:support-annotations:28.0.0">
            <repositories>
                <repository>https://maven.google.com/</repository>
            </repositories>
        </androidPackage>

    </androidPackages>
</dependencies>
```

- iOS
    - Dependencies.xml の設置（推奨）
    ```csharp
    <dependencies>

        <!-- iOS -->
        <iosPods>
        
            <!-- DFP -->
            <iosPod name="AdLimeMediation_Facebook" version="~> 5.6.0.0">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```
    - 手動でダウンロード

    SDK を 直接ダウンロードして解凍し、下記のフレームワークを Assets/Plugins/iOS に入れてください。
    
    [FBAudienceNetwork.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/FBAudienceNetwork/FBAudienceNetwork_5.6.0.zip)<br>
    [AdLimeMediation_Facebook.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Facebook/5.6.0.2.zip)

### 依存関係の設定
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、依存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。

- iOS

    AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

## 利用できる広告フォーマット

### 広告フォーマット
|ネットワーク|バナー   |インタースティシャル         |動画リワード |
|:-----:|:----:|:----------:|:------:|
|Facebook  |Y     | Y          |Y       |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Facebook    |Y       |Y         |Y        |        |        |         |

## 広告枠の設置
AdLime を使って Facebook Audience Network の広告枠を配置する前に、Facebook Audience Network の管理画面上で広告枠を作成し、その広告枠の情報を設定する必要があります。
- Placement ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Facebook を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Facebook Audience Network 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Facebook Audience Network 広告を追加してください。

## バージョン情報

### リリースバージョン
- Android
    | Facebook バージョン | アダプタ バージョン|
    |:-----------------|:----------------|
    | 5.6.0             | 5.6.0.0 / 5.6.0.3.alpha |
    | 5.5.0             | 5.5.0.1        |
    | 5.4.1             | 5.4.1.1        |
    | 5.1.0             | 5.1.0.2        |

- iOS
    | Facebook バージョン | アダプタ バージョン    |
    |:-----------------|:----------------|
    |5.6.0             |5.6.0.0          |
    |5.5.1             |5.5.1.0          |
    |5.4.0             |5.4.0.4          |

### 更新履歴
- Android
    | アダプタ バージョン| 日付        | 更新内容                             |
    |-----------------|------------|----------------------------------|
    | 5.6.0.3.alpha   | 2019-11-26 | HeaderBidding をサポートする|
    | 5.6.0.0         | 2019-11-13 | Facebook Audience Network SDK 5.6.0 に対応|
    | 5.5.0.1         | 2019-10-3  | Facebook Audience Network SDK 5.5.0 に対応|
    | 5.4.1.1         | 2019-7-16  |動画リワード広告のクリックイベントが通知されない問題を修正             |
    | 5.1.0.2         | 2019-4-25  |android:networkSecurityConfig 設定の改善|

- iOS
    | アダプタ バージョン| 日付        | 更新内容                             |
    |-----------------|------------|----------------------------------|
    | 5.6.0.0         | 2019-11-7  | Facebook Audience Network SDK 5.6.0 に対応|
    | 5.5.1.0         | 2019-10-14 | Facebook Audience Network SDK 5.5.1 に対応|
    | 5.4.0.4         | 2019-8-6   | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
    | 5.4.0.2         | 2019-7-15  | 動画リワード広告のイベント最適化             |
    | 5.4.0.1         | 2019-7-9   | ネイティブ広告のクリックイベントの改善        |
    | 5.4.0.0         | 2019-6-30  | Facebook Audience Network SDK 5.4.0 に対応|
