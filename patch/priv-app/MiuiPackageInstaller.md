## MIUI软件包安装程序
APK位置： `/system/priv-app/MiuiPackageInstaller/MiuiPackageInstaller.apk`

安卓L及以下版本： `/system/priv-app/PackageInstaller/PackageInstaller.apk`

apktool命令： `apktool d *.apk`

### 移除广告
代码位置： `com/android/packageinstaller/config/CommonConfig.smali`
```
.method public isAdsEnable()Z
# return false
```

### 移除『资源推荐』设置项
代码位置： `com/android/packageinstaller/SettingsActivity.smali`
```
.method protected onCreate
# 在方法结束 return-void 前增加以下代码：
const-string v0, "pc_group"

invoke-virtual {p0, v0}, Lcom/android/packageinstaller/SettingsActivity;->findPreference(Ljava/lang/CharSequence;)Landroid/preference/Preference;

move-result-object v0

check-cast v0, Landroid/preference/PreferenceGroup;

iget-object v1, p0, Lcom/android/packageinstaller/SettingsActivity;->mOpenAds:Landroid/preference/CheckBoxPreference;

invoke-virtual {v0, v1}, Landroid/preference/PreferenceGroup;->removePreference(Landroid/preference/Preference;)Z
```
代码位置： `res/xml/settings.xml`
```
# 为 pref_key_open_ads 所在的 <PreferenceCategory> 增加 android:key 属性
android:key="pc_group"
```

