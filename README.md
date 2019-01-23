# iOS - Widget

[Today Widgets in iOS Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/extensions/widgets/)

[App Extension Programming Guide](https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Today.html)

![](https://i.imgur.com/pPRx5YA.png)

A widget is an extension that displays a small amount of timely, useful information or app-specific functionality. For example, the News widget shows top headlines. Calendar provides two widgets, one that shows today’s events and one that shows what’s up next. Notes lets you preview recent notes and quickly create new notes, reminders, photos, and drawings. Widgets are highly customizable and can contain buttons, text, layout customizations, images, and more.

## 基本設定

## 畫面設定

**更新畫面資料 [widgetPerformUpdateWithCompletionHandler:](https://developer.apple.com/documentation/notificationcenter/ncwidgetproviding/1490262-widgetperformupdatewithcompletio)**

- NCUpdateResultNewData—The new content required you to redraw the view

- NCUpdateResultNoData—The widget doesn’t require updating

- NCUpdateResultFailed—An error occurred during the update process

>  NOTE: 
> <br> 1. Avoid putting a scroll view inside a Today widget. It’s difficult for users to scroll within a widget without inadvertently scrolling the Today view.
> <br> 2. No keyboard entry

## 資料傳遞

## 參考
> https://medium.com/nine9devtw/ios-today-extension-swift-%E6%95%99%E5%AD%B8%E7%AD%86%E8%A8%98-5361446d1950
