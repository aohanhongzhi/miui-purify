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

### 修复浏览器跳转异常

代码位置： `com/xiaomi/rcs/tool/RmsUtils.smali`

```
.method public static getRcsServiceAgreementIntent()Landroid/content/Intent;
# 删除诸如以下代码：
const-string/jumbo v2, "com.android.browser"

invoke-virtual {v1, v2}, Landroid/content/Intent;->setPackage(Ljava/lang/String;)Landroid/content/Intent;

const/high16 v2, 0x10000000

invoke-virtual {v1, v2}, Landroid/content/Intent;->addFlags(I)Landroid/content/Intent;
```

### 移除底部菜单

APK位置： `/system/app/SmsExtra/SmsExtra.apk`

apktool命令： `apktool d -r *.apk`

代码位置： `com/miui/smsextra/ui/BottomMenu.smali`
```
.method public static allowMenuMode
# return false
```

