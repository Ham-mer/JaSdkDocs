# DFP NetworkConfig

## バナー広告
### AdLimeDFPBannerConfig
 Adaptive Bannerのサイズについて黙認としては画面の幅とマッチされる高さです。下記の方法でサイズを調整できます。

```objectivec
@import AdLimeMediation_GoogleAds;

// 画面の横縦でサイズを設定します。。
AdLimeDFPBannerConfig *config = [[AdLimeDFPBannerConfig alloc] init];
// config.adaptiveBannerAdSize = GADCurrentOrientationAnchoredAdaptiveBannerAdSizeWithWidth(320);
```

```objectivec
@import AdLimeMediation_GoogleAds;

// また、プリロードの場合に、希望する画面の横縦を指定できます。
AdLimeDFPBannerConfig *config = [[AdLimeDFPBannerConfig alloc] init];
// config.adaptiveBannerAdSize = GADPortraitAnchoredAdaptiveBannerAdSizeWithWidth(320);
// config.adaptiveBannerAdSize = GADLandscapeAnchoredAdaptiveBannerAdSizeWithWidth(320);
```