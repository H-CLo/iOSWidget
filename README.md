# iOS - Widget

[Today Widgets in iOS Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/extensions/widgets/)

[App Extension Programming Guide](https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Today.html)

![](https://i.imgur.com/pPRx5YA.png)

A widget is an extension that displays a small amount of timely, useful information or app-specific functionality. For example, the News widget shows top headlines. Calendar provides two widgets, one that shows today’s events and one that shows what’s up next. Notes lets you preview recent notes and quickly create new notes, reminders, photos, and drawings. Widgets are highly customizable and can contain buttons, text, layout customizations, images, and more.

## 理解Today Widgets

- Ensure that content always looks up to date

- Respond appropriately to user interactions

- Perform well (in particular, iOS widgets must use memory wisely or the system may terminate them)

## 替換初始畫面

在**info.plist**裡頭有段叫**NSExtension**，將 **NSExtensionMainStoryboard** 修改為 **NSExtensionPrincipalClass**
<br>並且填上你要使用的畫面，如下

    <dict>
        <key>NSExtensionPointIdentifier</key>
        <string>com.apple.widget-extension</string>
        <key>NSExtensionPrincipalClass</key>
        <string>TodayViewController</string>
    </dict>

## 畫面設定

**每次啟動Widget時，可以透過此事件更新畫面資料 [widgetPerformUpdateWithCompletionHandler:](https://developer.apple.com/documentation/notificationcenter/ncwidgetproviding/1490262-widgetperformupdatewithcompletio)**

可以傳遞三種狀態：

- NCUpdateResultNewData—The new content required you to redraw the view

- NCUpdateResultNoData—The widget doesn’t require updating

- NCUpdateResultFailed—An error occurred during the update process

> 備註：
> <br>1. Widget畫面的初始高度，就是110，最大不會超過畫面的高度
> <br>2. 請盡量避免放進去有關ScrollView元件
> <br>3. Widget沒有鍵盤功能

## 顯示更多

**執行 widgetActiveDisplayModeDidChange的協定，並在裡頭客製化自己要的畫面大小**

    preferredContentSize = CGSize(width: maxSize.width, height: 110)

## 打開App

1. 設定urlScheme在要被開啟的App

2. 透過 **NSExtensionContext** 裡頭的 **openURL:completionHandler:** 去執行

3. 在主程式的AppDelegate openURL裡頭去接收資料

## 資料傳遞

1. 需在Apple Developer 新增Group ID，並使用新的憑證

**UserDefault**

    func saveFileToSharedDefault(str: String) {
        let userDefault = UserDefaults.init(suiteName: "your group id")
        userDefault?.set(str, forKey: "TestWidget")
        userDefault?.synchronize()
    }
    
**FileManager**

    func saveFileToShared(data: Data) {
        guard var url = FileManager.default.containerURL(forSecurityApplicationGroupIdentifier: "your goup id") else {return}
        url.appendPathComponent("Library/Caches/Widget")
        do {
            try data.write(to: url, options: [.atomic])
        } catch {
            
        }
    }

## 參考
> https://medium.com/nine9devtw/ios-today-extension-swift-%E6%95%99%E5%AD%B8%E7%AD%86%E8%A8%98-5361446d1950
