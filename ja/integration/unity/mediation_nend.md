# Nend
- [Nend Webサイト](https://nend.net/)
- [Nend 開発者ガイド](https://github.com/fan-ADN/nendSDK-Unity)

## 前提条件
- Android
    - Android API レベル 16 以上
- iOS
    - ターゲットバージョン iOS 8.1 以上

## SDK の導入
AdLime SDK で Nend 広告ネットワークを使用するために、Nend SDK と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
Dependencies.xml に、依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- Nend -->
        <androidPackage spec="com.access_company.adlime:mediation_nend:5.4.2.1">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="net.nend.android:nend-sdk:5.4.2">
            <repositories>
                <repository>http://fan-adn.github.io/nendSDK-Android-lib/library</repository>
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
        
            <!-- Nend -->
            <iosPod name="AdLimeMediation_Nend" version="~> 5.1.1.4">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```

    - 手動でダウンロード

    iOS プロジェクトで、 CocoaPods から SDK が ダウンロードできない場合は、 SDK を直接ダウンロードして解凍し、下記のフレームワークを Assets/Plugins/iOS に入れてください。
    
    [NendAd.embeddedframework](https://github.com/fan-ADN/nendSDK-iOS-pub/releases/download/5.4.0/nendSDK_iOS.zip)<br>
    [AdLimeMediation_Nend.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Nend/5.4.0.1.zip)

### 依存関係の解析
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。

- iOS

    AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

    Xcode上で、プロジェクトファイルを選択し、任意のターゲットの Build Phases > Link Binary With Libraries に以下の フレームワークを追加します。
    - AdSupport.framework
    - Security.framework
    - ImageIO.framework
    - AVFoundation.framework
    - CoreMedia.framework
    - SystemConfiguration.framework
    - WebKit.framework

    以下のフレームワークはオプションです。 広告の詳細情報を取得可能です。
    - CoreLocation.framework
    - CoreMotion.framework
    - CoreTelephony.framework

## 利用可能な広告フォーマット

### 広告フォーマット
|アドネットワーク|バナー |インタースティシャル|動画リワード |
|:-----:|:----:|:----------:|:------:|
|Nend   |Y     | Y          |Y       |

### Bannerサイズ
|ネットワーク |320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート    |
|:-------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Nend     |Y       |Y         |Y        |        |Y       |         |

## 広告枠の設置
AdLime を使って Nend の広告枠を設置する前に、Nend の管理画面上で広告枠を作成し、その広告枠の情報を設定する必要があります。
- Api Key
- Spot ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Nend を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Nend を表示する広告枠で、「広告のソース追加」をクリックし、Nend を追加してください。

**Nend には、ネイティブ広告は二つの種類があります。ネイティブ広告を追加する場合に Native Mode を入力してください**
| Native Mode     | 値 |
|:----------------|:--------|
|Native Ads       |0        |
|Native Video Ads |1        |

**Nendには、インタースティシャル広告は三つの種類があります。インタースティシャル広告を追加する場合に Native Mode を入力してください**
| Interstitial Mode     | 値 |
|:----------------------|:--------|
|Interstitial Ads       |0        |
|Interstitial Video ads |1        |
|Fullscreen Ads         |2        |

## バージョン情報

### リリースバージョン
- Android
    | Nend バージョン     | アダプタ バージョン  |
    |:-----------------|:------------------|
    | 5.4.1            | 5.4.1.1           |
    | 5.1.1            | 5.1.1.4           |

- iOS
    | Nend バージョン     | アダプタ バージョン |
    |:-----------------|:-----------------|
    | 5.3.0            | 5.3.0.0          |
    | 5.1.1            | 5.1.1.4          |

### バージョン履歴
- Android
    | アダプタ バージョン | 日付       | 更新内容                         |
    |-----------------|------------|--------------------------------------|
    | 5.4.1.1         | 2020/2/5    | 5.4.1 に対応|
    | 5.1.1.4         | 2019-7-16  | バナー表示の最適化                  |
    | 5.1.1.2         | 2019-6-29  | バナーのサイズアダブティブを削除   |
    | 5.1.1.1         | 2019-6-21  | Nend SDK 5.1.1 に対応      |

- iOS
    | アダプタ バージョン | 日付       | 更新内容                          |
    |-----------------|------------|---------------------------------------|
    | 5.3.0.0         | 2019-10-14 | Nend SDK 5.3.0 に対応       |
    | 5.1.1.4         | 2019-8-6   | NativeAdLayout インタラクティブエリアのカスタマイズに対応|
    | 5.1.1.2         | 2019-7-6   | クラスが重複する問題を改修          |
    | 5.1.1.1         | 2019-7-2   | インターステーシャル広告イベントの最適化 |
    | 5.1.1.0         | 2019-6-30  | Nend SDK 5.1.1 に対応       |
