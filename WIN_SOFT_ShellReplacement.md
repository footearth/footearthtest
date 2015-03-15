## Game Boost ##

> 原名是BLEEM BOOST。安装替换成Shell后，在顶部显示一个图标，右键可以配置。但是菜单不可定制，相当于一个调用Explorer的Run Shell。同名字一样，是为运行游戏而设计成功能简单资源占用少的外壳。只能手动改system.ini还原成explorer。

## EVWM ##

> 已绝迹的Shell，小巧占用资源少。支持Litestep，Wharfapp plugin。左右键点击桌面弹出菜单。可定制。但是如果快捷方式错误会还原到Explorer。

## Emerge Desktop ##

> 只支持NT系统。可定制菜单、快捷键等，快速！支持额外的Applets组件。

## DARKSTEP ##

> 支持 Lite Step 主题和模块，基本内核是命令行模式，用过 Lite Step 的才易上手。需手动修改注册表或下载额外程序来改回成explorer。

## DESKTOP MANAGER ##

> DM实际上是一个虚拟桌面工具，同时也可替换成Shell(system.ini)。以模块来增强功能，自带RAM监控，Email检测。

## Aston ##

> 这个不用说了，迄今为止我见过与Windows最兼容的Shell了。使用简单，用户可定制化强。内核占用资源少且快。等待A2的诞生。

## Windows XP Embedded ##

> 微软提供的可自定义组件和设备支持的XP系统制作版本。因此也可以自定义系统启动的主Shell。

P.S. 外壳很多，大多数是基于LiteStep的，故功能界面都差不多，我就不一一介绍了。像Talisman, LiteStep, Blackbox等有名的Shell就略了。还有一些不再开发的网上也下载不到的我也没有去试。
更多可见Shell Family Tree Shell List

如果程序不带还原功能的，可以做如下修改：

  * Windows 9x下是修改system.ini里的shell=explorer.exe。

  * NT系统是修改注册表的Logon，比如：

```
Windows Registry Editor Version 5.00 

[HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon] 

"Shell"="explorer.exe" 
```

## bblean ##

> 基于blackbox的简小版。同bluebox等一样可以改变皮肤，由菜单和任务栏组成。很方便。

## NextWin ##

> 能在explorer之上运行。很 Next Step。只有80K，但功能却不弱。

## Lite Shell ##

> 一名学生写的外壳，简单到只有一个菜单。占用很小的RAM和CPU。反安装可以还原外壳。

## Codex 3000 Shell ##

> 我在Win Me上没有安装成功。简介说有自己的控制面板、任务列表等等，还可皮肤化。由于支持的人不多故还是beta版就停止制作了。

## Shape E ##

> 比较新的一个Shell，可定制功能强，界面很漂亮。也比较稳定。插件也不少，就是速度不快。

## SERENADE ##

> 有些岁数的Shell了。主页很漂亮，似乎仍在开发。但我没怎么研究，定制起来似乎有点麻烦。

## Outsider 99 ##

> Outsider可以像WindowBlinds一样改变Windows外观，改变任务栏，选项很多，自带简单的皮肤编辑器和文件浏览器。虽然在win9x下可能会出错，但确实很不错。可惜不再更新了。

## @Shell ##

> 只有一个工具条，功能就调用外部程序来实现。唯一的功能是cpu占用的监测。 可以在explorer上运行也可以单独做为Shell(手动)

## BeOs ##

> 模仿Beos的Shell。因为网上只有未编译版本， 我手头上没有VB去编译，况且BeOS本身就支持在Windows之上运行的，所以还不如装原版。

## GeoShell ##

> Geo Shell的外壳。很漂亮，有不少插件，速度也不错。就是用户定制不太方便，新版已经有了交互的定制程序，在安装文件夹下的Utilities下面。主页上还提供了方便的Shell设置工具。