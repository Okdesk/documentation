# Android集成

## 在Android App中添加客服功能

使用Mirachat的Android SDK，提供和Android App的原生(native)集成，提供最优的用户体验。Mirachat Android SDK支持Android Studio + Gradle。

1. 点击下面的链接来下载最新的Mirachat Android SDK：
    <div style="text-align: center;"><div><a href="https://cdn.okdesk.cn/sdk/android/mirachat_android_sdk.zip"><img src="https://cdn.okdesk.cn/documentation/source/images/android.png" class="sdk"></a></div>下载Android SDK</div>

2. 在Android Studio中打开您的项目；

3. 打开下载的zip文件，然后把**mirachat.aar**文件拷贝到下面的目录当中：${project}/app/libs/；

4. 点击Android Studio中的File/New/New Module/Import .JAR/.AAR Package，选择上面的aar文件，然后点击Finish；

5. 点击 Project Structure/{app}/Dependencies，然后点击 Add/Module dependency，在弹出的 Choose Modules 对话框中选择 mirachat，然后 OK；

6. 在${project}/app/build.gradle中，添加下面的依赖：

    `compile 'com.android.support:cardview-v7:23.1.1'`

    `compile 'com.balysv.materialmenu:material-menu:1.5.4'`

    `compile 'com.google.android.gms:play-services-gcm:8.3.0'`

    //RETROFIT

    `compile 'com.squareup.retrofit2:retrofit:2.0.0-beta4'`

    `compile 'com.squareup.retrofit2:converter-gson:2.0.0-beta4'`

    `compile 'com.squareup.retrofit2:converter-scalars:2.0.0-beta4'`

    //OKHTTP

    `compile 'com.squareup.okhttp3:okhttp:3.3.0'`

    //PICASSO

    `compile 'com.squareup.picasso:picasso:2.5.2'`

    //UNIVERSAL IMAGE LOADER

    `compile 'com.nostra13.universalimageloader:universal-image-loader:1.9.4'`
    
    `compile 'com.commit451:PhotoView:1.2.4'`
    
    //Failsafe
    
    `compile 'net.jodah:failsafe:0.9.2'`
    
    `compile ('io.socket:socket.io-client:0.7.0') {
        exclude group: 'org.json', module: 'json'
    }`

7. 在${project}/app/src/main/res/values/styles.xml中，将style标签的parent属性改成：Theme.AppCompat.Light.NoActionBar；

8. 在需要添加客服功能的view中添加一个按钮。为了方便，称其为客服按钮；

9. 在客服按钮的点击响应方法中，添加以下代码：

    `Intent intent = Mirachat.getChatIntent(context, "B3AV712p-B3AV712p", "androidApp", new MirachatEventListener() {
                public void handleEvent(MirachatEvent event) {
                    Log.d("Mirachat", "Mirachat event handler called!");
                }
            });`

    `context.startActivity(intent);`

10. 编译项目，并确保成功通过；

11. 登录工作台，跳转到访客页面。您现在已经准备好处理即将进来的客服请求了；

12. 运行手机上的App，跳转到集成客服按钮的Activity，然后点击该按钮。Mirachat的客服界面出现了。

	在底部的输入框尝试输入“Hi”，稍后您会看到这条消息出现在工作台中。

	在工作台中打开这通对话，然后输入“Hey”，稍后您就会看到它出现在App的客服界面中。

成功！您已经把客服功能集成到Android App里面了。现在您的App用户可以在Android App中发起客服通话了！

<aside class="success">
提示 — Mirachat Android SDK支持Android Studio和Gradle。
</aside>

## 推送

Mirachat 的 Android SDK 的推送设置步骤和 iOS SDK 完全一样，请参照[这里](https://www.mirachat.com/documentation/zh/#推送)。