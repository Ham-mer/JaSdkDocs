# TikTok Ads
- [TikTok Ads ウェブサイト](https://ad.oceanengine.com/union/media/login/?from=i18n)
- [TikTok Ads 開発者ガイド](https://ad.oceanengine.com/union/media/union/download)

## 前提条件
- Android
    - Android API レベル 14 以上
- iOS
    - ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で TikTok Ads 広告ネットワークを使用するために、TikTok Ads と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
Dependencies.xml に、下記の依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- TikTok -->
        <androidPackage spec="com.access_company.adlime:mediation_toutiao:2.5.3.2.2">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.access_company.adlime:toutiao_open_ad_sdk:2.5.3.2">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="pl.droidsonroids.gif:android-gif-drawable:1.2.6">
            <repositories>
                <repository>https://jcenter.bintray.com/</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.android.support:support-v4:27.1.1">
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
        
            <!-- TikTok -->
            <iosPod name="AdLimeMediation_TikTok" version="~> 2.8.0.1.0">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```

    - 手動でダウンロード

    iOS プロジェクトで、 CocoaPods から SDK が ダウンロードできない場合は、 SDK を直接ダウンロードして解凍し、下記のフレームワークを Assets/AdLime/Plugins/iOS に入れてください。
    
    [BUAdSDK.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/Networks/BUAdSDK/BUAdSDK_2.5.1.2.zip)<br>
    BUAdSDK.bundle<br>
    [AdLimeMediation_TikTok.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_TikTok/2.5.1.2.0.zip)

### 依存関係の設定
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。
    
- iOS

    AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

    Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。

    - StoreKit.framework
    - MobileCoreServices.framework
    - WebKit.framework
    - MediaPlayer.framework
    - CoreMedia.framework
    - AVFoundation.framework
    - CoreTelephony.framework
    - SystemConfiguration.framework
    - AdSupport.framework
    - CoreMotion.framework
    - libresolv.9.tbd
    - libc++.tbd
    - libz.tbd

## 其它设置
- Android

    AndroidManifestの設定
    ```java
    <!-- 追加 -->
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES"/>
    <uses-permission android:name="android.permission.GET_TASKS"/>

    <!-- 追加，同意を貰って位置情報を取得すると、TikTok はこの権限を基づいて精確にターゲットできる告 -->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    ```

    **TikTok SDKは上記の権限を強制取得ではない、取得しなくても広告をリクエストできる。上記の権限を取得してから TikTok はもっと精確にターゲットしてユーザ体験改善してecpmを高める。**

## 利用可能な広告フォーマット

### 広告フォーマット
|アドネットワーク|バナー|インタースティシャル      |動画リワード|
|:-----:|:----:|:----------:|:------:|
|TikTok Ads|Y     | Y          |Y       |

### Bannerサイズ
|アドネットワーク |320×50  |300×250   |320×100  |468×60  |728×90  |スマート  |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|TikTok Ads  |        |Y         |Y        |        |Y       |         |

## 広告枠の配置
AdLime を使って Tiktok の広告枠を配置する前に、 Tiktok の管理画面上で広告枠を作成し、その広告枠の情報を設定する必要があります。
- App ID
- Code ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Tiktok を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Tiktok 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Tiktok を追加してください。
**Tiktok にはインタースティシャルが2種類があります，インタースティシャルを追加する場合に Interstitial Mode を入力してください**
| Interstitial Mode     | 値 | 説明      |
|:----------------------|:--------|:-----------|
|Interstitial           |0        |インタースティシャル       |
|FullScreenVideo        |1        |フルスクリーン動画    |

**Tiktok においてフルスクリーンと動画リワードは縦・横画面があります。設定する場合に、 Orientation を指定してください**
| Orientation     | 値| 説明        |
|:----------------|:--------|:-----------|
|Vertical         |1        |縦        |
|Horizontal       |2        |横       |

## バージョン情報

### リリースバージョン
- Android
    | TikTok Ads バージョン| アダプタ バージョン    |
    |:-----------------|:---------------|
    | 2.5.3.2          | 2.5.3.2.2      |
    | 2.5.2.6          | 2.5.2.6.1      |
    | 2.2.0.2          | 2.2.0.2.1      |
    | 2.0.1.7          | 2.0.1.7.1      |
    | 2.0.1.1          | 2.0.1.1.5      |

- iOS
    | TikTok Ads バージョン| アダプタ バージョン    |
    |:-----------------|:----------------|
    | 2.5.1.2          | 2.5.1.2.0       |
    | 2.4.6.3          | 2.4.6.3.1       |
    | 2.1.0.1          | 2.1.0.1.5       |

### バージョン履歴
- Android
    | アダプタ バージョン | 日付         | 更新内容                   |
    |:-----------------|:------------|:----------------------------------|
    | 2.5.3.2.2       | 2020-1-6    | TikTok SDK 2.5.3.2 に対応|
    | 2.5.2.6.1       | 2019-12-2   | TikTok SDK 2.5.2.6 に対応|
    | 2.2.0.2.1	      | 2019-8-6    | TikTok SDK 2.2.0.2 に対応        |
    | 2.0.1.7.1	      | 2019-7-16   | TikTok SDK 2.0.1.7 に対応        |
    | 2.0.1.1.5       | 2019-6-13   | DrawFeedList イベントの最適化      |
 

- iOS
    | アダプタ バージョン | 日付       | 更新内容                   |
    |-----------------|------------|----------------------------------|
    | 2.5.1.2.0       | 2019-10-14 | TikTok Ads SDK 2.5.1.2 に対応|
    | 2.4.6.3.1       | 2019-10-14 | TikTok Ads SDK 2.4.6.3 に対応|
    | 2.1.0.1.5       | 2019-8-6   | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
    | 2.1.0.1.2       | 2019-7-15  | 動画リワード広告のイベント最適化             |
    | 2.1.0.1.1       | 2019-7-8   | 動画リワード広告の初期化できない問題に対応 |
    | 2.1.0.1.0       | 2019-7-5   | TikTok Ads SDK 2.1.0.1 に対応|
