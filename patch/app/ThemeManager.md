## 主题
APK位置： `/system/app/ThemeManager/ThemeManager.apk`

apktool命令： `apktool d -r *.apk`

### 删除首页的banner推荐
代码路径： `com/android/thememanager`
```
.method public getAdMarker()I
# return false

# 在上面方法对应的类中有一个布尔方法，通过 ->getImgUrls()Ljava/util/List; 定位
# return false
# 函数原型： .method private static isSupported
```
代码路径： `com/android/thememanager/view`
```
# 在 res/values/public.xml 中找到 ad_banner_view 对应的 id
# 在当前路径搜索该id所在的方法，并在当前类搜索调用该方法的函数，return null
```
### 删除在线主题详情页的广告
代码路径： `com/android/thememanager/v9`
```
# 在当前路径搜索 onAdLoadSucceeded 定位相关方法
.method public onAdLoadSucceeded
# 修改该方法的函数体与 .method public onAdLoadFailed 方法一致
# 修改后的示例代码：
.method public onAdLoadSucceeded(Lcom/miui/zeus/chameleon/sdk/api/IChameleonNativeAd;)V
    .locals 3

    iget-object v0, p0, Lcom/android/thememanager/v9/b/c;->a:Lcom/android/thememanager/v9/b/b;

    invoke-static {v0}, Lcom/android/thememanager/v9/b/b;->a(Lcom/android/thememanager/v9/b/b;)Ljava/util/List;

    move-result-object v0

    invoke-interface {v0}, Ljava/util/List;->iterator()Ljava/util/Iterator;

    move-result-object v1

    :cond_0
    :goto_0
    invoke-interface {v1}, Ljava/util/Iterator;->hasNext()Z

    move-result v0

    if-eqz v0, :cond_1

    invoke-interface {v1}, Ljava/util/Iterator;->next()Ljava/lang/Object;

    move-result-object v0

    check-cast v0, Lcom/android/thememanager/v9/b/a$a;

    if-eqz v0, :cond_0

    invoke-interface {p1}, Lcom/miui/zeus/chameleon/sdk/api/IChameleonNativeAd;->getTagId()Ljava/lang/String;

    move-result-object v2

    invoke-interface {v0, v2}, Lcom/android/thememanager/v9/b/a$a;->a(Ljava/lang/String;)V

    goto :goto_0

    :cond_1
    return-void
.end method
```

### 修复反编译导致DRM异常
代码路径： `com/android/thememanager`

搜索代码 ` Lcom/android/thememanager/jni/DrmAgent;->`，删除诸如以下的调用链：
```
new-instance v0, Lcom/android/thememanager/jni/DrmAgent;

invoke-direct {v0}, Lcom/android/thememanager/jni/DrmAgent;-><init>()V

iput-object v0, p0, Lcom/android/thememanager/a/b/c;->c:Lcom/android/thememanager/jni/DrmAgent;
```
```
iget-object v0, p0, Lcom/android/thememanager/a/b/c;->c:Lcom/android/thememanager/jni/DrmAgent;

invoke-virtual {v7}, Lcom/android/thememanager/e/w;->c()Ljava/lang/String;

move-result-object v1

invoke-virtual {v0, v8, v1}, Lcom/android/thememanager/jni/DrmAgent;->saveRightObject(Ljava/lang/String;Ljava/lang/String;)V
```

