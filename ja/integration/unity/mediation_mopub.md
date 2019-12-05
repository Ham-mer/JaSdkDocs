# MoPub
- [MoPub Webサイト](https://app.mopub.com/apps)
- [MoPub 開発者ガイド](https://developers.mopub.com/publishers/unity/get-started/)

## 前提条件
- Android
    - Android API レベル 16 以上
- iOS
    - ターゲットバージョン iOS 9.0 以上

## SDKの導入
AdLime SDK で MoPub を使用するために、 MoPub SDK と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
Dependencies.xml に、下記の依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- MoPub -->
        <androidPackage spec="com.access_company.adlime:mediation_mopub:5.8.0.1">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.mopub:mopub-sdk:5.8.0">
            <repositories>
                <repository>https://jcenter.bintray.com/</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.google.android.gms:play-services-basement:16.1.0">
            <repositories>
                <repository>https://maven.google.com/</repository>
            </repositories>
        </androidPackage>

    </androidPackages>
</dependencies>
```

- iOS
    - Dependencies.xml を設定する（推奨）
    ```csharp
    <dependencies>

        <!-- iOS -->
        <iosPods>
        
            <!-- MoPub -->
            <iosPod name="AdLimeMediation_MoPub" version="~> 5.10.0.1">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```

    - 手動でダウンロード
    
    iOS プロジェクトで、 CocoaPods から SDK が ダウンロードできない場合は、 SDK を直接ダウンロードして解凍し、下記のフレームワークを Assets/Plugins/iOS に入れてください。
    
    [MoPubSDKFramework.framework](https://github.com/mopub/mopub-ios-sdk/releases/download/5.9.0/mopub-framework-5.10.0.zip)<br>
    [AdLimeMediation_MoPub.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_MoPub/5.10.0.1.zip)

    MoPub SDKをダウンロードした後、mopub-framework-5.10.0/MoPubSDKFramework/universal にフレームワークファイルがあります。

### 依存関係の解析
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。

    Edit build.gradle file, add below setting:
    ```
    android {
        ...

        compileOptions {
            sourceCompatibility JavaVersion.VERSION_1_8
            targetCompatibility JavaVersion.VERSION_1_8
        }
        
        ...
    }
    ```

- iOS

    AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

    Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の MoPub フレームワークを追加します。

    - AdSupport.framework
    - AVFoundation.framework
    - CoreGraphics.framework
    - CoreLocation.framework
    - CoreMedia.framework
    - CoreTelephony.framework
    - Foundation.framework
    - MediaPlayer.framework
    - MessageUI.framework
    - QuartzCore.framework
    - SafariServices.framework
    - StoreKit.framework
    - SystemConfiguration.framework
    - UIKit.framework
    - WebKit.framework

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク|バナー  |インタースティシャル        |動画リワード|
|:-----:|:----:|:----------:|:------:|
|MoPub  |Y     | Y          |Y       |

### バナーサイズ
|ネットワーク  |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|MoPub    |Y       |Y         |         |        |Y       |         |

## 広告枠の設置
AdLime を使って Mobup の広告枠を配置する前に、 Mobup の管理画面上で広告枠を作成し、その広告枠の情報を設定する必要があります。
- AdUnit ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Mobup を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Mobup 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Mobup 広告を追加してください。

## バージョン情報

### リリースバージョン
- Android
    | MoPub バージョン  | アダプタ バージョン|
    |:---------------|:----------------|
    | 5.8.0          | 5.8.0.1         |
    | 5.7.1          | 5.7.1.0         |
    | 5.5.0          | 5.5.0.2         |
    | 5.4.1          | 5.4.1.2         |

- iOS
    | MoPub バージョン  | アダプタ バージョン |
    |:---------------|:----------------|
    | 5.10.0         | 5.10.0.1         |
    | 5.9.0          | 5.9.0.0         |
    | 5.6.0          | 5.6.0.3         |

### バージョン履歴
- Android
    | バージョン        | 日付       | 更新内容                     |
    |-----------------|------------|----------------------------------|
    | 5.8.0.1         | 2019-11-24 | 動画リワードコールバックされると失効の問題解決 |
    | 5.8.0.0         | 2019-11-5  | MoPub SDK 5.8.0 に対応 |
    | 5.7.1.0         | 2019-7-19  | MoPub SDK 5.7.1 に対応|
    | 5.5.0.2         | 2019-7-16  | 動画リワード広告のイベント改善|
    | 5.5.0.1         | 2019-6-27  | Mopub のコンテキストに対応|

- iOS
    | バージョン        | 日付       | 更新内容                    |
    |-----------------|------------|----------------------------------|
    | 5.10.0.1        | 2019-11-19 | MoPub SDK 5.10.0 バナー に対応 |
    | 5.10.0.0        | 2019-10-14 | MoPub SDK 5.10.0 に対応 |
    | 5.9.0.0         | 2019-10-14 | MoPub SDK 5.9.0 に対応 |
    | 5.6.0.3         | 2019-8-6   | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
    | 5.6.0.1         | 2019-7-15  | 動画リワード広告のイベント最適化    |
    | 5.6.0.0         | 2019-6-30  | MoPub SDK 5.6.0 に対応 |
