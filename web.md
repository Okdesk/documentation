# 网页集成

## 在网页中添加客服功能

在网页中添加客服功能非常简单，只需要1分钟。

1. 如果还没有创建 Okdesk 帐户，请现在<a href="https://www.okdesk.cn/register" target="_blank">创建</a>一个，否则直接到下一步；

2. <a href="https://www.okdesk.cn/login" target="_blank">登录</a>到 Okdesk 工作台；

3. 在工作台中，点击网页设置，拷贝 **Javascript 代码**文本框中的代码；

4. 在编辑器中打开您需要集成客服聊天功能的网页，然后在 **&lt;body&gt;** 标签前面粘贴第3步拷贝的代码，如果您的页面代码是动态生成的，比如说用 Java、PHP 或者是其他语言，则需要保证该行 JS 代码位于生成的 HTML 代码的 **&lt;body&gt;** 标签前面。如下图：

	![插入Javascript代码](https://www.okdesk.cn/tutorial/web/img/js_added_zh.png)

5. 如果您还有其他的网页需要集成客服聊天功能，重复上一步；

6. 如果在本地编辑这些网页的话，还需要把网页上传到服务器；

7. 登录工作台，跳转到访客页面。您现在已经准备好处理即将进来的客服请求了；

8. 在浏览器中刷新服务器上的网页，您将会看到右下角有一个小窗口，点击它，然后整个窗口就会弹出来。这个窗口叫对话窗口。

	在对话窗口中的文本输入框里输入“Hi”并按回车键，接下来您会在工作台中看到该消息了。

	在工作台中点击该通话，然后在文本框中输入“Hey”并发送，接下来该消息将会出现在该网页的对话窗口中。

现在，您的访客可以在网页跟客服聊天了。由于该 JS 代码同时支持桌面网页和移动网页，因此手机网页访客也可以跟客服聊天!

<aside class="tip">
网页集成 Okdesk 客服，只需要插入一行 Javascript 代码。同时支持桌面网页和移动网页。
</aside>

## 对话窗口

在网页上嵌入 JS 代码后，在网页的右下方会出现最小化的对话窗口。

在桌面网页上是这样的：

![对话窗口](https://www.okdesk.cn/documentation/source/images/widget.png)

在移动网页上是这样的：

<p style="text-align: center;">
    <img src="https://www.okdesk.cn/documentation/source/images/widget_mobile.png" style="height: 480px;">
</p>

点击它，完整的对话窗口将会弹出来。在对话窗口中，访客可以给客服发送消息以及接受来自客服的消息。

<aside class="tip">
对话窗口可以在以下浏览器中运行：IE9/IE10/IE11/Edge, Chrome, Firefox, Opera, Safari 5.1及更高，以及国内主流的浏览器。不支持 IE8 以及更低版本的 IE。
</aside>

## 定制对话窗口文字

你可以定制对话窗口的文字来符合要求。比如说，当客服在线时，想要对话窗口的标题显示为"需要帮助吗?"，你可以有两个办法：

1. 在工作台->网页集成->界面文本->定制界面文本中设置；这种方法比较简单，但是只能够定制对话窗口部分位置的文本；

2. 用 Javascript API setString 方法来完成：

    1. 找到需要更改的文字的 string_name：浏览至[这里](https://www.okdesk.cn/?mirachat_develop_mode=on)，然后把鼠标悬停到你想要改变的文字的位置，然后 string_name 就会弹出来。如下所示：

        <p style="text-align: center;">
            <img src="https://www.okdesk.cn/documentation/source/images/widget_string.png">
        </p>

        在上图中，chat_button_online 就是我们要找的 string_name。
    2. 找到 string_name 以后，调用下面的方法来改变该段文字：
        `setString(string_name, "需要帮助吗?", "zh");`

    这种方法可以定制桌面网页对话窗口的任何地方的文本。详情可以看「API 参考」中的<a href="https://www.mirachat.com/api/zh/#setstring" target="_blank">setString</a>。

<aside class="warning">
目前移动网页对话窗口的文本不可以定制。
</aside>
        
## 定制对话窗口外观

可以选择一个颜色主题，来达到改变对话窗口外观的目的。在工作台->网页集成->通用->颜色主题中设置。

## 定制对话窗口行为

在某些情况下，我们希望对话窗口执行某些动作，来达到更好地沟通的目的。例如打开/隐藏/显示窗口，发送消息等。这可以通过使用触发器完成。通过灵活使用强大的触发器功能，可以更好地满足企业的业务需要。

每一个触发器规则由一系列的条件和动作组成。触发器的基本工作原理是：当定义的条件满足的时候，执行对应的动作。

例如，如果访客在付款页面上面停留超过2分钟的时候，可能是碰到了问题。为了防止顾客流失，我们希望向访客发送一条提供帮助的消息，邀请他加入对话，从而帮他解决问题。为了达到这个目的，我们可以创建一个触发器，它的条件是"在付款页面上面停留超过2分钟"，动作是"发送提供帮助的消息"。如下所示：

(TBD)
