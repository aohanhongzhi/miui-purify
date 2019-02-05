## 状态栏（系统用户界面）
APK位置： `/system/priv-app/MiuiSystemUI/MiuiSystemUI.apk`

apktool命令： `apktool d -r *.apk`

## 优化搜索按钮的点击行为
代码位置： `com/android/systemui/statusbar/HeaderView.smali`
```
.method private buildShortcutClickIntent()Landroid/content/Intent;
# 将代码 sget-boolean v1, Lcom/android/systemui/Constants;->IS_INTERNATIONAL:Z 修改为：
sget-boolean v1, Lcom/winterssy/MiuiPurify;->TRUE:Z
```

