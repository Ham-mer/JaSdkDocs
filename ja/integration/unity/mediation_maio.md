# Maio
- [Maio Webサイト](https://maio.jp/)
- [Maio 開発者ガイド](https://github.com/imobile-maio/maio-Unity-Plugin)

## 前提条件
- Android
    - Android API レベル 16 以上
- iOS
    - ターゲットバージョン iOS 8.0 以上

## SDK の導入
AdLime SDK で Maio を使用するためには、 Maio SDK と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
Dependencies.xml に、下記の依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- Maio -->
        <androidPackage spec="com.access_company.adlime:mediation_maio:1.1.10.0">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.maio:android-sdk:1.1.10@aar">
            <repositories>
                <repository>https://imobile-maio.github.io/maven</repository>
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

- iOS
    - Dependencies.xml の設置（推奨）
    ```csharp
    <dependencies>

        <!-- iOS -->
        <iosPods>
        
            <!-- Maio -->
            <iosPod name="AdLimeMediation_Maio" version="~> 1.4.8.0">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```

    - 手動でダウンロード

    iOS プロジェクトで、 CocoaPods から SDK が ダウンロードできない場合は、 SDK を直接ダウンロードして解凍し、フレームワークを Assets/Plugins/iOS に入れてください。
    
    [Maio.framework](https://github.com/imobile-maio/maio-iOS-SDK/releases/download/v1.4.8/Maio.framework.zip)<br>
    [AdLimeMediation_Maio.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_Maio/1.4.8.1.zip)

### 依存関係の設定
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。

- iOS

    AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

## 利用可能な広告フォーマット

### 広告フォーマット
|アドネットワーク|バナー|インタースティシャル|動画リワード |
|:-----:|:----:|:----------:|:------:|
|Maio   |      | Y          |Y       |

## 広告枠の配置
AdLime を使って Maio の広告枠を設置する前に、 Maio の管理画面上で広告枠を作成し、その広告枠の情報を設定する必要があります。
- Media ID
- Zone ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Maio を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、 Maio 広告を表示する広告枠で、「広告のソース追加」をクリックし、 Maio 広告を追加してください。

## バージョン情報

### リリースバージョン
- Android
    | Maioバージョン  | Adapterバージョン|
    |:--------------|:----------------|
    | 1.1.10        | 1.1.10.0        |
    | 1.1.9         | 1.1.9.0         |
    | 1.1.8         | 1.1.8.1         |

- iOS
    | Maioバージョン     | Adapterバージョン |
    |:-----------------|:----------------|
    | 1.4.8            | 1.4.8.0         |
    | 1.4.6            | 1.4.6.2         |

### バージョン履歴
- Android
    | Adapterバージョン | 日付       | 更新内容                    |
    |-----------------|------------|----------------------------------|
    | 1.1.10.0        | 2019-11-4  | Maio SDK 1.1.10 に対応     | 
    | 1.1.9.0         | 2019-7-18  | Maio SDK 1.1.9 に対応|
    | 1.1.8.1         | 2019-6-28  | 動画リワードの追加|

- iOS
    | Adapterバージョン | 日付       | 更新内容                    |
    |-----------------|------------|----------------------------------|
    | 1.4.8.0         | 2019-10-14  | Maio SDK 1.4.8 に対応   |
    | 1.4.6.2         | 2019-8-6   | 不要なヘッダーファイルの削除|
    | 1.4.6.1         | 2019-7-15  | 動画リワード広告のイベント最適化             |
    | 1.4.6.0         | 2019-6-30  | Maio SDK 1.4.6 に対応   |
