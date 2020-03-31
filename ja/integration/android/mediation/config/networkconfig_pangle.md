# Pangle NetworkConfig

## Global Config
### TikTokGlobalConfig

```java
TikTokGlobalConfig.Builder()
                // Set whether user is a paid user
                .setIsPaid(false)
                // Set the keyword list for user portraits, it cannot exceed 1000 characters
                // .setKeywords("")
                // Set additional user information, cannot exceed 1000 characters
                // .setData("")
                // Set the landing page theme, default it TTAdConstant.TITLE_BAR_THEME_LIGHT
                .setTitleBarTheme(TTAdConstant.TITLE_BAR_THEME_LIGHT)
                // Set whether to allow SDK to pop up notifications
                .setAllowShowNotify(true)
                // Set whether to allow the landing page to appear on the lock screen
                .setAllowShowPageWhenScreenLock(true)
                // Set whether to support multiple processes
                .setSupportMultiProcess(false)
                // You can set the privacy information control switch, please see the "TTCustomController description" below
                .setCustomController(new TTCustomController() {})
                // Indicate whether user a child or an adult, 0: adult, 1: child
                // .coppa(0);
                .build();
```

**Multi-process description**

If your application needs to support multiple processes, be sure to set TTAdConfig.supportMultiProcess(true). Confirm that App multi-process supports judgment methods: ad loading and ad display. These two key points are called in different processes, otherwise it is a single process.

If not necessary, try not to use the multi-process switch. Multi-process efficiency is not as high as single process.

**TTCustomController**
```java
new TTCustomController() {
    /**
    * Whether to allow the Pangle to actively use the geographic location information
    * @return true can be obtained, false is prohibited. Default is false
    */
    @Override
    public boolean isCanUseLocation() {
        return super.isCanUseLocation();
    }

    /**
    * Whether to allow Pangle to actively use mobile phone hardware parameters, such as: imei
    * @return true can be used, false is prohibited. Default is false
    */
    @Override
    public boolean isCanUsePhoneState() {
        return super.isCanUsePhoneState();
    }

    /**
    * When isCanUsePhoneState = false, imei information can be passed in, Pangle uses the imei information passed in
    * @return imei information
    */
    @Override
    public String getDevImei() {
        return super.getDevImei();
    }

    /**
    * Whether to allow the Pangle to actively use the ACCESS_WIFI_STATE permission
    * @return true can be used, false is prohibited. Default is true
    */
    @Override
    public boolean isCanUseWifiState() {
        return super.isCanUseWifiState();
    }

    /**
    * Whether to allow Pangle to actively use WRITE_EXTERNAL_STORAGE permission
    * @return true can be used, false is prohibited. Default is false
    */
    @Override
    public boolean isCanUseWriteExternal() {
        return super.isCanUseWriteExternal();
    }
}
```