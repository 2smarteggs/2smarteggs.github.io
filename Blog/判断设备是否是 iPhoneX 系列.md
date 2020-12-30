# 判断设备是否是 iPhoneX 系列

通过是否有以及safeArea判断

```swift
// MARK: - Device Infomation
let isIPhoneXOrHigher: Bool = {
    var iPhoneXSeries: Bool = false
    if UIDevice.current.userInterfaceIdiom != UIUserInterfaceIdiom.phone {
        iPhoneXSeries = true
    }
    if #available(iOS 11.0, *) {
        if UIApplication.shared.windows[0].safeAreaInsets.bottom > 0.0 {
            iPhoneXSeries = true
        }
    }
    return iPhoneXSeries
}()
```

