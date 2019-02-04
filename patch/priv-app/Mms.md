## 短信
APK位置： `/system/priv-app/Mms/Mms.apk`

apktool命令： `apktool d -r *.apk`

### 移除广告
代码位置： `com/android/mms/ui/MessageItem.smali`
```
.method public needShowADMargin()Z
# return false
```

代码位置： `com/android/mms/util/SmartMessageUtils.smali`

```
.method public static checkCustomerADStatus()Z
# return false
```

APK位置： `/system/app/SmsExtra/SmsExtra.apk`

apktool命令： `apktool d -r *.apk`

### 移除底部菜单
代码位置： `com/miui/smsextra/ui/BottomMenu.smali`
```
.method public static allowMenuMode
# return false
```

