# AdMob NetworkConfig

## 全体配置
### AdMobGlobalConfig
全体のテスト設備のIDを設置。

テスト設置で取れるのはテスト広告です。"Ads"を"Log Tag"で設備のTestDeviceIdを確認出来ます。，例：
```
I/Ads: Use AdRequest.Builder.addTestDevice("Your Test Device Id") to get test ads on this device.
```

```java
AdMobGlobalConfig.Builder()
                // Idテスト設備IDの追加
                .addTestDevice("Your Test Device Id 1")
                .addTestDevice("Your Test Device Id 2")
                .build();
```

## バナー広告
### AdMobBannerConfig
Adaptive Bannerのサイズについて黙認としては画面の幅とマッチされる高さです。下記の方法でサイズを調整できます。

```java
// 画面の横縦でサイズを設定します。
AdMobBannerConfig.Builder()
                // .setAdaptiveBannerSize(AdSize.getCurrentOrientationAnchoredAdaptiveBannerAdSize(BannerActivity.this, 320))
                .build();
```

```java
// また、プリロードの場合に、希望する画面の横縦を指定できます。
AdMobBannerConfig.Builder()
                // .setAdaptiveBannerSize(AdSize.getPortraitAnchoredAdaptiveBannerAdSize(BannerActivity.this, 320))
                // .setAdaptiveBannerSize(AdSize.getLandscapeAnchoredAdaptiveBannerAdSize(BannerActivity.this, 320))
                .build();
```