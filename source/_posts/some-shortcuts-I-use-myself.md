---
title: 一些自用的快捷方式（？）
date: 2026-05-24 04:54:57
toc: true
---

记录一些自用的小技巧和快捷方式，防止以后忘记。

目前包括：

1. 躺在床上关闭 Mac 显示器
2. 快速移除 Gatekeeper 隔离标记
3. 在通知栏开关 ADB

<!--more-->

# 1. Shortcuts 调整 Mac 音量 / 关闭显示器

用来躺在床上远程调 Mac 音量和关闭显示器。


## 调整音量
在Shortcuts中创建：

>**Run script over SSH**
>Command `osascript -e "set colume output volume [Ask Each Time]"`

## 关闭显示器
在Shortcuts中创建：

>**Run script over SSH**
>Command `pmset displaysleepnow`

<img src="shortcuts-1.png" style="zoom:28%;" />
<img src="shortcuts-2.png" style="zoom:28%;" />


# 2. Remove Quarantine Flag


众所周知，mac 遇到签名问题无法运行 App 时，一般执行：

```bash
sudo spctl --master-disable
```

然后修改：

**System Settings → Privacy & Security → Security → Allow applications from → Anywhere**

即可运行。

有时候还会遇到 App “is damaged and can’t be opened. You should move it to the Trash.”
这是 **Gatekeeper 隔离标记** 导致的，使用命令行移除即可解决。

1. 只移除 quarantine 标记
```bash
xattr -r -d com.apple.quarantine /Applications/xxx.app
```
2. 移除所有扩展属性
```bash
xattr -cr /Applications/xxx.app
```

推荐优先使用第一种，第二种会删除所有扩展属性。

## 加入Finder右键菜单



按照下图，创建一个 **Automator / Quick Action**：

<img src="automator-1.png" style="zoom:28%;" />

<img src="automator-2.png" style="zoom:28%;" />

> **Workflow receives current** `files or folders` in `Finder.app`

> **Get Selected Finder Items**

> **Run Shell Script**
> Pass input  `as arguments`
> Command ```osascript -e "do shell script \"xattr -r -d com.apple.quarantine $(printf '%q ' "$@")\" with administrator privileges"```

创建后脚本会保存到：

```bash
~/Library/Services/Remove Quarantine Flag.workflow
```

并添加到Finder右键菜单：

<img src="automator-3.png" style="zoom:28%;" />

~~但是这个脚本不能处理文件名里有空格/中文的文件，使用之前记得把app重命名一下再执行~~

# 3. 在通知栏开关ADB（要root）

使用了这三个root命令实现：

```bash
am start -a android.settings.APPLICATION_DEVELOPMENT_SETTINGS # 打开开发者设置
settings get global adb_enabled # 获取adb状态
settings put global adb_enabled 0/1 # 更改adb状态
```

安装 [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm)

切换到**TASKS**标签页创建两个Task: 
- `Open Developer Options`
- `Toggle USB Debug`

添加完成后手动执行一次Toggle USB Debug，然后就可以去通知栏里添加开关了。

<img src="tasker-1.png" style="zoom:28%;" />

<img src="tasker-2.png" style="zoom:28%;" />

<img src="tasker-3.png" style="zoom:28%;" />

<img src="tasker-4.png" style="zoom:28%;" />

## Open Developer Option

>**Run Shell**
>Command `am start -a android.settings.APPLICATION_DEVELOPMENT_SETTINGS`
>Use Root `✓`

## Toggle USB Debug

>**Run Shell**
>Command `settings get global adb_enabled`
>Use Root `✓`
>Store Optout In `%adb`

>**If** `%adb ~ 1`

>**Run Shell**
>Command `settings put global adb_enabled 0`
>Use Root `✓`

>**Else If** `%adb ~ 0`

>**Run Shell**
>Command `settings put global adb_enabled 1`
>Use Root `✓`

>**End If**

>**Run Shell**
>Command `settings get global adb_enabled`
>Use Root `✓`
>Store Optout In `%adb`

>**If** `%adb ~ 1`

>**Set up Quick Setting Tile**
>Number `1st`
>Task `Toggle USB Debug`
>Status `Active`
>Long Click Task `Open Developer Options`
>Icon `android.resource://net.dinglisch.android.taskerm/drawable/mw_device_usb`

>**Else If** `%adb ~ 0`

>**Set up Quick Setting Tile**
>Number `1st`
>Task `Toggle USB Debug`
>Status `Inactive`
>Long Click Task `Open Developer Options`
>Icon `android.resource://net.dinglisch.android.taskerm/drawable/mw_device_usb`

>**End If**
