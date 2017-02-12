# iOS 集成

## 在 iOS App 中添加客服功能

使用 Okdesk 的 iOS SDK，提供和 iOS App 的原生(native)集成，提供最优的用户体验。本教程对 Objective-C 和 Swift 项目同时适用。目前 Okdesk iOS SDK 支持 Xcode 8，Xcode 7.3 和 7.3.1，不支持 Xcode 7.3 以下版本。

1. 点击下面的链接来下载最新的 Okdesk iOS SDK：
    <div style="text-align: center;"><div><a href="https://cdn.okdesk.cn/sdk/ios/mirachat_ios_sdk.zip"><img src="https://cdn.okdesk.cn/documentation/source/images/ios.png" class="sdk"></a></div>下载 iOS SDK</div>

2. 在 Xcode 中打开您的项目；

3. 打开下载的 zip 文件，然后把 **Mirachat.framework** 文件拖放到 Xcode 里面的项目中，如下图所示：

	![添加 SDK 文件](https://www.okdesk.cn/tutorial/ios/integrate-live-chat/img/SDK_added_zh.png)

4. 点击[项目]/Targets下面的[App]/General，然后把 **Mirachat.framework** 添加到 Embedded Binaries，如下图所示：

    ![添加到Embedded Binaries](https://www.okdesk.cn/tutorial/ios/integrate-live-chat/img/Embedded_zh.png)

5. 在项目的 Info.plist 中添加以下3项，来满足 iOS 10 的隐私设置要求：

    Key | Value
    ---------- | -------
    NSPhotoLibraryUsageDescription | Allow Mirachat to access photo library.
    NSCameraUsageDescription | Allow Mirachat to access camera.
    NSMicrophoneUsageDescription | Allow Mirachat to access microphone.

    如果忘记添加以上3项，app 在 iOS 10 设备上运行可能会崩溃；

6. 在需要添加客服功能的 view 中添加一个按钮。为了方便，称其为客服按钮；

7. 如果还没有创建 Okdesk 帐户，请现在[创建](https://www.okdesk.cn/register)一个，否则直接到下一步；

8. [登录](https://www.okdesk.cn/login)到 Okdesk 工作台；

9. 在工作台中，点击 App 集成 | 添加 App，然后填写 app 名称和推送 URL (可选)，然后保存。点击 App 集成，然后拷贝刚才创建的 app 的 **App ID**。我们接下来需要 App ID 来激活客服功能；

10. 如果您的项目使用 Objective-C，那么：

	1. 在客服按钮所在的 view 的 view controller 文件的开始引入 Mirachat 头文件：

			`#import <Mirachat/Mirachat-Swift.h>`

	2. 在客服按钮的 TouchUpInside 的 IBAction 方法中添加下面的代码：

			`[self pushViewController:[Mirachat getChatViewController:@"appID" appName:@"Store 1.0A" eventHandler:nil] animated:YES completion:nil];`

	然后用第9步中得到的 App ID 来代替上面的 appID；

11. 如果您的项目使用 Swift，那么：

	1. 在客服按钮所在的 view 的 view controller 文件的开始引入 Mirachat 库：

			`import Mirachat`

	2. 在客服按钮的 TouchUpInside 的 IBAction 方法中添加下面的代码：

			`self.pushViewController(
                Mirachat.getChatViewController("appID", appName: "Store 1.0A", eventHandler: nil),
                animated: true,
                completion: nil)`

	然后用第9步中得到的 App ID 来代替上面的 appID；

12. 编译项目，并确保成功通过；

13. 登录工作台，跳转到访客页面。您现在已经准备好处理即将进来的客服请求了；

14. 运行手机上的App，跳转到集成客服按钮的 view，然后点击该按钮。Okdesk 的客服界面出现了。

	在底部的输入框尝试输入“Hi”，稍后您会看到这条消息出现在工作台中。

	在工作台中打开这通对话，然后输入“Hey”，稍后您就会看到它出现在 App 的客服界面中。

成功！您已经把客服功能集成到 iOS App 里面了。现在您的 App 用户可以在 iOS App 中发起客服通话了！

访问这个 Github <a href="https://github.com/mirachat/ios-oc-demo" target="_blank">链接</a>来下载集成好的 Objective-C 样例工程。

<aside class="success">
提示 — Okdesk iOS SDK 可以用于 Objective-C 或者 Swift 项目中。
</aside>

## 处理 Okdesk 事件

```objective_c
// Objective C
UIViewController* vc = [Mirachat getChatViewController:@"tenant_code"
appName:@"Store 1.0A"
appId:@"0"
eventHandler:^(MirachatEvent *event) {
	if (event.type == MirachatEventTypeMessageReceived)
	{
		dispatch_async(dispatch_get_main_queue(), ^{
			[[self chatButton] setTitle:@"New" forState:UIControlStateNormal];
		});
	}
	else if (event.type == MirachatEventTypeMessageDeliveryFailed)
	{
		dispatch_async(dispatch_get_main_queue(), ^{
			[[self chatButton] setTitle:@"Failed" forState:UIControlStateNormal];
		});
	}
	else if (event.type == MirachatEventTypeMessageSent)
	{
		dispatch_async(dispatch_get_main_queue(), ^{
			[[self chatButton] setTitle:@"Chat" forState:UIControlStateNormal];
		});
	}
}];

[self presentViewController: vc animated:YES completion:nil];
```

```swift
// Swift
func handler(event: MirachatEvent!) -> Void {
	func changeButton() -> Void {
		if (event.type == MirachatEventType.MessageReceived)
		{
			self.chatButton.setTitle("New", forState: UIControlState.Normal);
		}
		else if (event.type == MirachatEventType.MessageDeliveryFailed)
		{
			self.chatButton.setTitle("Failed", forState: UIControlState.Normal);
		}
		else if (event.type == MirachatEventType.MessageSent)
		{
			self.chatButton.setTitle("Chat", forState: UIControlState.Normal);
		}
	}

	dispatch_async(dispatch_get_main_queue(), changeButton);
}

	var vc:UIViewController = Mirachat.getChatViewController("tenant_code", appName: "Store 1.0A", appId: "0", eventHandler: handler)

	self.presentViewController(
		vc,
		animated: true,
		completion: nil)
```

处理 Okdesk 事件可以更有效地更新 app 的状态，吸引用户注意力，使其及时返回通话界面。Okdesk 可以产生以下4种事件：

    事件 | 原因
    ---------- | -------
    Mirachat_MessageReceived | 收到新的消息
    Mirachat_MessageSent | 消息已经发送
    Mirachat_MessageDelivered | 消息已经送达
    Mirachat_MessageDeliveryFailed | 消息无法送达

比如当 Okdesk 收到一条新的消息，会产生一个 **Mirachat_MessageReceived** 事件。类似地，当一条消息投递到发送队列后，也会产生一个 **Mirachat_MessageSent** 事件。如果消息成功地送达对方，会产生一个 **Mirachat_MessageDelivered**。如果由于网络离线或者其他原因，导致消息无法送达，会产生一个 **Mirachat_MessageDeliveryFailed** 事件。您的 app 可以截获这些事件，在回调函数中处理自定义的任务。

要处理 Okdesk 事件，只需要在调用 getChatViewController 的时候传递一个自定义的 block 就可以了。该 block 有一个 MirachatEvent 参数，代表发生的事件。当 Okdesk 事件发生时，该 block 根据不同的事件做不同的处理。如右所示。同样地，记得用公司代码来代替 tenant_code。

在右边的代码中，当收到新消息的时候，我们把通话按钮的文字设成 New；当发送了一条消息的时候，把通话按钮的文字设成 Chat；当消息无法送达的时候，把通话按钮的文字设成 Failed。当然您也可以采用其他的通知方式，比如播放音效。这样即使用户已经退出 Okdesk 通话界面，也能及时获知通话的状态。

<br>
<br>

<aside class="success">
提示 — 适当地处理 Okdesk 事件可以有效地使用户获知通话的状态。
</aside>

## 推送
如果 app 在后台，当客服发送消息的时候，Okdesk 可以向指定的服务器推送通知。设置的方法如下：

1. 点击 App 集成，然后点击 app 的"编辑"链接；

2. 填写"推送URL"；如果在创建 App 时已经填写，可以忽略；

3. 在您的推送URL地址建立一个 PHP 文件，内容如下：(TBD)。

在上面的文件中，您可以接受来自 Okdesk 的推送，并且进一步把它推送到对应的设备上去。

## 定制界面

```objective_c
// Objective C
[Mirachat setOptions: @{@"theme" : @"cyan", @"companyTitle" : @"秒通客服", @"greeting" : @"亲，您好！"}];
```

```swift
// Swift
Mirachat.setOptions(["theme": "red", "companyTitle": "秒通客服", "greeting": "亲，您好！"]);
```

您可以定制您的界面来使其更加符合您的品牌风格。这通过调用 setOptions 方法来实现。

### Objective-C 方法

`+ (void)setOptions:(NSDictionary *)options`

### options 键说明

键值 | 类型 | 说明
--------- | ------- | -----------
theme | NSString | 主题颜色，为"purple", "red", "yellow", "cyan"其中之一
companyTitle | NSString | 公司名称，显示在聊天界面的顶部
greeting | NSString | 打招呼消息

<aside class="warning">
注意 — setOptions 必须要在 getViewController 之前调用，否则将不起作用。
</aside>

## 定制文字

您可以改变界面中的文字，这通过在 custom.bundle/Resources 目录下面添加一个 Localizable.strings 文件来完成。
