# Amazon
- [Amazon Webサイト](https://developer.amazon.com/zh/)
- [Amazon 開発者ガイド](https://developer.amazon.com/zh/mobile-ads)

## 前提条件
- Android
    - Android API レベル 14 以上
- iOS
    - ターゲットバージョン iOS 10.0 以上

## SDK の導入
AdLime SDK で Amazon 広告ネットワークを使用するために、Amazon SDK と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
 Dependencies.xml に、依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- Amazon -->
        <androidPackage spec="com.access_company.adlime:mediation_amazon:5.9.0.3">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.google.android.gms:play-services-ads:17.2.1">
            <repositories>
                <repository>https://maven.google.com/</repository>
            </repositories>
        </androidPackage>

    </androidPackages>
</dependencies>
```

- iOS
    - Dependencies.xml を設定（推奨）
    ```csharp
    <dependencies>

        <!-- iOS -->
        <iosPods>
        
            <!-- Amazon -->
            <iosPod name="AdLimeMediation_Amazon" version="~> 2.2.17.1">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```

    - 手動ダウンロード

    iOS プロジェクトで、 CocoaPods から SDK が ダウンロードできない場合は、 SDK を直接ダウンロードして解凍し、下記のフレームワークを Assets/Plugins/iOS に入れてください。
    
    [AmazonAd.framework](https://app-craft-internal.ams3.digitaloceanspaces.com/Frameworks/AmazonAdSDK/AmazonMobileAds-iOS-v2.2.17.0.zip)<br>
    [AdLimeMediation_Amazon.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Amazon/2.2.17.3.zip)

### 依存関係の設定
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。

- iOS

    AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク |バナー |インタースティシャル |動画リワード |
|:-----:|:----:|:----------:|:------:|
|Amazon |Y     | Y          |        |

### バナーサイズ
|ネットワーク  |320×50  |300×250   |320×100  |468×60  |728×90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Amazon   |Y       |Y         |         |        |Y       | Y       |

## 広告枠の設置
AdLimeのページにてAmazonの広告枠を配置するためには、まずAmazonのページにおいて広告枠を作成して、下記の情報を獲得する必要があります：  
- Application Key

AdLimeのページを開き、左側の「ネットワーク」メニューをクリックして、Amazonをオンにしてください。

最後に、左側の「アプリ」メニューをクリックし、アプリの中からAmazon広告を追加する必要のある広告枠を見つけて、右上の「広告のソース追加」をクリックし、AdMob広告を追加してください。

## バージョン情報

### リリースバージョン
- Android
    | Amazon バージョン  | アダプタ バージョン |
    |:-----------------|:-----------------|
    | 5.9.0            | 5.9.0.2          |

- iOS
    | Amazon バージョン  | アダプタ バージョン |
    |:-----------------|:-----------------|
    | 2.2.17           | 2.2.17.1         |

### バージョン履歴
- Android
    | アダプタ バージョン | 日付        | 更新内容                             |
    |------------------|------------|----------------------------------|
    | 5.9.0.2          | 2019-7-18  | バナーサイズ 728×90 のサポート|
    | 5.9.0.1          | 2019-3-5   | 広告の読み込みが失敗する場合、コールバックされないバグ修正|

- iOS
    | アダプタ バージョン | 日付        | 更新内容                             |
    |------------------|------------|----------------------------------|
    | 2.2.17.1         | 2019-8-3   | 不要なヘッダーファイルの削除|
    | 2.2.17.0         | 2019-6-30  | Amazon SDK 2.2.17 に対応|
