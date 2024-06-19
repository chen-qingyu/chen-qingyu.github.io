---
title: Windows系统优化
date: 2018-11-13 14:34:03
categories: Others
---

这是我自己在实践中总结的一套优化Windows系统的流程，按流程走一次就够了。适用于Windows 10。

首先，下载一个很小的工具包：[Windows优化](/download/Windows优化.zip)，然后按照下列步骤操作：

1. 设置->应用->应用和功能->卸载多余应用、功能
2. 卸载预装应用->[Uninstall](#Uninstall)
3. 回收站->属性->每个盘：直接删除，显示删除确认对话框
4. 快速访问->选项->Win+E打开此电脑、去掉隐私项
5. 删除此电脑那七个文件夹->/WindowsRegistry.reg
6. 设置->系统->关于->重命名这台电脑
7. 优化右键菜单->/RightMenuMgr/RightMenuMgr.exe
8. Windows管理工具->磁盘清理->以管理员模式清理系统盘
9. 安装[CCleaner](http://www.ccleaner.com/ccleaner/download)->快速清理、注册表清理->卸载CCleaner

另外：

- 如果是笔记本电脑可以：设置->系统->电源和睡眠->其他电源设置->关闭盖子时不采取任何操作，防止一不小心合上盖子休眠导致一些进程被kill。
- 建议：桌面在开机后和关机前都没有任何图标（“此电脑”用<kbd>Win</kbd>+<kbd>E</kbd>打开，“回收站”不用），原因无他，好看而已（前提是有一张好看的壁纸）。

---

<span id="Uninstall">Uninstall</span>

管理员模式打开PowerShell，复制所需命令：

```sh
# 应用商店：
Get-AppxPackage *WindowsStore* | Remove-AppxPackage

# OneNote：
Get-AppxPackage *OneNote* | Remove-AppxPackage

# 3D：
Get-AppxPackage *3d* | Remove-AppxPackage

# Camera相机：
Get-AppxPackage *camera* | Remove-AppxPackage

# 邮件和日历：
Get-AppxPackage *communi* | Remove-AppxPackage

# 新闻订阅：
Get-AppxPackage *bing* | Remove-AppxPackage

# Groove音乐、电影与电视：
Get-AppxPackage *zune* | Remove-AppxPackage

# 人脉：
Get-AppxPackage *people* | Remove-AppxPackage

# 手机伴侣：
Get-AppxPackage *phone* | Remove-AppxPackage

# 纸牌游戏：
Get-AppxPackage *solit* | Remove-AppxPackage

# 录音机：
Get-AppxPackage *soundrec* | Remove-AppxPackage

# Xbox：
Get-AppxPackage *xbox* | Remove-AppxPackage
```

解释一下原理：`Get-AppxPackage`是一条命令，后面接参数。`*`是通配符，能匹配任意字符串，因而`*WindowsStore*`表示含有`WindowsStore`的任意字符串，作为命令的参数。其他同理。由前一个命令得到的标准输出通过管道符`|`转换为标准输入传给`Remove-AppxPackage`这个命令进行卸载操作。

---
