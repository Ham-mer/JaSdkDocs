# Unity Ads
- [Unity Ads Webサイト](https://operate.dashboard.unity3d.com)
- [Unity Ads 開発者ガイド](https://unityads.unity3d.com/help/unity/integration-guide-unity)

## 前提条件
- Android
    - Android API レベル 14 以上
- iOS
    - ターゲットバージョン iOS 8.1 以上

## SDKの導入
AdLime SDK で Unity 広告を使用するためには、 Unity Ads SDK と、それに対応した AdLime SDK アダプタを導入してください。

### 依存関係の追加
Dependencies.xml に、下記の依存関係を追加してください。
- Android
```csharp
<dependencies>

    <!-- Android -->
    <androidPackages>

        <!-- Unity Ads -->
        <androidPackage spec="com.access_company.adlime:mediation_unity:3.1.0.2">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>
        <androidPackage spec="com.access_company.adlime:unity-ads:3.1.0">
            <repositories>
                <repository>https://dl.bintray.com/adlime/AdLime</repository>
            </repositories>
        </androidPackage>

    </androidPackages>
</dependencies>
```

- iOS
    - Dependencies.xml を設定（推奨）
    ```csharp
    <dependencies>

        <!-- iOS -->
        <iosPods>
        
            <!-- Unity Ads -->
            <iosPod name="AdLimeMediation_UnityAds" version="~> 3.3.0.0">
                <sources>
                    <source>https://github.com/CocoaPods/Specs</source>
                </sources>
            </iosPod>
        </iosPods>

    </dependencies>
    ```

    - 手動でダウンロード

    iOS プロジェクトで、 CocoaPods から SDK が ダウンロードできない場合は、 SDK を直接ダウンロードして解凍し、下記のフレームワークを Assets/Plugins/iOS に入れてください。
    
    [UnityAds.framework](https://github.com/Unity-Technologies/unity-ads-ios/releases/download/3.3.0/UnityAds.framework.zip)<br>
    [AdLimeMediation_UnityAds.framework](https://github.com/Ham-mer/AdLime-iOS-Pub/raw/master/DownloadZip/AdLimeMediation_UnityAds/3.3.0.1.zip)

### 依存関係の設定
- Android

    Unity エディタで、[Assets] > [Play Services Resolver] > [Android Resolver] > [Resolve] を選択します。Unity Play Services Resolver ライブラリにより、存関係が Unity アプリの Assets/Plugins/Android ディレクトリにコピーされます。

- iOS

    AdLime SDK を Unity に取り込むための手順はこれ以上ありません。iOS の SDK の依存関係は CocoPods によって管理します。CocoPods はビルドプロセスの最後に行われます。

## 利用可能な広告フォーマット

### 広告フォーマット
|ネットワーク |バナー |インタースティシャル |動画リワード |
|:--------:|:----:|:----------:|:------:|
|Unity Ads |Y     | Y          |Y       |

### バナーサイズ
|アドネットワーク|320 × 50  |300 × 250   |320 × 100  |468 × 60  |728 × 90  |スマート |
|:--------:|:------:|:--------:|:-------:|:------:|:------:|:-------:|
|Unity Ads |Y       |          |         |        |        |         |

## 広告枠の配置
AdLime を使って Unity Ads の広告枠を設置する前に、 Unity Ads の管理画面上で広告枠を作成し、その広告枠の情報を設定する必要があります。
- Game ID
- Placement ID

AdLime の管理画面を開き、左側の「ネットワーク」メニューをクリックして、 Unity Ads を有効にしてください。

最後に、左側の「アプリ」メニューをクリックし、Unity Ads を表示する広告枠で、「広告のソース追加」をクリックし、 Unity Ads を追加してください。

## バージョン情報

### リリースバージョン
- Android
    | Unity Ads バージョン   | アダプタ バージョン |
    |:-----------------|:---------------|
    |3.1.0             |3.1.0.0         |
    |3.0.0             |3.0.0.1         |

- iOS
    | Unity Ads バージョン| アダプタ バージョン |
    |:-----------------|:----------------|
    |3.3.0             |3.3.0.0          |
    |3.1.0             |3.1.0.1          |

### バージョン履歴
- Android
    | アダプタ バージョン | 日付       | 更新内容                    |
    |-----------------|------------|----------------------------------|
    | 3.1.0.0         | 2019-7-19  | Unity Ads SDK 3.1.0 に対応|
    | 3.0.0.1         | 2019-2-14  | Unity Ads に対応|

- iOS
    | アダプタ バージョン | 日付       | 更新内容                    |
    |-----------------|------------|----------------------------------|
    | 3.3.0.0         | 2019-10-14 | Unity Ads SDK 3.3.0 に対応|
    | 3.1.0.2         | 2019-8-4   | 不要なヘッダーファイルの削除|
    | 3.1.0.1         | 2019-7-15  | 動画リワード広告のイベント最適化|
    | 3.1.0.0         | 2019-6-30  | Unity Ads SDK 3.1.0 に対応|
