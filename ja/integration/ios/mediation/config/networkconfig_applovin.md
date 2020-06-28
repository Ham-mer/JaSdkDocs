# AppLovin NetworkConfig

## 全体配置
### AdLimeAppLovinGlobalConfig

```objectivec
@import AdLimeMediation_AppLovin;

AdLimeAppLovinGlobalConfig *appLovinGlobalConfig = [[AdLimeAppLovinGlobalConfig alloc] init];
// 広告の音はについて、黙認としては on にされます
appLovinGlobalConfig.muted = NO;
```

## ネイティブ
### AdLimeAppLovinNativeConfig

```objectivec
@import AdLimeMediation_AppLovin;

AdLimeAppLovinNativeConfig *appLovinNativeConfig = [[AdLimeAppLovinNativeConfig alloc] init];
// 広告の音はについて、黙認としては off にされます。AdLimeAppLovinNativeConfig はAdLimeAppLovinGlobalConfigの設置をカバーします
appLovinNativeConfig.muted = YES;
```