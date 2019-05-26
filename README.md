AppCan 开发用的在线打包方式很是麻烦，我们可以把打包这一步转移到 Android Studio 中来。

该项目就是运行 Android Studio 版的 AppCan hello world project，适用于 AppCan 项目 和 AppCan 插件项目。

# 1. Copy Res 资源

将该项目 Res 目录下的资源全部 copy 到 目标项目中

>添加资源结束后点击编译，没有错误的时候我们再继续下一步

# 2. 在 libs 目录下添加 jar 包

添加 AppCanEngine.jar, 注意选择适合你的版本，已你在 AppCan 平台上选择的 AppCanEngine.jar 版本为准。

同样的，你在开发 AppCan 时选用的一些 jar 包也需要在这添加引用。

- [AppCanEngine 下载链接](http://plugin.appcan.cn/download/appcan-4.0-release/Engine/android/)
- [AppCan 常用插件下载链接](http://plugin.appcan.cn/download/appcan-4.0-release/plugins/)

> 我这里运行的是 Hello World 版，所以只需要添加两个 jar 包，AppCanEngine.jar 和 libacedes-v1.jar 

添加完之后右键点击 jar 包，选择 `add as a library`.

# 3. 在 AndroidManifest.xml 中添加配置

### 添加权限

我这里为了方便，就加了许多，实际是用到什么加什么

```
    <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.FLASHLIGHT" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"
        tools:ignore="ProtectedPermissions" />
    <uses-permission android:name="android.permission.WRITE_SETTINGS"
        tools:ignore="ProtectedPermissions" />
```

### 添加 Application 和 Activity

```
    <application
        android:name="org.zywx.wbpalmstar.widgetone.WidgetOneApplication"
        android:allowBackup="false"
        android:allowClearUserData="false"
        android:hardwareAccelerated="true"
        android:usesCleartextTraffic="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <!--<intent-filter>-->
                <!--<action android:name="android.intent.action.MAIN" />-->

                <!--<category android:name="android.intent.category.LAUNCHER" />-->
            <!--</intent-filter>-->
        </activity>

        <activity
            android:name="org.zywx.wbpalmstar.engine.EBrowserActivity"
            android:alwaysRetainTaskState="true"
            android:configChanges="keyboardHidden|orientation|screenSize"
            android:launchMode="singleTask"
            android:theme="@style/browser_main_theme"
            android:screenOrientation="portrait"
            android:windowSoftInputMode="adjustResize|stateHidden">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="appcanscheme" />
            </intent-filter>
        </activity>
        <activity
            android:name="org.zywx.wbpalmstar.engine.TempActivity"
            android:launchMode="standard"
            android:theme="@style/browser_loading_theme" />
        <activity
            android:name="org.zywx.wbpalmstar.engine.LoadingActivity"
            android:configChanges="keyboardHidden|orientation"
            android:launchMode="standard"
            android:theme="@style/browser_loading_theme">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

            <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
```

# 4. enable multiDex

```
android {
    compileSdkVersion 28
    defaultConfig {
        applicationId "com.york.appcan.basic"
        minSdkVersion 14
        targetSdkVersion 28
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
        //         Enabling multidex support.
        multiDexEnabled true
    }
    ...
}
```

# 5. 添加 AppCan 项目中的代码

将 AppCan IDE 中的代码全部放到 Android assets/widget 目录下。

```
---- assets
    ---- error //原封不动 copy 到你的项目中
    ---- widget //将你在 AppCan IDE 中的代码全部 copy 到该文件夹
    
```


>**注意**：修改 assets/widget/config.xml 中的 obfuscation 属性，务必将其改为 false。


