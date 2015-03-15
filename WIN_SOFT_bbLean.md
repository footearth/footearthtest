
  * [bblean中文讨论区 - 深度](http://bbs.deepin.org/forum-382-1.html)
  * [bb4win.org](http://www.bb4win.org)
  * [bb4win - sourceforge](http://bb4win.sourceforge.net/)
  * [bblean 官方网站](http://bb4win.sourceforge.net/bblean/)
  * [bblean 官方论坛](http://www.lostinthebox.com/index.php)
  * [插件下载](http://bb4win.sourceforge.net/plugins.htm)
  * [BB桌面秀](http://www.boxshots.org)
    * [不定期更新的风格包（数千风格）](http://www.boxshots.org/styles.zip)

## 笔记 ##

  * 一些常见教程名称，请自行GOOGLE之
    * bblean 扫盲 + FAQ + 教程
    * bb4win 各版本的区别（发展史）
    * BBlean 最初级的入门教程（纯文字）
    * BBlean + DO 让 Explorer 彻底走开
    * BBlean 的精细教程
  * Beoplayer 在 BBlean 中无法使用。

### 目录结构 ###

```
bblean
│ blackbox.exe
│ blackbox.rc 主配置文件
│ bsetroot.exe 设置墙纸的程序，功能类似linux下的xloadimage
│ bsetroot.rc bsetroot配置文件
│ extensions.rc 一些杂项设置，比如编辑配置文件的编辑器，全局的式样设置
│ INSTALL.bat 把bblean安装成默认shell
│ menu.rc bblean系统菜单
│ plugins.rc 插件的开关文件
│ shellfolders.rc 定义了系统路径的别名，比如 C:\Windows 等
│ stickywindows.ini 设置可以跨越工作区的程序名称
│ UNINSTALL.bat 取消bblean成为默认shell
├─backgrounds 墙纸可以搁这里
├─docs
├─fonts
├─plugins 插件目录
│ ├─bbfoomp
│ ├─bbGesture
│ ├─bbIcons
│ ├─bbInterface 功能强大的容器插件，可以在桌面方便的搁很多很多东西，替代bbSlit,bbSlider等
│ ├─bbKeys 最必要的快捷键插件
│ ├─bbKontroller 日本人写的一个proxy，作为控制bblean的桥梁，给bblean传递消息
│ ├─bbLeanBar 类似win的任务栏，但是功能更多
│ ├─bbLeanSkin wm里边给窗口添加的附加内容，比如标题栏
│ ├─bbMemShrink
│ ├─bbNote
│ ├─bbPager 多个工作区的分页器
│ ├─BBRecycleBin 回收站的接口
│ ├─BBSeekbar
│ ├─bbSlider
│ ├─bbSlit
│ ├─BBSysmon 系统信息监视器，比如cpu,ram,ip,disc
│ ├─bbSysmonPlus
│ ├─bbTray 可以把tray栏提出来
│ ├─bbWinTrans 很酷的透明化窗口功能，类似vista，但耗资源
│ └─BroamTimer
└─styles
```

### 插件 ###

  * bblean 1.17 汉化方法
> > 编辑 $bblean$extensions.rc
      * blackbox.options.translation: nls-cn.txt
      * 开始菜单不汉化，直接编辑 $bblean$menu.rc
  * bbleanskin
> > 编辑 $bblean$plugins\bbleanskin\exclusions.rc
      * Chrome/Chromium
        * `chrome.exe:Chrome_WidgetWin_0`
      * Office 2007
        * `wwlib.dll:OpusApp`
        * `wwlib.dll:_WwB`
      * Gvim
        * `gvim.exe:VIM_MESSAGES`
        * `gvim.exe:Vim`
  * bbleanbar
  * bbkeys
  * bbinterface
  * 输入法图标问题
> > 使用 imetool
      * 输入法风格 勾选
      * 选择 输入法指定器
      * 切换输入法 勾选
      * 快捷键使用 Ctrl + Shift

### bb4win 各版本的区别（发展史） ###

鸣谢：作者-=3p=-

转自：[想看的请翻墙](http://sites.google.com/site/yinsuoqiudao/home/wo-zai-chen-si/bb4win-ge-ban-ben-de-qu-bie)

  * bb4win = blackbox for windows
    * bblean (by grischka) 1.16
      * bblean mod (by Alex3D nocd5 coolguy)
      * bbclean (by Zeytok noccy)
      * BBDeleted (by monohouse)
      * bb2 (by tao)
      * bbcore (by Carsomyr)
    * bblean (by grischka) 1.17 - 2009

|              |bblean    |bbclean   |bbleanmod                                 |
|:-------------|:---------|:---------|:-----------------------------------------|
|菜单图标      |不支持    |智能化    |需手动添加                                |
|菜单音量      |不支持    |支持      |支持                                      |
|菜单位置      |不可配置  |可自定义  |不可配置                                  |
|文字阴影      |不支持    |支持      |支持                                      |
|菜单分割线    |NOP       |+separator|+separator                                |
|桌面鼠标动作  |默认      |+鼠标动作 |+鼠标动作                                 |
|音量broam     |无        |有        |有                                        |
|菜单箭头      |默认      |+9大行星  |+9大行星+图片                             |
|自带bbleanbar |默认      |+图标设置 |+任务窗口宽度+托盘图标显/隐+图标设置+其他 |

bb4win 就是 blackbox for windows 的简称。

bb4win 旗下有很多的分支。

bblean 就是其分支之一。

bblean 1.16 算是作者 grischka 认为较为完美的一版。

**路人甲：功能不够。**

bblean mod 出世了，这是 bblean 的子分支，也就是 bb4win 的孙分支。

支持了菜单调节音量等等功能。

然后他的作者，来自莫斯科的 Alex3D，挂了。

还好来自日本的nocd5把它接了过来。延续更新至今。bb1.17出了以后，中国的coolguy也综合了不少功能进行mod。

代表功能：可用outline来修改字体，动态的子菜单图标。

**路人甲：不方便，麻烦。**

然后是bblean的修改版，bbclean。曾经用过bbleanz这个名字。

也是bb4win的孙分支。

由法国的Zeytok制作，后来，他也挂了。

有瑞典，斯特卡德的noccy接手。最后在某个诡异的实验室中，他们做出了支持4种颜色的bbclean。但是流传度不高。

代表功能：在菜单结尾处<`*`>就可以自动添加菜单图标，可以用代码控制菜单位置。

**路人甲：速度慢了好些。**

来自不知道那里的monohouse制作了BBDeleted。

也是孙分支。

改善了速度和代码，删除了一些没什么大用的东西。

代表功能：有两个版本，一个是intel cpu的 一个是amd cpu的。

**路人甲：不漂亮。**

德国的tao（读作：套）制作了bb2

还是孙分支。

支持了半透明，和窗口修改。

然后卒之，中国的风之都接手，修改大量bug，遂，卒之。

代表功能：漂亮了很多，拥有一个像mac系统的dockbar一样的快捷方式栏。

**路人甲：vista能用不？**

南非，比勒陀利亚的Carsomyr制作了bbcore。

同上。

修改了不少代码，可以完美运行于vista。我没啥条件测试。功能上多了一个他自己做的boxbar。可以竖起来用。

代表功能：用在vista上，可以竖起来的boxbar。

**路人甲：怎么老是这些东西，都是bblean1.16的，两年没有更新了。**

grischka在09年终于更新了他的作品，只是源代码部分，由nocd5修订成型，从此bblean1.16改为1.17。

这里是子分支。

做了很多改变，但是他也说过，这始终是bblean不是bbclean也不是bbleanmod。所以他不考虑加载其中的功能。

没死，据说还有可能会更新。因为这个只是一个test而不是最终版。

代表功能：汉化包，或者是xx包。可以简单地修改所有的语言。部分功能增强，例如代码控制菜单的位置和部分属性。

**路人甲：难道就没有一个绿色的，精简的，汉化的，免费的......**

话说到这儿，grischka拿起手手边的烟灰缸像，路人甲砸去。血水顺着红色的沙发，缓缓地留下来。但是grischka还没有停止他的动作，像咬碎牙齿一般的怒意涌了出来。一下，两下...

不知道过了多久，路人甲的手慢慢地停止了抽搐...

末了，grischka用血染的手颤抖地点燃了一根烟，烟雾触响了警报器，雨点一般的水喷射出来，grischka微笑着洗干净了烟灰缸，混进慌乱的人群中。

### 让 BBnote 支持汉字 ###

[原文看这里](http://hi.baidu.com/kun_g/blog/item/8df97c344330d3b1d1a2d312.html)

这个 BBnote 是 BBlean 的一个小工具。

其实说它不支持汉字有点冤枉它了，因为用它打开TXT文件（RC以外的文件应该都可以）就会发现汉字显示的很正常。之所以在RC文件中就出问题是因为它要实现语法高亮，而在进行语法高亮时把所有字符都当ASCII处理了。

带参数（需要编辑的文件名）载入 BBnote，断 ReadFile，然后用内存断点跟踪存储文件内容的那块内存。程序来回捣腾这块内存里的数据后，来到这个地方：

```
004043BE /$ A1 543B4100   mov     eax, dword ptr [413B54]
004043C3 |. 8B4C24 04     mov     ecx, dword ptr [esp+4]
004043C7 |. 8B50 0C       mov     edx, dword ptr [eax+C]
004043CA |. 3BCA          cmp     ecx, edx
004043CC |. 7C 0F         jl      short 004043DD
004043CE |. 3B48 10       cmp     ecx, dword ptr [eax+10]
004043D1 |. 7D 0A         jge     short 004043DD
004043D3 |. 2BC2          sub     eax, edx
004043D5 |. 8A8408 ED0000>mov     al, byte ptr [eax+ecx+ED]
004043DC |. C3            retn
```

这个函数就是用来读文件缓冲区的，被N处调用。乱跟一通就跟到了这里：

```
004094E9 |. E8 D0AEFFFF   |call    004043BE
004094EE |. 8AD8          |mov     bl, al
004094F0 |. 59            |pop     ecx
004094F1 |. 80FB 20       |cmp     bl, 20
004094F4 |. 885D FC       |mov     byte ptr [ebp-4], bl
004094F7 |. 0F84 19010000 |je      00409616
004094FD |. 80FB A0       |cmp     bl, 0A0
00409500 |. 0F84 10010000 |je      00409616
00409506 |. 80FB 80       |cmp     bl, 80
00409509 |. 0F83 BA010000 |jnb     004096C9
```

就是在00409506处，它把汉字给忽略掉了……直接跳到：

```
004096C9      33F6          xor     esi, esi
004096CB      C645 FF 01    mov     byte ptr [ebp-1], 1
004096CF      46            inc     esi
004096D0    ^ E9 5DFFFFFF   jmp     00409632
```

这个jmp是跳过去显示当前字符串的，esi里放的是字符串的字节数，这个地方把字节数设为1了。来一段代码给它改成2好了：

＝＝＝＝＝004096C9处代码

```
004096C9     /E9 C44E0000   jmp     0040E592
004096CE     |90            nop
004096CF     |90            nop
004096D0    ^|E9 5DFFFFFF   jmp     00409632
```

＝＝＝＝＝0040E592处代码

```
0040E592      C645 FF 01    mov     byte ptr [ebp-1], 1
0040E596      BE 02000000   mov     esi, 2
0040E59B    ^ E9 30B1FFFF   jmp     004096D0
```

o~yeah

ps:BBNOTE.INI里可以设置字体