#App Extension Programming Guide
#App 扩展编程指南




>**非常重要**




表1-1列出了iOS和OS X的扩展点，并给出了任务，你可能会在一个应用程序扩展为每个扩展点实现的一个例子。



|-|-|
| Today (iOS and OS X) | Get a quick update or perform a quick task in the Today view of Notification Center (A Today extension is called a widget) |
|Share (iOS and OS X) |Post to a sharing website or share content with others|



>Each app extension you create matches exactly one of the extension points listed in Table 1-1. You don’t create a generic extension that matches more than one extension point.

>**重点**
>你创建的每个应用程序的扩展完全匹配表1-1中列出的扩展点之一。您不可能创建一个符合多个扩展点的扩展。














>注释：即使您的应用程序扩展名不显示任何自定义用户界面（不是图标等），用户仍然明白，你的扩展是从当前的应用程序不同，因为他们采取了具体的行动来激活它。

##Understand How an App Extension Works
##了解一个App扩建工程 







![](https://developer.apple.com/library/ios/documentation/General/Conceptual/ExtensibilityPG/Art/app_extensions_lifecycle_2x.png)



在图2-1的步骤3中，在用户执行或取消该任务的应用程序的扩展或解散它。响应于这个动作，扩展通过立即执行用户的任务，或者如果需要的话，启动一个后台进程来执行它完成主机应用程序的请求。主机应用程序的销毁扩展的视图和用户返回到主机的应用程序在其前面的内容。当该扩展的任务完成时，无论是立即或稍后，其结果可以被返回给主机的应用程序。






在一个典型请求/响应事务处理，该系统将打开代表一个主机应用程序的一个应用程序扩展，在由主机提供的扩展的上下文传送数据。扩展显示用户界面，执行一些工作，如果需要返回数据到主机。 






由于在系统中的聚焦机制，一个应用程序扩展是没有资格参加某些活动。一个应用程序扩展不能： 

* 访问sharedApplication对象，所以不能在那个对象上使用任何方法 
* 使用标头文件中的任何API和NS_EXTENSION_UNAVAILABLE宏或者不可用 
* 宏，或者不可用的框架，任何API 
* 例如，在8.0的iOS，在HealthKit框架和EventKit UI框架是不可用的应用程序扩展。 
* 访问摄像头、麦克风或在iOS设备上执行长时间运行的后台任务 
* 这一限制的具体因平台而异，如在本文件中的扩展点的章节介绍。
