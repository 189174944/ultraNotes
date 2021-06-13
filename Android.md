> 隐藏标题栏 
```
getWindow().addFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN);
getSupportActionBar().hide();
setContentView(R.layout.activity_splash);
```

> 在AndroidManifest设置android:parentActivityName会显示会退按钮

DialogFragment、PopWindow、



>android网络权限配置

```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>

		<!--    网络请求权限-->
    <uses-permission android:name="android.permission.INTERNET" />
    <!--外部文件存储权限-->
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```