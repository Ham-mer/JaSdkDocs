# AppLovin NetworkConfig

## 全体配置
### TXADAppLovinGlobalConfig

```objectivec
@import TaurusXAdMediation_AppLovin;

TXADAppLovinGlobalConfig *appLovinGlobalConfig = [[TXADAppLovinGlobalConfig alloc] init];
// 広告の音はについて、黙認としては on にされます
appLovinGlobalConfig.muted = NO;
```

## ネイティブ
### TXADAppLovinNativeConfig

```objectivec
@import TaurusXAdMediation_AppLovin;

TXADAppLovinNativeConfig *appLovinNativeConfig = [[TXADAppLovinNativeConfig alloc] init];
// 広告の音はについて、黙認としては off にされます。TXADAppLovinNativeConfig はTXADAppLovinGlobalConfigの設置をカバーします
appLovinNativeConfig.muted = YES;
```