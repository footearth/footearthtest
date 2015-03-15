## EGE 图形库 ##

  * 简介
    * 为什么要写这个库？
    * 本图形库的优点
    * 简单安装说明
    * 简要使用说明
  * 函数库
    * 绘图环境相关函数
    * 颜色表示及相关函数
    * 绘制图形相关函数
    * 文字输出相关函数
    * 图像处理相关函数
    * 鼠标相关函数
    * 时间函数
    * 数学函数
    * 随机函数
    * 其它函数
  * 教程
    * 第一章
    * 第二章
    * 第三章

## 简介 ##

> [EGE](http://code.google.com/p/misaka/)（Easy Graphics Engine）库是一个类似graphics.h的面向C/C++语言新手的BGI图形库。

> 它的使用方法与TC中的graphics.h相当接近，只要 `#include "graphics.h"` 就可以了。对于学习过TC图形的同学来说很容易上手，而且因为接口意义直观。即使是之前完全没有接触过图形编程的，也能迅速学会基本的绘图。

> 目前，EGE图形库已经完美支持VC6, VC2005, VC2008, VC2010, C-Free等IDE，且对于MingGW环境的支持较好。

  * [讨论区](http://easyx.uueasy.com/)
  * [贴吧](http://tieba.baidu.com/f?kw=ege)
  * [一些文档](http://tcgraphics.svn.sourceforge.net/viewvc/tcgraphics/trunk/man/index.htm)
  * [misakamm's Blog 作者博客](http://blog.misakamm.org/)

### 为什么要写这个库？ ###

> 许多学编程的都是从 C 语言开始入门的，而目前的现状是

  1. 有些学校以 Turbo C 为环境讲 C 语言，只是 Turbo C 的环境实在太老了，复制粘贴都很不方便。
  1. 有些学校直接拿 VC 来讲 C 语言，因为 VC 的编辑和调试环境都很优秀，并且 VC 有适合教学的免费版本。可惜在 VC 下只能做一些文字性的练习题，想画条直线画个圆都很难，还要注册窗口类、建消息循环等等，初学者会受严重打击的。初学编程想要绘图就得用 TC，很是无奈。
  1. 还有计算机图形学，这门课程的重点是绘图算法，而不是 Windows 编程。所以，许多老师不得不用 TC 教学，因为 Windows 绘图太复杂了，会偏离教学的重点。新的图形学的书有不少是用的 OpenGL，可是门槛依然很高。

> 如果您刚开始学 C 语言，或者您是一位教C语言的老师，再或者您在教计算机图形学，那么这个库一定会让您兴奋的。采用EGE图形库，您将可以在VC的环境中方便的用类似TC的方法处理和生成图像。

### 本图形库的优点 ###

  * 绘图效率较好，特别在批量绘图模式下，640\*480的半透明混合，可以直接使用 getpixel / putpixel 完成，
    * 并且可以在大约1.5G CPU台式机器上达到60fps（要优化，否则一般的家用机再强也不行）
  * 灵活性更强，绘图可以直接针对一个IMAGE，不必只能画在屏幕上
  * 功能更多，支持拉伸贴图，支持透明半透明贴图，支持图像模糊滤镜操作，
    * 可以用对话框函数进行图形化的输入
  * 面向动画编程和游戏编程做了功能增强，可以方便地对帧率进行准确的控制
  * 附带简单的3D矢量运算函数和类，便于3D计算
  * 支持读写多种格式图片，支持读取bmp, jpg, png, gif，支持保存为bmp和png
  * 支持GUI模式编程

### 简要安装说明 ###

> 把include/graphics.h文件，复制到你的编译器安装目录下的include目录内

> 再把lib目录下的文件，复制到你的编译器安装目录下的lib目录内，具体编译器所依赖的文件情况

  * VC6: graphics.lib
  * VS2008: graphics08.lib graphics08d.lib
  * VS2010: graphics08.lib graphics10d.lib
  * MinGW: libgraphics.a

  * MSYS 中编译要点
    * g++ yourfile.cpp -lgraphics -lgdi32 -limm32 -lole32 -loleaut32 -lwinmm -luuid -mwindows
    * 其中yourfile.cpp是你要编译的cpp文件

  * C\_FREE 链接库设置
    * `菜单->构建->构建选项` 连接选项卡里添加
    * `graphics, gdi32, imm32, ole32, oleaut32, winmm, uuid 共7个`
    * ![http://cdupload.com/files/168069_f17h1/%E6%9C%AA%E5%91%BD%E5%90%8D.jpg](http://cdupload.com/files/168069_f17h1/%E6%9C%AA%E5%91%BD%E5%90%8D.jpg)
    * 此外，C-Free比较特殊的一点是，如果需要编译为Win32应用程序，那么要用`WinMain`来声明你的主函数，如
```
#include "graphics.h"
// 这里在graphics.h里已经定义了宏自动把它展开成合法的声明
// 以减免声明的麻烦，同时用来欺骗C-Free
int WinMain()
{
    /* ----------------------------
     * 1024 x 768 下 800 x 600 窗口
     * ----------------------------
     * setinitmode (0, 220, 142);
     * initgraph(800, 600);
     * ----------------------------
     * 1024 x 768 下 970 x 712 窗口
     * ----------------------------
     * setinitmode (0, 50, 30);
     * initgraph (970, 712);
     * ----------------------------
     */

    setinitmode (0, 220, 142);
    initgraph(800, 600);

    getch();

    closegraph();
    return 0;
}
```
    * 又或者，如果你不喜欢这样，那就在链接选项里（即刚刚截图里的参数框里）手工加上-mwindows也可

### 简要使用说明 ###

> 目前模拟了绝大多数 BGI 的绘图函数。使用上，基本和 TC / BC 没太大区别

> 看一个画圆的例子吧

```
// 引用ege图形库
#include "graphics.h"

int WinMain()
{
    // 初始化，显示一个窗口，这里和 TC 略有区别
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    // 画圆，圆心(200, 200)，半径 100
    circle(200, 200, 100);

    // 暂停一下等待用户按键
    getch();

    // 关闭图形界面
    closegraph();
    return 0;
}
```

> 呵呵，很简单吧。

## 库函数 ##

  * 控制台窗口显隐
    * VC6 默认隐藏，需要显示的话输入
```
#define SHOW_CONSOLE
```
    * C\_FREE 需要将主函数名由 `main()` 改为 `WinMain()`
  * EGE 开场动画的隐藏
    * 在 `initgraph()` 前调用
```
setinitmode (0)
```
    * 也可定义窗口左上角坐标，如
```
setinitmode (0, 50, 30)
```

### 绘图环境相关函数 ###

|cleardevice       |清除屏幕|
|:-----------------|:-----------|
|clearviewport     |清空视图|
|closegraph        |关闭图形环境|
|getviewport       |获取当前视图信息|
|initgraph         |初始化绘图环境|
|setactivepage     |设置当前绘图页|
|setinitmode       |设置初始化参数|
|setviewport       |设置当前视图|
|setvisualpage     |设置显示页，把页面内容输出到窗口的页|
|window getviewport|获取当前窗口可见部分|
|window setviewport|设置窗口可见部分|
|`WindowLock`  |切换到锁定窗口更新模式|
|`WindowFlush` |锁定模式下强制更新窗口|
|`WindowUnlock`|切换到自动更新模式|

#### cleardevice ####

  * 功能
    * 这个函数用于清除画面内容
    * 具体的，是用当前背景色清空画面
  * 声明
```
void cleardevice (
    PIMAGE pimg = NULL
);
```
  * 参数
    * pimg
      * 制定要清除的IMAGE，可选参数
      * 如果不填本参数，则清空屏幕

  * 返回值 无
  * 示例
```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    circle (200, 200, 100);
    getch();
    cleardevice();
    getch();
    closegraph();
    return 0;
}
```

#### clearviewport ####

  * 功能
    * 这个函数用于清空视图
    * 相当于对视图区进行 cleardevice
  * 声明
```
void clearviewport (
    PIMAGE pimg = NULL
);
```
  * 参数
    * pimg
      * 见 setviewport
  * 返回值 无
  * 示例 无

#### closegraph ####

  * 功能 这个函数用于关闭环境
  * 声明
```
void closegraph();
```
  * 参数 无
  * 返回值 无
  * 示例
```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    circle(200, 200, 100);
    getch();
    cleardevice();
    getch();
    closegraph();
    return 0;
}
```

#### getviewport ####

  * 功能 这个函数用于获取当前视图信息
  * 声明
```
void getviewport(
    int *pleft,
    int *ptop,
    int *pright,
    int *pbottom,
    int *pclip = NULL,
    PIMAGE pimg = NULL
);
```
  * 参数
    * pleft 返回当前视图的左部 x 坐标
    * ptop 返回当前视图的上部 y 坐标
    * pright 返回当前视图的右部 x 坐标
    * pbottom 返回当前视图的下部 y 坐标
    * pclip 返回当前视图的裁剪标志
    * pimg 详见 setviewport 的说明
  * 返回值 无
  * 示例 参见 setviewport

#### initgraph ####

  * 功能 这个函数用于初始化绘图环境
  * 声明
```
void initgraph(
    int Width,
    int Height,
    int Flag = INIT_DEFAULT
);

// 兼容 Borland C++ 3.1 的重载，不建议使用
void initgraph(
    int* gdriver,
    int* gmode,
    char* path
);
```
  * 参数
    * Width 绘图环境宽度。如果为-1，则使用屏幕宽度
    * Height 绘图环境高度。如果为-1，则使用屏幕高度
    * Style 请留空，为保留参数
  * 返回值 无
  * 示例
```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    circle(200, 200, 100);
    getch();
    cleardevice();
    getch();
    closegraph();
    return 0;
}
```

#### setactivepage ####

  * 功能 这个函数用于设置当前绘图页
  * 声明
```
void setactivepage (
    int page
);
```
  * 参数
    * page 绘图页，范围从0-3，越界会导致程序错误。默认值为0
  * 返回值 无
  * 示例 无

#### setinitmode ####

  * 功能 这个函数用于设置初始化图形的选项和模式
  * 声明
```
void setinitmode (
    int mode,
    int x = CW_USEDEFAULT,
    int y = CW_USEDEFAULT
);
```
  * 参数
    * mode
      * 初始化模式，是二进制组合的值
      * 如果为 INIT\_DEFAULT 表示使用默认值
      * 可以使用的值的组合
        * INIT\_NOBORDER 为无边框窗口
        * INIT\_CHILD 为子窗口（需要使用attachHWND制定要依附的父窗口，此函数不另说明）
        * INIT\_TOPMOST 使窗口总在最前
        * INIT\_WITHLOGO 使initgraph的时候显示开场动画
    * x, y
      * 初始化时窗口左上角在屏幕的坐标，默认为系统分配
  * 返回值 无
  * 说明 本函数只能在 initgraph 前调用
  * 示例

#### setviewport ####

  * 功能 这个函数用于设置当前视图。并且，将坐标原点移动到新的视图的 (0, 0) 位置
  * 声明
```
void setviewport(
    int left,
    int top,
    int right,
    int bottom,
    int clip = 1,
    PIMAGE pimg = NULL
);
```
  * 参数
    * left 视图的左部 x 坐标
    * top 视图的上部 y 坐标
      * (left, top) 将成为新的原点
    * right 视图的右部 x 坐标
    * bottom 视图的下部 y 坐标
      * (right-1, bottom-1) 是视图的右下角坐标
    * clip 视图的裁剪标志。如果为真，所有超出视图区域的绘图都会被裁剪掉。
    * pimg 要设置的图片
  * 返回值 无
  * 示例
```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setviewport(100, 100, 200, 200);
    rectangle(0, 0, 200, 200);
    getch();
    closegraph();
    return 0;
}
```

  * 注意：
> > 右端点和下端点取不到，上端点和左端点能取到


> 另外，这函数的最后一个参数为一个IMAGE\*的指针，是一个可选参数，如果不填，则设置到当前页。

> 如果填上，则设置到指定的IMAGE。

#### setvisualpage ####

  * 功能 这个函数用于设置当前显示页，显示页是输出到窗口的页
  * 声明
```
void setvisualpage(
    int page
);
```
  * 参数
    * page 绘图页，范围从，范围从0-3，越界会导致程序错误。默认值为0
  * 返回值 无
  * 示例 无

#### window getviewport ####

  * 功能 这个函数用于获取当前窗口可见区域
  * 声明
```
void window_getviewport(
    int *pleft,
    int *ptop,
    int *pright,
    int *pbottom,
);
```
  * 参数
    * pleft 返回当前视图的左部 x 坐标
    * ptop 返回当前视图的上部 y 坐标
    * pright 返回当前视图的右部 x 坐标
    * pbottom 返回当前视图的下部 y 坐标
  * 返回值 无
  * 示例 无

#### window setviewport ####

  * 功能 这个函数用于设置当前窗口可见区域
  * 声明
```
void window_setviewport(
    int left,
    int top,
    int right,
    int bottom
);
```
  * 参数
    * left 可见区域的左部 x 坐标
    * top 可见区域的上部 y 坐标
      * (left, top) 将成为新的原点
    * right 可见区域的右部 x 坐标
    * bottom 可见区域的下部 y 坐标
      * (right-1, bottom-1) 是视图的右下角坐标
  * 返回值 无
  * 示例
```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    window_setviewport(100, 100, 400, 400);
    rectangle(0, 0, 200, 200);
    getch();
    closegraph();
    return 0;
}
```

#### `WindowLock` ####

  * 功能 这个函数用于启用锁定窗口模式，禁止自动更新。
> > 执行后，任何绘图操作都将暂时不输出到屏幕上，直到执行
> > `delay/dealy_ms/delay_fps/delay_jfps/WindowFlush/getch/GetMouseMsg`
> > 函数时才更新窗口
> > （其中getch和`GetMouseMsg`仅当无消息时才更新屏幕并等待）。
> > 默认为自动更新模式，但建议使用本函数切换到锁定模式。
  * 声明
```
void WindowLock();
```
  * 参数 无
  * 返回值 无
  * 示例
> > 以下代码实现一个圆从左向右移动，会有比较明显的闪烁
> > 请取消 main 函数中的注释，以实现锁定模式绘图功能，可以消除闪烁，并且提升绘图效率

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    setcolor (WHITE);
    setfillstyle (RED);

    // WindowLock();
    for (int i=50; i<600; i++)
    {
        cleardevice();
        circle (i,100,40);
        floodfill (i, 100, WHITE);
        delay(5);
    }

    getch();
    closegraph();
    return 0;
}
```

#### `WindowFlush` ####

  * 功能 这个函数用于更新窗口，与delay(0)效果一样，仅工作在锁定更新模式
  * 声明
```
void WindowFlush();
```
  * 参数 无
  * 返回值 无
  * 示例 无

#### `WindowUnlock` ####

  * 功能 这个函数用于退出锁定更新模式，回到自动更新模式
> > 不需要和`WindowLock`函数配对使用
  * 声明
```
void WindowUnlock();
```
  * 参数 无
  * 返回值 无
  * 示例 无

### 颜色表示及相关函数 ###

|颜色表示      |介绍颜色表示方法|
|:-----------------|:-----------------------|
|getbkcolor    |获取当前绘图背景色|
|GetBValue     |返回指定颜色中的蓝色值|
|getcolor      |获取当前绘图前景色|
|GetGValue     |返回指定颜色中的绿色值|
|GetRValue     |返回指定颜色中的蓝色值|
|HSLtoRGB      |转换 HSL 颜色为 RGB 颜色|
|HSVtoRGB      |转换 HSV 颜色为 RGB 颜色|
|RGB           |通过红、绿、蓝颜色分量合成颜色|
|RGBtoGRAY     |转换 RGB 颜色为 灰度颜色|
|RGBtoHSL      |转换 RGB 颜色为 HSL 颜色|
|RGBtoHSV      |转换 RGB 颜色为 HSV 颜色|
|setbkcolor    |设置当前绘图背景色|
|setbkcolor\_f  |设置清屏时所用的背景色|
|setbkmode     |设置输出文字时的背景模式|
|setcolor      |设置当前绘图前景色|
|setfontbkcolor|设置当前文字背景色|


> 特殊说明：
> 这里部分函数的最后一个参数为一个PIMAGE的参数，是一个可选参数
    * 如果不填，则绘画到当前页
    * 如果填上，则设置或者绘画到指定的IMAGE

#### 颜色表示 ####

> 设置绘图色有以下几种办法

  * 用 16 进制的颜色表示，形式为
> > `0xbbggrr (bb=蓝，gg=绿, rr=红)`
  * 用预定义颜色

|BLACK         |`0x000000`    |黑    |
|:-------------|:-------------|:------|
|DARKGRAY      |`0x545454`    |深灰  |
|LIGHTGRAY     |`0xA8A8A8`    |浅灰  |
|WHITE         |`0XFCFCFC`    |白    |
|RED           |`0x0000A8`    |红    |
|LIGHTRED      |`0x5454FC`    |亮红  |
|BLUE          |`0xA80000`    |蓝    |
|LIGHTBLUE     |`0xFC5454`    |亮蓝  |
|GREEN         |`0x00A800`    |绿    |
|LIGHTGREEN    |`0x54FC54`    |亮绿  |
|CYAN          |`0xA8A800`    |青    |
|LIGHTCYAN     |`0xA8A8A8`    |亮青  |
|MAGENTA       |`0xA800A8`    |紫    |
|LIGHTMAGENTA  |`0xFC54FC`    |亮紫  |
|YELLOW        |`0x54FCFC`    |黄    |
|BROWN         |`0x0054A8`    |棕    |

  * 用 RGB 宏合成颜色
    * 详见 RGB

  * 用 HSLtoRGB HSVtoRGB 转换其他色彩模型到 RGB 颜色
    * 详见 HSLtoRGB HSVtoRGB

  * 示例 以下是部分设置前景色的方法
```
setcolor(0xff0000);
setcolor(BLUE);
setcolor(RGB(0, 0, 255));
setcolor(HSLtoRGB(240, 1, 0.5));
```

#### getbkcolor ####

  * 功能 这个函数用于获取当前绘图背景色
  * 声明
```
COLORREF getbkcolor(
    PIMAGE pimg = NULL
);
```
  * 参数 无
  * 返回值 返回当前绘图背景色
  * 示例 无

#### GetBValue ####

  * 功能 `GetBValue` 宏用于返回指定颜色中的蓝色值
  * 声明
```
BYTE GetBValue(
    COLORREF rgb
);
```
  * 参数
    * rgb 指定的颜色
  * 返回值 指定颜色中的蓝色值，值的范围 0~255
  * 示例 无
  * 注 `GetBValue` 宏在 Windows SDK 中定义

#### getcolor ####

  * 功能 这个函数用于获取当前绘图前景色
  * 声明
```
COLORREF getcolor(
    PIMAGE pimg = NULL
);
```
  * 参数 无
  * 返回值 返回当前绘图前景色
  * 示例 无

#### GetGValue ####

  * 功能 `GetGValue` 宏用于返回指定颜色中的绿色值
  * 声明
```
BYTE GetGValue(
    COLORREF rgb
);
```
  * 参数
    * rgb 指定的颜色
  * 返回值 指定颜色中的绿色值，值的范围 0~255
  * 示例 无
  * 注 `GetGValue` 宏在 Windows SDK 中定义

#### GetRValue ####

  * 功能 `GetRValue` 宏用于返回指定颜色中的红色值
  * 声明
```
BYTE GetRValue(
    COLORREF rgb
);
```
  * 参数
    * rgb 指定的颜色
  * 返回值 指定颜色中的红色值，值的范围 0~255
  * 示例 无
  * 注 `GetRValue` 宏在 Windows SDK 中定义

#### HSLtoRGB ####

  * 功能 该函数用于转换 HSL 颜色为 RGB 颜色
  * 声明
```
COLORREF HSLtoRGB(
    float H,
    float S,
    float L
);
```
  * 参数
    * H 原 HSL 颜色模型的 Hue(色相) 分量
      * 0 ≤ H ＜ 360
    * S 原 HSL 颜色模型的 Saturation(饱和度) 分量
      * 0 ≤ S ≤ 1
    * L 原 HSL 颜色模型的 Lightness(亮度) 分量
      * 0 ≤ L ≤ 1
  * 返回值 对应的 RGB 颜色
  * 说明 HSL 又称 HLS。
    * H 是英文 Hue 的首字母，表示色相，即组成可见光谱的单色
> > > 红色在 0 度，绿色在 120 度，蓝色在 240 度，以此方向过渡
    * S 是英文 Saturation 的首字母，表示饱和度
> > > 等于 0 时为灰色。在最大饱和度 1 时，具有最纯的色光
    * L 是英文 Lightness 的首字母，表示亮度
> > > 等于 0 时为黑色，等于 0.5 时是色彩最鲜明的状态，等于 1 时为白色
  * 示例 请参见示例程序中的“彩虹”

#### HSVtoRGB ####

  * 功能 该函数用于转换 HSV 颜色为 RGB 颜色
  * 声明
```
COLORREF HSVtoRGB(
    float H,
    float S,
    float V
);
```
  * 参数
    * H 原 HSL 颜色模型的 Hue(色相) 分量
      * 0 ≤ H ＜ 360
    * S 原 HSL 颜色模型的 Saturation(饱和度) 分量
      * 0 ≤ S ≤ 1
    * V 原 HSL 颜色模型的 Value(明度) 分量
      * 0 ≤ L ≤ 1
  * 返回值 对应的 RGB 颜色
  * 说明 HSV 又称 HSB
    * H 是英文 Hue 的首字母，表示色相，即组成可见光谱的单色
> > > 红色在 0 度，绿色在 120 度，蓝色在 240 度，以此方向过渡
    * S 是英文 Saturation 的首字母，表示饱和度
> > > 等于 0 时为灰色。在最大饱和度 1 时，每一色相具有最纯的色光
    * V 是英文 Value 的首字母，表示明度
> > > 等于 0 时为黑色，在最大明度 1 时，是色彩最鲜明的状态
  * 示例 HSV 颜色模型类似于 HSL，示例程序中的“彩虹”是 HSL 模型的操作范例，可以参考

#### RGB ####

  * 功能 RGB 宏用于通过红、绿、蓝颜色分量合成颜色
  * 声明
```
COLORREF RGB(
    BYTE byRed,     // 颜色的红色部分
    BYTE byGreen,   // 颜色的绿色部分
    BYTE byBlue     // 颜色的蓝色部分
);
```
  * 参数
    * byRed 颜色的红色部分，取值范围：0~255
    * byGreen 颜色的绿色部分，取值范围：0~255
    * byBlue 颜色的蓝色部分，取值范围：0~255
  * 返回值 返回合成的颜色
  * 说明
    * 可以通过 GetRValue、GetGValue、GetBValue 宏从颜色中分离出红、绿、蓝颜色分量
    * 详见 GetRValue、GetGValue、GetBValue
  * 示例 无
  * RGB 宏在 Windows SDK 中定义

#### RGBtoGRAY ####

  * 功能 该函数用于返回与指定颜色对应的灰度值颜色
  * 声明
```
COLORREF RGBtoGRAY(
    COLORREF rgb
);
```
  * 参数
    * rgb 原 RGB 颜色
  * 返回值 对应的灰度颜色
  * 示例 无

#### RGBtoHSL ####

  * 功能 该函数用于转换 RGB 颜色为 HSL 颜色
  * 声明
```
void RGBtoHSL(
    COLORREF rgb,
    float *H,
    float *S,
    float *L
);
```
  * 参数
    * rgb 原 RGB 颜色
    * H 原 HSL 颜色模型的 Hue(色相) 分量
      * 0 ≤ H ＜ 360
    * S 原 HSL 颜色模型的 Saturation(饱和度) 分量
      * 0 ≤ S ≤ 1
    * L 原 HSL 颜色模型的 Lightness(亮度) 分量
      * 0 ≤ L ≤ 1
  * 返回值 无
  * 说明 HSL 详见 HSLtoRGB
  * 示例 无

#### RGBtoHSV ####

  * 功能 该函数用于转换 RGB 颜色为 HSV 颜色
  * 声明
```
void RGBtoHSV(
    COLORREF rgb,
    float *H,
    float *S,
    float *V
);
```
  * 参数
    * rgb 原 RGB 颜色
    * H 原 HSL 颜色模型的 Hue(色相) 分量
      * 0 ≤ H ＜ 360
    * S 原 HSL 颜色模型的 Saturation(饱和度) 分量
      * 0 ≤ S ≤ 1
    * V 原 HSL 颜色模型的 Value(明度) 分量
      * 0 ≤ L ≤ 1
  * 返回值 无
  * 说明 HSV 详见 HSVtoRGB
  * 示例 无

#### setbkcolor ####

  * 功能 这个函数用于设置当前背景色

> > 并且会把当前图片上是原背景色的像素，转变为新的背景色
  * 声明
```
void setbkcolor(
    COLORREF color,
    PIMAGE pimg = NULL
);
```
  * 参数
    * color 指定要设置的背景颜色
> > > 注意，该设置会同时影响文字背景色
  * 返回值 无
  * 示例 无

#### setbkcolor\_f ####

  * 功能 这个函数用于设置当前背景色

> > 即仅设置cleardevice时所使用的颜色，不立即生效，需要等cleardevice调用
  * 声明
```
void setbkcolor(
    COLORREF color,
    PIMAGE pimg = NULL
);
```
  * 参数
    * color 指定要设置的背景颜色
> > > 注意，该设置会同时影响文字背景色
  * 返回值 无
  * 示例 无

#### setbkmode ####

  * 功能 这个函数用于设置输出文字时的背景模式
  * 声明
```
void setbkmode(
    int iBkMode,
    PIMAGE pimg = NULL
);
```
  * 参数
    * iBkMode 指定输出文字时的背景模式 可以是以下值

|OPAQUE        |背景用当前背景色填充（默认）|
|:-------------|:-----------------------------------------|
|TRANSPARENT   |背景是透明的|

  * 返回值 无
  * 示例 无

#### setcolor ####

  * 功能 这个函数用于设置绘图前景色
  * 声明
```
void setcolor(
    COLORREF color,
    PIMAGE pimg = NULL
);
```
  * 参数
    * color 要设置的前景颜色
  * 返回值 无
  * 示例 无

#### setfontbkcolor ####

  * 功能 这个函数用于设置文字背景色
  * 声明
```
void setfontbkcolor(
    COLORREF color,
    PIMAGE pimg = NULL
);
```
  * 参数
    * color 要设置的文字背景颜色
  * 返回值 无
  * 示例 无

### 绘制图形相关函数 ###

|arc           |画圆弧|
|:-------------|:--------|
|bar           |画无边框填充矩形|
|bar3d         |画有边框三维填充矩形|
|circle        |画圆|
|drawbezier    |画bezier曲线|
|drawlines     |画多条不连续线段|
|drawpoly      |画多边形|
|ellipse       |画椭圆弧线|
|fillellipse   |画填充的椭圆|
|fillpoly      |画填充的多边形|
|floodfill     |填充区域|
|getfillcolor  |获取当前填充颜色|
|getfillstyle  |获取当前填充类型（暂不支持）|
|getheight     |获取绘图区的高度|
|getlinestyle  |获取当前线形|
|getpixel      |获取像素点的颜色|
|getwidth      |获取绘图区的宽度|
|getx          |获取当前 x 坐标|
|gety          |获取当前 y 坐标|
|line          |画线|
|linerel       |画线|
|lineto        |画线|
|moverel       |移动当前点|
|moveto        |移动当前点|
|pieslice      |画填充圆扇形|
|putpixel      |画像素点|
|putpixels     |画多个像素点|
|rectangle     |画空心矩形|
|sector        |画填充椭圆扇形|
|setfillcolor  |设置当前填充颜色|
|setfillstyle  |设置当前填充类型|
|setlinestyle  |设置当前线形|
|setwritemode  |设置绘图位操作模式|

特殊说明：


> 以下所有函数的坐标模式为，如果以有向线段表示的量，起点能取到，终点取不到。比如line函数，起点x1,y1能画上点，终点x2,y2不会画上点，请注意。类似的有lineto, linerel, bar, bar3d, rectangle, ellipse, sector，函数说明内也会对本段进行补充。

> 另外，这里每一个函数的最后一个参数均为一个PIMAGE的指针，是一个可选参数，如果不填，则绘画到当前页。如果填上，则绘画到指定的IMAGE。

> 关于效率，如果使用窗口锁定模式（`WindowLock`），那以上所有函数的执行速度都会得到提升。不过，`WindowLock`函数的执行需要花费较多时间（几十毫秒），建议如果需要，那请全局开启，不要局部使用，就是说最好在初始化，或者对时间效率不敏感的地方调用。

#### arc ####

  * 功能 这个函数用于画圆弧。边线颜色由setcolor函数决定
  * 声明
```
void arc(
    int x,
    int y,
    int stangle,
    int endangle,
    int radius,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 圆弧的圆心 x 坐标。
    * y 圆弧的圆心 y 坐标。
    * stangle 圆弧的起始角的角度。
    * endangle 圆弧的终止角的角度。
    * radius 圆弧的半径。
  * 返回值 无
  * 示例 无

#### bar ####

  * 功能 这个函数用于画无边框填充矩形
> > 其中，填充颜色由setfillstyle函数决定
  * 声明
```
void bar(
    int left,
    int top,
    int right,
    int bottom,
    PIMAGE pimg = NULL
);
```
  * 参数
    * left 矩形左部 x 坐标
    * top 矩形上部 y 坐标
    * right 矩形右部 x 坐标
> > > （该点取不到，实际右边界为right-1）
    * bottom 矩形下部 y 坐标
> > > （该点取不到，实际下边界为bottom-1）
  * 返回值 无
  * 示例 无

#### bar3d ####

  * 功能 这个函数用于画有边框三维填充矩形

> > 其中，填充颜色由setfillstyle函数决定
  * 声明
```
void bar3d(
    int left,
    int top,
    int right,
    int bottom,
    int depth,
    bool topflag,
    PIMAGE pimg = NULL
);
```
  * 参数
    * left 矩形左部 x 坐标
    * top 矩形上部 y 坐标
    * right 矩形右部 x 坐标
> > > （该点取不到，实际右边界为right-1）
    * bottom 矩形下部 y 坐标
> > > （该点取不到，实际下边界为bottom-1）
    * depth 矩形深度
    * topflag 为 false 时，将不画矩形的三维顶部
> > > 该选项可用来画堆叠的三维矩形
  * 返回值 无
  * 示例
```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    setfillstyle(RED);
    bar3d(100, 100, 150, 150, 20, 1);
    getch();
    return 0;
}
```

#### circle ####

  * 功能 这个函数用于画圆

> > 此圆是空心的，不填充，而边线颜色由setcolor函数决定
  * 声明
```
void circle(
    int x,
    int y,
    int radius,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 圆的圆心 x 坐标
    * y 圆的圆心 y 坐标
    * radius 圆的半径
  * 返回值 无
  * 示例 无

#### drawbezier ####

  * 功能 这个函数用于画贝塞尔曲线
> > 边线颜色由setcolor函数决定
  * 声明
```
void drawbezier(
    int numpoints,
    const int *polypoints,
    PIMAGE pimg = NULL
);
```
  * 参数
    * numpoints 多边形点的个数
> > > 需要是被3除余1的数
> > > 如果不是，则忽略最后面若干个点
    * polypoints 每个点的坐标（依次两个分别为x,y）
> > > 数组元素个数为 `numpoints * 2`
    * 每一条bezier曲线由两个端点和两个控制点组成
    * 相邻两条则共用端点
  * 返回值 无
  * 示例 无

#### drawlines ####

  * 功能 这个函数用于画多条线段

> > 边线颜色由setcolor函数决定
  * 声明
```
void drawlines(
    int numliness,
    const int *polypoints,
    PIMAGE pimg = NULL
);
```
  * 参数
    * numlines 线段数目
    * polypoints 每个点的坐标（依次两个分别为x,y）
> > > 数组元素个数为 `numlines * 4`
    * 每两个点画一线段
  * 返回值 无
  * 示例 无

#### drawpoly ####

  * 功能 这个函数用于画多边形

> > 边线颜色由setcolor函数决定
  * 声明
```
void drawpoly(
    int numliness,
    const int *polypoints,
    PIMAGE pimg = NULL
);
```
  * 参数
    * numpoints 多边形点的个数。
    * polypoints 每个点的坐标（依次两个分别为x,y）
> > > 数组元素个数为 `numpoints * 2`
    * 该函数并不会自动连接多边形首尾
> > > 如果需要画封闭的多边形，请将最后一个点设置为与第一点相同
  * 返回值 无
  * 示例 无

#### ellipse ####

  * 功能 这个函数用于画椭圆弧线

> > 边线颜色由setcolor函数决定
  * 声明
```
void ellipse(
    int x,
    int y,
    int stangle,
    int endangle,
    int xradius,
    int yradius,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 椭圆弧线的圆心 x 坐标
    * y 椭圆弧线的圆心 y 坐标
    * stangle 椭圆弧线的起始角的角度
    * endangle 椭圆弧线的终止角的角度
    * xradius 椭圆弧线的 x 轴半径
    * yradius 椭圆弧线的 y 轴半径
  * 返回值 无
  * 示例 无

#### fillellipse ####

  * 功能 这个函数用于画填充的椭圆
> > 边线颜色由setcolor函数决定
> > 填充颜色由setfillstyle函数决定
  * 声明
```
void fillellipse(
    int x,
    int y,
    int xradius,
    int yradius,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 椭圆的圆心 x 坐标
    * y 椭圆的圆心 y 坐标
    * xradius 椭圆的 x 轴半径
    * yradius 椭圆的 y 轴半径
  * 返回值 无
  * 示例 无

#### fillpoly ####

  * 功能 这个函数用于画填充的多边形
> > 边线颜色由setcolor函数决定
> > 填充颜色由setfillstyle函数决定
  * 声明
```
void fillpoly(
    int numpoints,
    const int *polypoints,
    PIMAGE pimg = NULL
);
```
  * 参数
    * numpoints 多边形点的个数
    * polypoints 每个点的坐标
> > > 数组元素个数为 `numpoints * 2`
    * 该函数会自动连接多边形首尾
  * 返回值 无
  * 示例 无
  * 说明
    * 如果这个多边形发生自相交，那么自交次数为奇数的区域则不填充，偶数次的填充，不自交就是偶数次

> > 不过这样说明相信非常难理解，以下给个例子：
```
#include "graphics.h"
int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    setfillstyle(RED);
    int pt[] = {
        0,   0,
        100, 0,
        100, 100,
        10,  10,
        90,  10,
        0,   100,
    };
    fillpoly(6, pt);
    getch();
    return 0;
}
```
> > 第二个例子
```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    setfillstyle(RED);
    int pt[] = {
        0,   0,
        100, 0,
        100, 100,
        0,   100,
        0,   0,
        100, 0,
        100, 120,
        0,   100,
    };
    fillpoly(8, pt);
    getch();
    return 0;
}
```

#### floodfill ####

  * 功能 这个函数使用setfillstyle设置的填充方式对区域进行填充
> > 填充颜色由setfillstyle函数决定
  * 声明
```
void floodfill(
    int x,
    int y,
    int border,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 填充的起始点 x 坐标
    * y 填充的起始点 y 坐标
    * border 填充的边界颜色
> > > 填充动作在该颜色围成的区域内填充
> > > 如果该颜色围成的区域不封闭，那么将使全屏幕都填充上
  * 返回值 无
  * 示例 无

#### getfillcolor ####

  * 功能 这个函数用于设置当前填充颜色
  * 声明
```
COLORREF getfillcolor(
    IMAGE* pimg = NULL
);
```
  * 参数 无
  * 返回值 当前的填充颜色
  * 示例 无

#### getfillstyle ####

  * 功能 这个函数用于设置当前线形
  * 声明
```
void setlinestyle(
    int linestyle,
    WORD upattern = NULL,
    int thickness = 1,
    PIMAGE pimg = NULL
);
```
  * 参数
    * linestyle 线型，可以是以下值
  * 返回值
  * 示例

#### getheight ####

  * 功能 这个函数用于获取图片高度
  * 声明
```
int getheight(
    PIMAGE pimg = NULL
);
```
  * 参数 无
  * 返回值 返回图片高度
  * 示例 无

#### getlinestyle ####

  * 功能 这个函数用于获取当前线形
  * 声明
```
void getlinestyle(
    int  *plinestyle,
    WORD *pupattern = NULL,
    int  *pthickness = NULL,
    PIMAGE pimg = NULL
);
```
  * 参数
    * plinestyle 返回当前线型
> > > 详见 setlinestyle
    * pupattern 返回当前自定义线形数据
    * pthickness 返回当前线形宽度
  * 返回值 无
  * 示例 无

#### getpixel ####

  * 功能 这个函数用于获取像素点的颜色
  * 声明
```
COLORREF getpixel(
    int x,
    int y
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 要获取颜色的 x 坐标
    * y 要获取颜色的 y 坐标
  * 返回值 指定点的颜色
  * 示例 无
  * 说明

> > 另有高速版的getpixel\_f函数，参数一样，作用一样，但不进行相对坐标变换和边界检查
> > （如果越界绘图，要么画错地方，要么程序结果莫名其妙，甚至直接崩溃）
> > 并且必须在批量绘图模式下才能使用，否则将发生不可预知的结果

#### getwidth ####

  * 功能 这个函数用于获取图片宽度
  * 声明
```
int getwidth(
    PIMAGE pimg = NULL
);
```
  * 参数 无
  * 返回值 返回图片宽度
  * 示例 无

#### getx ####

  * 功能 这个函数用于获取当前 x 坐标
  * 声明
```
int getx(
    PIMAGE pimg = NULL
);
```
  * 参数 无
  * 返回值 返回当前 x 坐标
  * 示例 无

#### gety ####

  * 功能 这个函数用于获取当前 y 坐标
  * 声明
```
int gety(
    PIMAGE pimg = NULL
);
```
  * 参数 无
  * 返回值 返回当前 y 坐标
  * 示例 无

#### line ####

  * 功能 这个函数用于画线
  * 声明
```
void line(
    int x1,
    int y1,
    int x2,
    int y2,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x1 线的起始点的 x 坐标
    * y1 线的起始点的 y 坐标
    * x2 线的终止点的 x 坐标
> > > （该点本身画不到）
    * y2 线的终止点的 y 坐标
> > > （该点本身画不到）
  * 返回值 无
  * 示例 无
  * 说明

> > 另有高速版的line\_f函数，参数一样，作用一样，但不进行相对坐标变换和边界检查
> > （如果越界绘图，要么画错地方，要么程序结果莫名其妙，甚至直接崩溃）
> > 并且必须在批量绘图模式下才能使用，否则将发生不可预知的结果

#### linerel ####

  * 功能 这个函数用于画线
  * 声明
```
void linerel(
    int dx,
    int dy,
    PIMAGE pimg = NULL
);
```
  * 参数
    * dx 从“当前点”cx开始画线，沿 x 轴偏移 dx，终点为cx+dx
> > > （终点本身画不到）。
    * dy 从“当前点”cy开始画线，沿 y 轴偏移 dy，终点为cy+dy
> > > （终点本身画不到）。
  * 返回值 无
  * 示例 无
  * 说明

> > 另有高速版的linerel\_f函数，参数一样，作用一样，但不进行相对坐标变换和边界检查
> > （如果越界绘图，要么画错地方，要么程序结果莫名其妙，甚至直接崩溃）
> > 并且必须在批量绘图模式下才能使用，否则将发生不可预知的结果

#### lineto ####

  * 功能 这个函数用于画线
  * 声明
```
void lineto(
    int x,
    int y,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 从“当前点”开始画线，终点横坐标为 x
> > > （终点本身画不到）
    * y 从“当前点”开始画线，终点纵坐标为 y
> > > （终点本身画不到）
  * 返回值 无
  * 示例 无
  * 说明

> > 另有高速版的lineto\_f函数，参数一样，作用一样，但不进行相对坐标变换和边界检查
> > （如果越界绘图，要么画错地方，要么程序结果莫名其妙，甚至直接崩溃）
> > 并且必须在批量绘图模式下才能使用，否则将发生不可预知的结果

#### moverel ####

  * 功能 这个函数用于移动当前点
> > 有些绘图操作会从“当前点”开始，这个函数可以设置该点
  * 声明
```
void moverel(
    int dx,
    int dy,
    PIMAGE pimg = NULL
);
```
  * 参数
    * dx 将当前点沿 x 轴移动 dx
    * dy 将当前点沿 y 轴移动 dy
  * 返回值 无
  * 示例 无

#### moveto ####

  * 功能 这个函数用于移动当前点
> > 有些绘图操作会从“当前点”开始，这个函数可以设置该点
  * 声明
```
void moveto(
    int x,
    int y,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 新的当前点 x 坐标
    * y 新的当前点 y 坐标
  * 返回值 无
  * 示例 无

#### pieslice ####

  * 功能 这个函数用于画填充圆扇形
  * 声明
```
void pieslice(
    int x,
    int y,
    int stangle,
    int endangle,
    int radius,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 圆扇形的圆心 x 坐标
    * y 圆扇形的圆心 y 坐标
    * stangle 圆扇形的起始角的角度
    * endangle 圆扇形的终止角的角度
    * radius 圆扇形的半径
  * 返回值 无
  * 示例 无

#### putpixel ####

  * 功能 这个函数用于画点
  * 声明
```
void putpixel(
    int x,
    int y,
    COLORREF color,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 点的 x 坐标
    * y 点的 y 坐标
    * color 点的颜色
  * 返回值 无
  * 示例 无
  * 说明
> > 另有高速版的putpixel\_f函数，参数一样，作用一样，但不进行相对坐标变换和边界检查
> > （如果越界绘图，要么画错地方，要么程序结果莫名其妙，甚至直接崩溃）
> > 并且必须在批量绘图模式下才能使用，否则将发生不可预知的结果

#### putpixels ####

  * 功能 这个函数用于画多个点
  * 声明
```
void putpixels(
    int nPoint,
    int* pPoints,
    PIMAGE pimg = NULL
);
```
  * 参数
    * nPoint 点的数目
    * pPoints 指向点的描述的指针
> > > 一个int型的数组，依次每三个int描述一个点
> > > 第一个为x坐标，第二个为y坐标，第三个为颜色值
  * 返回值 无
  * 示例 无
  * 说明

> > 另有高速版的putpixels\_f函数，参数一样，作用一样，但不进行相对坐标变换和边界检查
> > （如果越界绘图，要么画错地方，要么程序结果莫名其妙，甚至直接崩溃）
> > 并且必须在批量绘图模式下才能使用，否则将发生不可预知的结果

#### rectangle ####

  * 功能 这个函数用于画空心矩形
  * 声明
```
void rectangle(
    int left,
    int top,
    int right,
    int bottom,
    PIMAGE pimg = NULL
);
```
  * 参数
    * left 矩形左部 x 坐标
    * top 矩形上部 y 坐标
    * right 矩形右部 x 坐标
    * bottom 矩形下部 y 坐标
  * 返回值 无
  * 示例 无

#### sector ####

  * 功能 这个函数用于画填充椭圆扇形
  * 声明
```
void sector(
    int x,
    int y,
    int stangle,
    int endangle,
    int xradius,
    int yradius,
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 椭圆扇形的圆心 x 坐标
    * y 椭圆扇形的圆心 y 坐标
    * stangle 椭圆扇形的起始角的角度
    * endangle 椭圆扇形的终止角的角度
    * xradius 椭圆扇形的 x 轴半径
    * yradius 椭圆扇形的 y 轴半径
  * 返回值 无
  * 示例 无

#### setfillcolor ####

  * 功能 这个函数用于设置当前填充颜色
  * 声明
```
void setfillcolor(
    COLORREF color,
    PIMAGE pimg = NULL
);
```
  * 参数
    * color 填充颜色
  * 返回值 无
  * 示例 设置蓝色固实填充
> > `setfillcolor(BLUE);`

#### setfillstyle ####

  * 功能 这个函数用于设置当前填充类型
> > 该函数的自定义填充部分尚不支持
  * 声明
```
void setfillstyle(
    COLORREF color,
    int pattern = SOLID_FILL,
    PIMAGE pimg = NULL
);
```
  * 参数
    * color 填充颜色
    * pattern 填充类型，可以是以下宏或值
> > > |NULL\_FILL   |1 |不填充    |
|:------------|:-|:------------|
> > > |SOLID\_FILL  |2 |固实填充  |
    * pupattern 指定图案填充时的样式，目前无作用
  * 返回值 指定图案填充时的样式，目前无作用
  * 示例 设置蓝色固实填充

> > `setfillstyle(BLUE);`

#### setlinestyle ####

  * 功能 这个函数用于设置当前线形
  * 声明
```
void setlinestyle(
    int linestyle,
    WORD upattern = NULL,
    int thickness = 1,
    PIMAGE pimg = NULL
);
```
  * 参数
    * linestyle 线型，可以是以下值
      * PS\_SOLID
        * 线形为实线
      * PS\_DASH
        * `－－－－－－－－－－－－`
      * PS\_DOT
        * `●●●●●●●●●●●●`
      * PS\_DASHDOT
        * `－●－●－●－●－●－●`
      * PS\_DASHDOTDOT
        * `－●●－●●－●●－●●`
      * PS\_NULL
        * 线行为不可见
      * PS\_USERSTYLE
        * 线形样式是自定义的，依赖于 upattern 参数
    * upattern 自定义线形数据
      * 自定义规则
> > > > 该数据为 WORD 类型，共 16 个二进制位，每位为 1 表示画线，为 0 表示空白。从低位到高位表示从起始到终止的方向。
> > > > 仅当线型为 PS\_USERSTYLE 时该参数有效。
  * 返回值 无
  * 示例
    * 设置线形为点划线

> > > `setlinestyle (PS_DASHDOT);`
    * 设置线形为宽度 3 像素的虚线
> > > `setlinestyle (PS_DASH, NULL, 3);`

#### setwritemode ####

  * 功能 这个函数用于设置绘图位操作模式
  * 声明
```
void setwritemode(
    int mode.
    PIMAGE pimg = NULL
);
```
  * 参数
    * mode 二元光栅操作码（即位操作模式）
> > > 支持全部的 16 种二元光栅操作码，罗列如下
|位操作模式    |描述|
|:------------------|:-----|
|R2\_BLACK      |绘制出的像素颜色 = 黑色|
|R2\_COPYPEN    |绘制出的像素颜色 = 当前颜色（默认）|
|R2\_MASKNOTPEN |绘制出的像素颜色 = 屏幕颜色 AND (NOT 当前颜色)|
|R2\_MASKPEN    |绘制出的像素颜色 = 屏幕颜色 AND 当前颜色|
|R2\_MASKPENNOT |绘制出的像素颜色 = (NOT 屏幕颜色) AND 当前颜色|
|R2\_MERGENOTPEN|绘制出的像素颜色 = 屏幕颜色 OR (NOT 当前颜色)|
|R2\_MERGEPEN   |绘制出的像素颜色 = 屏幕颜色 OR 当前颜色|
|R2\_MERGEPENNOT|绘制出的像素颜色 = (NOT 屏幕颜色) OR 当前颜色|
|R2\_NOP        |绘制出的像素颜色 = 屏幕颜色|
|R2\_NOT        |绘制出的像素颜色 = NOT 屏幕颜色|
|R2\_NOTCOPYPEN |绘制出的像素颜色 = NOT 当前颜色|
|R2\_NOTMASKPEN |绘制出的像素颜色 = NOT (屏幕颜色 AND 当前颜色)|
|R2\_NOTMERGEPEN|绘制出的像素颜色 = NOT (屏幕颜色 OR 当前颜色)|
|R2\_NOTXORPEN  |绘制出的像素颜色 = NOT (屏幕颜色 XOR 当前颜色)|
|R2\_WHITE      |绘制出的像素颜色 = 白色|
|R2\_XORPEN     |绘制出的像素颜色 = 屏幕颜色 XOR 当前颜色|

  * 注意
    1. AND / OR / NOT / XOR 为布尔位运算
    1. "屏幕颜色"指绘制所经过的屏幕像素点的颜色
    1. "当前颜色"是指通过 setcolor 设置的用于当前绘制的颜色
  * 返回值 无
  * 示例 无

### 文字输出相关函数 ###

|getfont       |获取当前字体样式|
|:-------------|:-----------------------|
|LOGFONT 结构体|保存字体样式的结构体|
|outtext       |在当前位置输出字符串|
|outtextrect   |在指定矩形区域内输出字符串|
|outtextxy     |在指定位置输出字符串|
|setfont       |设置当前字体样式|
|settextjustify|设置当前文字对齐方式|
|textheight    |获取字符串的高|
|textwidth     |获取字符串的宽|

特殊说明：这里部分函数的最后一个参数为一个PIMAGE的参数，是一个可选参数，如果不填，则绘画到当前页。如果填上，则设置或者绘画到指定的IMAGE

#### getfont ####

  * 功能 这个函数用于获取当前字体样式
  * 声明
```
void getfont(
    LOGFONT *font
    PIMAGE pimg = NULL
);
```
  * 参数
    * font 指向 LOGFONT 结构体的指针
  * 返回值 无
  * 示例 无

#### LOGFONT 结构体 ####

  * 功能 这个结构体定义了字体的属性
  * 声明
```
struct LOGFONT {
    LONG lfHeight;
    LONG lfWidth
    LONG lfEscapement;
    LONG lfOrientation;
    LONG lfWeight;
    BYTE lfItalic;
    BYTE lfUnderline;
    BYTE lfStrikeOut;
    BYTE lfCharSet;
    BYTE lfOutPrecision;
    BYTE lfClipPrecision;
    BYTE lfQuality;
    BYTE lfPitchAndFamily;
    TCHAR lfFaceName[LF_FACESIZE];
};
```
  * 成员
    * lfHeight 指定高度（逻辑单位）
      * 如果为正，表示指定的高度是字体的完整高度
      * 如果为负，表示指定的高度不包含 tmInternalLeading 的高度
      * 也就是说相同绝对值下，负的比正的会稍高一些
      * 而实际输出的字体高度，正数时精确匹配，负数时，和实际略有偏差，绝对值比实际的略小。
    * lfWidth 指定字符的平均宽度（逻辑单位）
      * 如果为 0，则比例自适应
    * lfEscapement 字符串的书写角度，单位 0.1 度，默认为 0
    * lfOrientation 每个字符的书写角度，单位 0.1 度，默认为 0
    * lfWeight 字符的笔画粗细，范围 0~1000，0 表示默认粗细
      * FW\_DONTCARE   0
      * FW\_THIN       100
      * FW\_EXTRALIGHT 200
      * FW\_ULTRALIGHT 200
      * FW\_LIGHT      300
      * FW\_NORMAL     400
      * FW\_REGULAR    400
      * FW\_MEDIUM     500
      * FW\_SEMIBOLD   600
      * FW\_DEMIBOLD   600
      * FW\_BOLD       700
      * FW\_EXTRABOLD  800
      * FW\_ULTRABOLD  800
      * FW\_HEAVY      900
      * FW\_BLACK      900
    * lfItalic 指定字体是否是斜体
    * lfUnderline 指定字体是否有下划线
    * lfStrikeOut 指定字体是否有删除线
    * lfCharSet 指定字符集。以下是预定义的值
      * ANSI\_CHARSET
      * BALTIC\_CHARSET
      * CHINESEBIG5\_CHARSET
      * DEFAULT\_CHARSET
        * 表示字符集基于本地操作系统
      * EASTEUROPE\_CHARSET
      * GB2312\_CHARSET
      * GREEK\_CHARSET
      * HANGUL\_CHARSET
      * MAC\_CHARSET
      * OEM\_CHARSET
        * 表示字符集依赖本地操作系统
      * RUSSIAN\_CHARSET
      * SHIFTJIS\_CHARSET
      * SYMBOL\_CHARSET
      * TURKISH\_CHARSET
      * 例如，系统位置是 English (United States),字符集将设置为 ANSI\_CHARSET
    * lfOutPrecision 指定文字的输出精度
> > > 输出精度定义输出与所请求的字体高度、宽度、字符方向、行距、间距和字体类型相匹配必须达到的匹配程度
      * OUT\_DEFAULT\_PRECIS
> > > > 指定默认的映射行为
      * OUT\_DEVICE\_PRECIS
> > > > 当系统包含多个名称相同的字体时，指定设备字体
      * OUT\_OUTLINE\_PRECIS
> > > > 指定字体映射选择 `TrueType` 和其它的 outline-based 字体。
      * OUT\_RASTER\_PRECIS
> > > > 当系统包含多个名称相同的字体时，指定光栅字体（即点阵字体）
      * OUT\_STRING\_PRECIS
> > > > 这个值并不能用于指定字体映射，只是指定点阵字体枚举数据
      * OUT\_STROKE\_PRECIS
> > > > 这个值并不能用于指定字体映射，只是指定 `TrueType` 和其他的 outline-based 字体，以及矢量字体的枚举数据
      * OUT\_TT\_ONLY\_PRECIS
> > > > 指定字体映射只选择 `TrueType` 字体。如果系统中没有安装 `TrueType` 字体，将选择默认操作
      * OUT\_TT\_PRECIS
> > > > 当系统包含多个名称相同的字体时，指定 `TrueType` 字体
    * lfClipPrecision 指定文字的剪辑精度

> > > 剪辑精度定义如何剪辑字符的一部分位于剪辑区域之外的字符
      * CLIP\_DEFAULT\_PRECIS
> > > > 指定默认的剪辑行为
      * CLIP\_STROKE\_PRECIS
> > > > 这个值并不能用于指定字体映射，只是指定光栅（即点阵）、矢量或 `TrueType` 字体的枚举数据
      * CLIP\_EMBEDDED
> > > > 当使用内嵌的只读字体时，必须指定这个标志
      * CLIP\_LH\_ANGLES
        * 如果指定了该值，所有字体的旋转都依赖于坐标系统的方向是逆时针或顺时针
        * 如果没有指定该值，设备字体始终逆时针旋转，但是其它字体的旋转依赖于坐标系统的方向
        * 该设置影响 lfOrientation 参数的效果。
    * lfQuality 指定文字的输出质量

> > > 输出质量定义图形设备界面 (GDI) 必须尝试将逻辑字体属性与实际物理字体的字体属性进行匹配的仔细程度
      * ANTIALIASED\_QUALITY
> > > > 指定输出质量是抗锯齿的（如果字体支持）
      * DEFAULT\_QUALITY
> > > > 指定输出质量不重要
      * DRAFT\_QUALITY
> > > > 草稿质量。字体的显示质量是不重要的。对于光栅字体（即点阵字体），缩放是有效的，这就意味着可以使用更多的尺寸，但是显示质量并不高。如果需要，粗体、斜体、下划线和删除线字体会被合成
      * NONANTIALIASED\_QUALITY
> > > > 指定输出质量不是抗锯齿的
      * PROOF\_QUALITY
> > > > 正稿质量。指定字体质量比匹配字体属性更重要。对于光栅字体（即点阵字体），缩放是无效的，会选用其最接近的字体大小。虽然选中 PROOF\_QUALITY 时字体大小不能精确地映射，但是输出质量很高，并且不会有畸变现象。如果需要，粗体、斜体、下划线和删除线字体会被合成

> > > 如果 ANTIALIASED\_QUALITY 和 NONANTIALIASED\_QUALITY 都未被选择，抗锯齿效果将依赖于控制面板中字体抗锯齿的设置
    * lfPitchAndFamily 指定以常规方式描述字体的字体系列
      * 字体系列描述大致的字体外观
      * 字体系列用于在所需精确字体不可用时指定字体
      * 1~2 位指定字体间距
        * DEFAULT\_PITCH 指定默认间距。
        * FIXED\_PITCH 指定固定间距。
        * VARIABLE\_PITCH 指定可变间距。
      * 4~7 位指定字体系列
        * FF\_DECORATIVE 指定特殊字体
> > > > > 例如 Old English
        * FF\_DONTCARE 指定字体系列不重要
        * FF\_MODERN 指定具有或不具有衬线的等宽字体
> > > > > 例如 Pica、Elite 和 Courier New 都是等宽字体
        * FF\_ROMAN 指定具有衬线的等比字体
> > > > > 例如 MS Serif
        * FF\_SCRIPT 指定设计为类似手写体的字体
> > > > > 例如 Script 和 Cursive
        * FF\_SWISS 指定不具有衬线的等比字体
> > > > > 例如 MS Sans Serif
      * 字体间距和字体系列可以用布尔运算符 OR 连接(即符号 |)
    * lfFaceName 字体名称，名称不得超过 31 个字符

> > > 如果是空字符串，系统将使用第一个满足其它属性的字体

#### outtext ####

  * 功能 这个函数用于在当前位置输出字符串
  * 声明
```
void outtext(
    LPCSTR textstring,
    PIMAGE pimg = NULL
);
void outtext(
    CHAR c,
    PIMAGE pimg = NULL
);
void outtext(
    LPCWSTR textstring,
    PIMAGE pimg = NULL
);
void outtext(
    WCHAR c,
    PIMAGE pimg = NULL
);
```
  * 参数
    * textstring 要输出的字符串的指针
    * c 要输出的字符
  * 返回值 无
  * 示例
```
// 输出字符串
char s[] = "Hello World";
outtext(s);
// 输出字符
char c = 'A';
outtext(c);
// 输出数值，先将数字格式化输出为字符串
char s[5];
sprintf(s, "%d", 1024);
outtext(s);
```

#### outtextrect ####

  * 功能 这个函数用于在指定矩形范围内输出字符串
  * 声明
```
void outtextrect(
    int x,
    int y,
    int w,
    int h,
    LPCSTR textstring
    PIMAGE pimg = NULL
);
void outtextrect(
    int x,
    int y,
    int w,
    int h,
    LPCWSTR textstring
    PIMAGE pimg = NULL
);
```
  * 参数
    * x, y, w, h 要输出字符串所在的矩形区域
    * textstring 要输出的字符串的指针
  * 返回值 无
  * 示例 无

#### outtextxy ####

  * 功能 这个函数用于在指定位置输出字符串
  * 声明
```
void outtextxy(
    int x,
    int y,
    LPCSTR textstring
    PIMAGE pimg = NULL
);
void outtextxy(
    int x,
    int y,
    CHAR c
    PIMAGE pimg = NULL
);
void outtextxy(
    int x,
    int y,
    LPCWSTR textstring
    PIMAGE pimg = NULL
);
void outtextxy(
    int x,
    int y,
    WCHAR c
    PIMAGE pimg = NULL
);
```
  * 参数
    * x 字符串输出时头字母的 x 轴的坐标值
    * y 字符串输出时头字母的 y 轴的坐标值
    * textstring 要输出的字符串的指针
    * c 要输出的字符
  * 返回值 无
  * 示例
```
// 输出字符串
char s[] = "Hello World";
outtextxy(10, 20, s);
// 输出字符
char c = 'A';
outtextxy(10, 40, c);
// 输出数值，先将数字格式化输出为字符串
char s[5];
sprintf(s, "%d", 1024);
outtextxy(10, 60, s);
```

#### setfont ####

  * 功能 这个函数用于设置当前字体样式
  * 声明
```
void setfont(
    int nHeight,
    int nWidth,
    LPCSTR lpszFace,
    PIMAGE pimg = NULL
);
void setfont(
    int nHeight,
    int nWidth,
    LPCSTR lpszFace,
    int nEscapement,
    int nOrientation,
    int nWeight,
    bool bItalic,
    bool bUnderline,
    bool bStrikeOut,
    PIMAGE pimg = NULL
);
void setfont(
    int nHeight,
    int nWidth,
    LPCSTR lpszFace,
    int nEscapement,
    int nOrientation,
    int nWeight,
    bool bItalic,
    bool bUnderline,
    bool bStrikeOut,
    BYTE fbCharSet,
    BYTE fbOutPrecision,
    BYTE fbClipPrecision,
    BYTE fbQuality,
    BYTE fbPitchAndFamily,
    PIMAGE pimg = NULL
);
void setfont(
    const LOGFONT *font,
    PIMAGE pimg = NULL
);
```
  * 参数
    * nHeight
> > > 指定高度（逻辑单位）。如果为正，表示指定的高度包括字体的默认行距；如果为负，表示指定的高度只是字符的高度
    * nWidth
> > > 字符的平均宽度（逻辑单位）。如果为 0，则比例自适应
    * lpszFace
> > > 字体名称。对于此参数均有LPCSTR和LPCWSTR两个版本，以上函数声明仅列出一种。提供两个接口是为了方便能同时使用两种不同的字符集
    * nEscapement
> > > 字符串的书写角度，单位 0.1 度
    * nOrientation
> > > 每个字符的书写角度，单位 0.1 度
    * nWeight
> > > 字符的笔画粗细，范围 0~1000。0 表示默认粗细。使用数字或下表中定义的宏均可
      * FW\_DONTCARE   0
      * FW\_THIN       100
      * FW\_EXTRALIGHT 200
      * FW\_ULTRALIGHT 200
      * FW\_LIGHT      300
      * FW\_NORMAL     400
      * FW\_REGULAR    400
      * FW\_MEDIUM     500
      * FW\_SEMIBOLD   600
      * FW\_DEMIBOLD   600
      * FW\_BOLD       700
      * FW\_EXTRABOLD  800
      * FW\_ULTRABOLD  800
      * FW\_HEAVY      900
      * FW\_BLACK      900
    * bItalic
> > > 是否斜体，true / false。
    * bUnderline
> > > 是否有下划线，true / false。
    * bStrikeOut
> > > 是否有删除线，true / false。
    * fbCharSet
> > > 指定字符集(详见 LOGFONT 结构体)。
    * fbOutPrecision
> > > 指定文字的输出精度(详见 LOGFONT 结构体)。
    * fbClipPrecision
> > > 指定文字的剪辑精度(详见 LOGFONT 结构体)。
    * fbQuality
> > > 指定文字的输出质量(详见 LOGFONT 结构体)。
    * fbPitchAndFamily
> > > 指定以常规方式描述字体的字体系列(详见 LOGFONT 结构体)。
    * font
> > > 指向 LOGFONT 结构体的指针。
  * 返回值 无
  * 示例
```
// 设置当前字体为高 16 像素的“宋体”（忽略行距）。
setfont(-16, 0,"宋体");

outtextxy(0, 0,"测试");

// 设置输出效果为抗锯齿
LOGFONT f;

// 获取当前字体设置
getfont(&f);

// 设置字体高度为 48（包含行距）
f.lfHeight = 48;

// 设置字体为“黑体”
strcpy(f.lfFaceName, "黑体");

// 设置输出效果为抗锯齿 
f.lfQuality = ANTIALIASED_QUALITY;

// 设置字体样式
setfont(&f);

outtextxy(0,50,"抗锯齿效果");
```

#### settextjustify ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### textheight ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### textwidth ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

### 图像处理相关函数 ###

|getimage                  |从屏幕 / 文件 / 资源 / IMAGE 对象中获取图像|
|:-------------------------|:--------------------------------------------------------|
|IMAGE                     |对象 保存图像的对象|
|imagefilter\_blurring      |对指定图像进行图像模糊滤镜操作|
|putimage                  |在屏幕上绘制指定图像|
|putimage\_alphablend       |在屏幕上以半透明方式绘制指定图像|
|putimage\_transparent      |在屏幕上以透明方式绘制指定图像|
|putimage\_alphatransparent |在屏幕上以透明/半透明方式绘制指定图像|
|三元光栅操作码            |介绍三元光栅操作码|

#### getimage ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### IMAGE ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### imagefilter\_blurring ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### putimage ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### putimage\_alphablend ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### putimage\_transparent ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### putimage\_alphatransparent ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### 三元光栅操作码 ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

### 鼠标相关函数 ###

|`FlushMouseMsgBuffer` |清空鼠标消息缓冲区|
|:---------------------|:--------------------------|
|`GetMouseMsg`         |获取一个鼠标消息。如果当前鼠标消息队列中没有，就一直等待|
|`GetMousePos`         |获取当前鼠标位置。无等待|
|`MouseHit`            |检测当前是否有鼠标消息|
|`ShowMouse`           |设置鼠标显示状态|
|MOUSEMSG                  |结构体 保存鼠标消息的结构体|

#### `FlushMouseMsgBuffer` ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### `GetMouseMsg` ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### `GetMousePos` ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### `MouseHit` ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### `ShowMouse` ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### MOUSEMSG ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

### 时间函数 ###

|API\_Sleep |实际调用API中的Sleep，因直接调用Sleep会被转化为调用delay|
|:----------|:--------------------------------------------------------------------------|
|delay     |同delay\_ms|
|delay\_ms  |延迟以毫秒为单位的时间|
|delay\_fps |延迟以FPS为准的时间，以实现稳定帧率|
|delay\_jfps|延迟以FPS为准的时间，以实现稳定帧率（带跳帧）|
|fclock    |获取当前程序从初始化起经过的时间，以秒为单位|

#### API\_Sleep ####

  * 功能 与Sleep函数完全相同，单纯延迟指定时间（精确程度由系统API决定），其它事情什么都不干
  * 声明
```
VOID API_Sleep(
    DWORD dwMilliseconds
);
```
  * 参数
    * dwMilliseconds 要延迟的时间，以毫秒为单位，如果为 0 则不产生延时的作用（相当于无意义调用）
> > > 不会附带刷新窗口的作用
  * 返回值 无
  * 示例 无

#### delay ####

  * 功能 与delay\_ms完全相同，详见delay\_ms
  * 声明
```
void delay(
    int Milliseconds
);
```
  * 参数
    * Milliseconds 要延迟的时间，以毫秒为单位
  * 返回值 无
  * 示例 无

#### delay\_ms ####

  * 功能 延迟以毫秒为单位的时间
  * 声明
```
void delay_ms(
    int Milliseconds
);
```
  * 参数
    * Milliseconds 要延迟的时间，以毫秒为单位
  * 返回值 无
  * 示例 无

#### delay\_fps ####

  * 功能 延迟以FPS为准的时间，以实现稳定帧率
  * 声明
```
void delay_fps(
    int fps
);
```
  * 参数
    * fps 要得到的帧率，平均延迟1000/fps毫秒，并更新FPS计数值
> > > 这个函数一秒最多能调用fps次
  * 返回值 无
  * 示例 无

#### delay\_jfps ####

  * 功能 延迟以FPS为准的时间，以实现稳定帧率（带跳帧）
  * 声明
```
void delay_jfps(
    int fps
);
```
  * 参数
    * fps 要得到的帧率，平均延迟1000/fps毫秒，并更新FPS计数值
> > > 这个函数一秒最多能调用fps次


> 注意的是，即使这帧跳过了，仍然会更新FPS计数值
  * 返回值 无
  * 示例 无

#### fclock ####

  * 功能 获取当前程序从初始化起经过的时间，以秒为单位
  * 声明
```
double fclock();
```
  * 参数 无
  * 返回值 返回一个以秒为单位的浮点数，精度比API的GetTickCount稍高
> > 程序中使用一般用于求时间差，一般不要直接使用这个值
  * 示例 无

### 数学函数 ###

|rotate\_point3d\_x      |把一个3d点绕x轴旋转|
|:-----------------------|:--------------------------|
|rotate\_point3d\_y      |把一个3d点绕y轴旋转|
|rotate\_point3d\_z      |把一个3d点绕z轴旋转|
|VECTOR3D              |库提供的3d向量类，以下为类的成员简介|
|VECTOR3D::operator =  |向量复制|
|VECTOR3D::operator +  |3d向量加法|
|VECTOR3D::operator -  |3d向量减法|
|VECTOR3D::operator |与浮点数相乘时为向量缩放，与向量相乘时为点乘|
|VECTOR3D::operator &  |向量叉乘|
|VECTOR3D::GetAngel    |计算两个3d向量的夹角|
|VECTOR3D::GetModule   |计算3d向量的模|
|VECTOR3D::GetSqrModule|计算3d向量模的平方|
|VECTOR3D::Rotate      |3d向量绕另一任意向量旋转，或者按指定旋转角旋转|
|VECTOR3D::SetModule   |在保持方向不变的情况下把3d向量长度改为设定值|

#### rotate\_point3d\_x ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### rotate\_point3d\_y ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### rotate\_point3d\_z ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::operator = ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::operator + ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::operator - ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::operator **####**

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::operator & ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::GetAngel ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::GetModule ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::GetSqrModule ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::Rotate ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### VECTOR3D::SetModule ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

### 随机函数 ###

|random    |生成0 - n-1范围内的随机数|
|:---------|:---------------------------------|
|randomf   |生成0.0-1.0范围内的随机数（0.0取到，1.0取不到）|
|randomize |初始化随机数序列|

#### random ####

  * 功能 这个函数用于生成某范围内的随机整数
  * 声明
```
unsigned int random(
    unsigned int n = 0
    );
```
  * 参数
    * n 生成0至n-1之间的整数
> > > 如果n为0，则返回0 - 0xFFFFFFFF的整数
  * 返回值 返回一个随机整数
  * 其它说明

> > 建议不要使用stdlib里的rand函数，而改用本函数。 本函数使用专业的随机数生成算法，随机性远超系统的rand函数。另，千万不要自己`random() % n`的方式取获得一个范围内的随机数，请使用`random(n)`，切记。本随机序列的初始化只能调用randomize函数，不能使用srand。

#### randomf ####

  * 功能 这个函数用于生成0-1范围内的随机浮点数
  * 声明
```
double randomf();
```
  * 参数 无
  * 返回值 返回一个0-1之间的随机浮点数
> > 0.0可能取得到，1.0一定取不到
  * 其它说明
> > 本随机序列的初始化只能调用randomize函数，不能使用srand

#### randomize ####

  * 功能 这个函数用于初始化随机数序列
> > 如果不调用本函数，那么random返回的序列将会是确定不变的
  * 声明
```
void randomize();
```
  * 参数 无
  * 返回值 无
  * 示例 无

### 其它函数 ###

|GetFPS            |获取当前窗口刷新率（FPS = Frame Per Second）|
|:-----------------|:------------------------------------------------------|
|GetHWnd           |获取当前窗口句柄|
|InputBoxGetLine	|使用对话框让用户输入一个字符串|
|keystate          |判断某按键是否按下|

#### GetFPS ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### GetHWnd ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### InputBoxGetLine ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

#### keystate ####

  * 功能
  * 声明
  * 参数
  * 返回值
  * 示例

## 教程 ##

### 第一章 ###

#### 第01课 第一个图形窗口程序 ####

```
#include "graphics.h"

int WinMain()
{
    //初始化为800*600大小
    //默认会显示一个EGE的Logo，如果你不希望显示调用
	//setinitmode(0);
    //本函数只要调用过一次，那么那个Logo就不会显示，这个函数只在initgraph前调用才有效
    //更多参数见文档
    //setinitmode (0, 50, 30);
    //initgraph (970, 712);
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第02课 第一个画图程序 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    //设置画图颜色，GREEN是颜色常数，详细可以查graphics.h对这个宏的定义的值
    setcolor (GREEN);

    //画一直线，从(100,100)到(500,200)
    //特别注意的是端点，(100,100)这个点会被画上颜色，但(500,200)不会画上颜色
    //以下所有的矩形（或者说两点）描述方式，总是前一个点取得到，但后一个点取不到
    line (100, 100, 500, 200);

    getch();

    closegraph();
    return 0;
}
```

#### 第03课 色彩的运用计算 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    //设置画图颜色，使用RGB宏，三个参数值的范围均为0 - 255 (0xFF)
    //分别表示红色亮度，绿色亮度，蓝色亮度
    //RGB(0xFF, 0x0, 0x0) (纯红色) 等价于0x0000FF 注意次序是反着的
    //setcolor (RGB (0xFF, 0x0, 0x0));
    setcolor (0x0000FF);

    //画一圆，圆心在(200,200)，半径100
    circle(200, 200, 100);

    getch();

    closegraph();
    return 0;
}
```

#### 第04课 颜色填充 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    // 设置填充颜色
    // setfillstyle (RGB( 0xFF, 0x0, 0x80));
    setfillstyle (0x8000FF));

    // 画一实心矩形，范围为 x坐标从50-300，y坐标从100-200
    bar (50, 100, 300, 200);

    getch();

    closegraph();
    return 0;
}
```

#### 第05课 图形边界和填充 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    // 设置绘图颜色，一般用于边界
    // setcolor (RGB (0xFF, 0xFF, 0x0));
    setcolor (0x00FFFF);

    // 设置填充颜色，一般为图形内部颜色
    // setfillstyle (RGB (0xFF, 0x0, 0x80));
    setfillstyle (0x8000FF);

    // 画一带填充的椭圆
    fillellipse (200, 200, 150, 100);

    // 画一个空心圆
    circle (500, 300, 100);

    // 再次设置填充颜色，用于决定下一函数填充的颜色
    // setfillstyle (RGB (0x80, 0x0, 0xFF));
    setfillstyle (0xFF0080);

    // 手工填充
    // x,y是开始填充的坐标，第三个参数是填充的边界颜色，或者说以这个颜色作为边界
    // 如果这个边界不封闭，那么会导致整个屏幕都是这个颜色
    // floodfill (500, 300, RGB (0xFF, 0xFF, 0x0));
    floodfill (500, 300, 0x00FFFF);
   
    getch();

    closegraph();
    return 0;
}
```

#### 第06课 屏幕背景色 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    //第一次设置背景色（仅设置不立即生效）
    setbkcolor_f(RGB(0x0, 0x40, 0x0)); //浅绿色
    //清屏，这时就使用前面设置的背景色，使屏幕颜色全部为背景色
    cleardevice();

    setcolor(RGB(0xFF, 0xFF, 0x0));
    setfillstyle(RGB(0xFF, 0x0, 0x80));

    //画带填充的扇形
    sector(200, 200, 45, 135, 150, 100);

    getch();

    //按下一任意键后，再次改变背景色
    //这个设置方式是立即生效，把当前为旧背景色的像素的颜色变为新的背景色
    setbkcolor(RGB(0x0, 0x0, 0x40)); //浅蓝色

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第07课 文字绘制与文字相关设置 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    //先画一个矩形，以便于看出背景色的问题
    setfillstyle(RGB(0x0, 0x80, 0x80));
    bar(50, 50, 500, 200);

    //文字颜色
    setcolor(RGB(0x0, 0xFF, 0x0));

    //文字背景色（setbkcolor函数也会改变文字背景色）
    setfontbkcolor(RGB(0x80, 0x00, 0x80));

    //设置字体，第一个参数是字体的高度（像素），第二个参数是字体的宽度，第二个参数如果为0，就使用默认比例值
    //如果高度为12，即相当于小五号字，或者9磅字，实际的换算就自己完成吧
    setfont(12, 0, "宋体");

    //写文字，注意：outtextxy不支持\t \n这类格式化用的特殊字符，这类字符会被忽略
    //要使用特殊格式化字符请用outtextrect
    outtextxy(100, 100, "Hello EGE Graphics");
    outtextrect(100, 120, 200, 100, "\tHello EGE Graphics\nHere is the next line.");

    //设置文字背景填充方式为透明，默认为OPAQUE不透明
    setbkmode(TRANSPARENT);
    outtextxy(100, 150, "Hello EGE Graphics, 中文也是支持的");

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第08课 图形视口剪裁 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    //设置视口矩形区域为(200,100) - (330, 130)
    //最后一个参数为1表示出了这个区域的图形会被裁剪
    //后面所绘画的图形的原点坐标(0,0)，会映射到(200,100)
    setviewport(200, 100, 330, 130, 1);

    //画一些文字，注意文字会因区域被裁剪的效果
    setcolor(RGB(0x0, 0xFF, 0x0));
    setfontbkcolor(RGB(0x80, 0x00, 0x80));
    setfont(18, 0, "宋体");
    outtextxy(0, 0, "Hello EGE Graphics");

    setbkmode(TRANSPARENT);
    outtextxy(0, 20, "Hello EGE Graphics");

    //还原视口
    setviewport(0, 0, getwidth(), getheight(), 1);
    outtextxy(0, 0, "Hello EGE Graphics");


    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第09课 使用IMAGE——抓图，绘画到IMAGE，IMAGE到屏幕 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    //先随便画一些东西
    setcolor(RGB(0xFF, 0xFF, 0x0));
    setfillstyle(RGB(0xFF, 0x0, 0x80));
    fillellipse(50, 50, 50, 50);
   
    //声明一个img图片对象
    //注意这个声明绝对不能放在initgraph的前面，除非你使用IMAGE*或者PIMAGE
    //然后用new在initgraph后创建这个对象。但记得要delete
    //绝不能使用malloc来新建一个IMAGE对象
    IMAGE img;

    //从屏幕上截取(0, 0) - (80, 60)这部分作为img，这个img大小为80*60
    //注意，(0,0)这点会被包含在img里，但(80, 60)不包含
    getimage(&img, 0, 0, 80, 60);

    //对img设置填充色为绿色（第二第三个参数使用了默认值，这两参数极少使用非默认值，这两参数更多的解释见文档）
    //最后一个参数写你要设置的IMAGE对象
    setfillstyle(RGB(0x0, 0x70, 0x0), SOLID_FILL, &img);

    //对img画实心矩形
    bar(40, 20, 70, 50, &img); 
   
    int x, y;
    //把img平铺在屏幕上，使用一个二重循环
    for (y = 0; y < 8; ++y)
    {
        for (x = 0; x < 8; ++x)
        {
            //把img整个，画在指定的坐标上，左上角对齐这个坐标
            putimage(x * 80, y * 60, &img);
        }
    }

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第10课 使用IMAGE——图片缩放 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    //先随便画一些东西
    setcolor(RGB(0xFF, 0xFF, 0x0));
    setfillstyle(RGB(0xFF, 0x0, 0x80));
    fillellipse(50, 50, 50, 50);

    IMAGE img;

    getimage(&img, 0, 0, 160, 120);

    int x, y;
    //把img平铺在屏幕上，使用一个二重循环
    for (y = 0; y < 8; ++y)
    {
        for (x = 0; x < 8; ++x)
        {
            //把img整个，拉伸画在指定的矩形里
            //需要指定目标矩形，源矩形
            //源矩形参数不能忽略，否则会和其它非拉伸功能的贴图函数混淆
            putimage(x * 80, y * 60, 80, 60, &img, 0, 0, 160, 120);
        }
    }

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第11课 使用IMAGE——透明，半透明 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    //先随便画一些东西
    setcolor (RGB (0xFF, 0xFF, 0x0));
    setfillstyle (RGB (0xFF, 0x0, 0x80));
    fillellipse (50, 50, 50, 50);

    IMAGE img;

    getimage (&img, 0, 0, 160, 120);

    //先画一个非黑色背景，以便于比较
    setbkcolor (0x808080);
    cleardevice();

    //四种贴图比较
    putimage (0, 0, &img);
    //半透明度为0x80
    putimage_alphablend (NULL, &img, 160, 0, 0x80);
    //透明贴图，关键色为BLACK，源图为这个颜色的地方会被忽略
    putimage_transparent (NULL, &img, 0, 80, BLACK);
    //同时使用透明和半透明
    putimage_alphatransparent (NULL, &img, 160, 80, BLACK, 0xA0);

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第12课 用户交互——键盘 ####

```
#include "graphics.h"

//这个例子需要这个头文件
#include "stdio.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph (800, 600);

    setfont(18, 0, "宋体");
    outtextxy(0, 0, "请任意按下键盘上的按键");

    int k = 0;

    // 27是ESC的值，表明你按下ESC就退出
    for ( ; k != 27; )
    {
        char str[32];
        //等待用户按键，并把得到的按键给k
        //如果你不想等待，可以在调用getch之前
        //使用kbhit检测是否有按键按下
        //如 if ( kbhit() ) k = getch();
        k = getch();

        //格式化输出为字符串，用于后面输出
        sprintf(str, "%c %3d", k, k);

        cleardevice();
        outtextxy(0, 0, str);
    }

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

##### 多按键同时检测状态和判断按键首次按下的办法 #####


> 该办法仅用于EGE

方法，使用getch/kbhit的扩展参数实现，直接获得键盘消息和虚拟键码，详见以下代码：

```
#include "graphics.h"
#include <stdio.h>

int WinMain()
{
    //记录按键状态的数组
    int keys[256] = {0};
   
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setfont(12, 6, "宋体");
    BeginBatchDraw();

    for (int k; (k = kbhit(1)) != -1; delay_fps(60))
    {
        while (k)
        {
            // 如果有按键消息，则获取一个
            k = getch(1);

            //按键按下消息
            if (k & KEYMSG_DOWN)
            {
                keys[k & 0xFFFF] = 1;
            }
            //按键松开消息
            else if (k & KEYMSG_UP)
            {
                keys[k & 0xFFFF] = 0;
            }
            //检查还有没有消息
            k = kbhit(1);
        }
        cleardevice();

        //遍历A-Z，查看其状态并输出
        for (int n=0; n<26; n++)
        {
            char str[10];
            if (keys['A' + n])
            {
                sprintf(str, "%c       Down", 'A' + n);
            }
            else
            {
                sprintf(str, "%c", 'A' + n);
            }
            outtextxy(10, n*12, str);
        }
    }
    EndBatchDraw();

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();

    return 0;
}
```

说明： 调用getch(1)的时候，返回值分为高16位和低16位，高16位是这个消息的类型，分为按键松开和按键按下两种，低16位是虚拟键码值。所以，k & 0xFFFF就是低16位，虚拟键码范围一般在1-255之间

再补充一段，用于判断是否第一次按下按键的代码（使用这个时，也请先运行以下这个例子，以明白工作方式）

```
#include "graphics.h"
#include <stdio.h>

int WinMain()
{
    int keys[256] = {0};

    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setfont(12, 6, "宋体");

    BeginBatchDraw();

    for (int k; (k = kbhit(1)) != -1; delay_fps(60))
    {
        while (k)
        {
            k = getch(1);
            if (k & KEYMSG_FIRSTDOWN)
            {
                keys[k& 0xFFFF] = 2;
            }
            else if (k & KEYMSG_DOWN)
            {
                keys[k& 0xFFFF] = 1;
            }
            else if (k & KEYMSG_UP)
            {
                keys[k& 0xFFFF] = 0;
            }
            k = kbhit(1);
        }
        cleardevice();
        for (int n=0; n<26; n++)
        {
            char str[10];
            if (keys['A' + n] == 2)
            {
                sprintf(str, "%c       FirstDown", 'A' + n);
            }
            else if (keys['A' + n] == 1)
            {
                sprintf(str, "%c       Down", 'A' + n);
            }
            else
            {
                sprintf(str, "%c", 'A' + n);
            }
            outtextxy(10, n*12, str);
        }
    }

    EndBatchDraw();

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();

    return 0;
}
```

#### 第13课 用户交互——鼠标1 ####

```
#include "graphics.h"
#include <stdio.h>

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setfont(18, 0, "宋体");

    int k = 0;
    for ( ; kbhit() == 0; )
    {
        char str[32];
        int x, y;

        //获取鼠标坐标，此函数不等待。若鼠标移出了窗口，那么坐标值不会更新
        //特殊情况是，你按着鼠标键不放，拖出窗口，这样坐标值会依然更新
        GetMousePos(&x, &y);

        //格式化输出为字符串，用于后面输出
        sprintf(str, "%4d %4d", x, y);

        outtextxy(0, 0, str);
    }

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第14课 用户交互——鼠标2 ####

```
#include "graphics.h"
#include <stdio.h>

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setfont(18, 0, "宋体");

    int k = 0;
    for ( ; kbhit() == 0; )
    {
        char str[32];
        MOUSEMSG msg;
        //获取鼠标消息，这个函数会等待，等待到有消息为止
        //类似地，有和kbhit功能相近的函数MouseHit，用于检测有没有鼠标消息
        msg = GetMouseMsg();

        //格式化输出为字符串，用于后面输出
        sprintf(str, "%4d %4d 左键=%d 右键=%d 中键=%d",
            msg.x, msg.y,
            msg.mkLButton, msg.mkRButton, msg.mkMButton);

        outtextxy(0, 0, str);
    }

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第15课 用户交互——字符串数据输入 ####

```
#include "graphics.h"
#include <stdio.h>

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    //用来接收输入
    char str[100];
    //调用对话框函数
    InputBoxGetLine("请输入", "你爱输入什么就输入什么（回车确认）", str, 100);

    //显示输入的内容
    outtextxy(0, 0, str);

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第16课 高级：更多的文字对齐方式设置 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setfont(18, 0, "宋体");
    //settextjustify(LEFT_TEXT, TOP_TEXT); //默认值
    outtextxy(300, 0, "Hello Graphics");

    settextjustify(RIGHT_TEXT, TOP_TEXT);
    outtextxy(300, 50, "Hello Graphics");

    settextjustify(CENTER_TEXT, TOP_TEXT);
    outtextxy(300, 100, "Hello Graphics");

    settextjustify(LEFT_TEXT, BOTTOM_TEXT);
    outtextxy(300, 50, "Hello Graphics");

    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第17课 高级：更多的颜色表示（HSV/HSL） ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    //初始化随机数种子
    randomize();

    for (; ;)
    {
        //使用随机色彩，纯度为1.0，亮度为0.5
        //第一个参数范围从0 - 360，表示一个角度，这个颜色所在的HSL双头圆锥的方位
        //0是红色，120是绿色，240是蓝色，详见pdf文档内的HSL颜色空间的说明
        setfillstyle(HSLtoRGB(float(random(3600) / 10.0), 1.0f, 0.5f));

        bar(100,100, 300, 200);

        //按一下按键变化一次颜色，ESC退出
        if (getch() == 27) break;
    }
    //等待用户按键
    getch();

    //关闭图形界面
    closegraph();
    return 0;
}
```

#### 第18课 高级：绘画渐变色/彩虹 ####

```
#include "graphics.h"

// alpha 混合计算函数
COLORREF alphasingle(COLORREF a, COLORREF b, COLORREF alpha)
{
    return (a * (0xFF - alpha) + b * alpha) >> 8;
}

// 颜色alpha混合计算函数
COLORREF alphacol(COLORREF d, COLORREF s, COLORREF alpha)
{
    return (alphasingle(d&0xFF00FF, s&0xFF00FF, alpha) & 0xFF00FF)
        | (alphasingle(d&0xFF00, s&0xFF00, alpha) >> 8 << 8);
}

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);
    int c;

    //画渐变色
    for (c=0; c<256; ++c)
    {
        COLORREF a = 0xFF0000, b = 0x0000FF;
        setcolor(alphacol(a, b, c));
        line(0, c, 200, c);
    }

    //画彩虹
    for (c=0; c<360; ++c)
    {
        setcolor(HSLtoRGB((float)c, 1.0f, 0.5f));
        line(200, c, 400, c);
    }
    getch();

    closegraph();
    return 0;
}
```

### 第二章 ###

#### 第01课 基础动画一 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setcolor(0x00FF00);
    setfillstyle(0xFF0000);

    // 动画控制变量，控制横坐标，初始值为0
    int x = 0;

    // 动画主循环，delay_fps(60)令动画每一秒稳定刷新60次（但如果系统忙，有可能少于60）
    // 为什么使用60？因为60是显示器的默认刷新率，99.9%的显示器都是这个设置
    // kbhit()用于检测有没有按键按下，如果有，返回非0值，即如果有按键按下就退出
    for ( ; kbhit() == 0; delay_fps(240) )
    {
        //计算新坐标，右移一个像素，如果等于440则重新移回x=0，达到动画循环
        x = ( x + 1 ) % 440;

        //清屏，重新在新的位置绘图图像
        cleardevice();

        //以x为圆的左边界绘画，为什么是左边界？因为圆心坐标是 (x + 半径) 了
        fillellipse(x + 100, 200, 100, 100);
    }
    getch();

    closegraph();
    return 0;
}
```

#### 第02课 基础动画二，防闪烁 ####

```
#include "graphics.h"

//前一课的例子动画里，会产生偶尔的闪烁，这一课就是要解决这个问题

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setcolor(0x00FF00);
    setfillstyle(0xFF0000);

    int x = 0;
    // 开启批量绘图，保证在你需要更新时，才让窗口内容更新，以免中途更新产生闪烁
    // 如果表明你需要更新呢？当你调用delay/Sleep/delay_fps/delay_ms/getch/GetMouseMsg这类带有等待属性的函数的时候
    // 你调用带有等待属性的函数，就会通知窗口更新
    // 使用批量绘图模式会加速绘图速度，使图形显示更稳定流畅
    BeginBatchDraw();
    for ( ; kbhit() == 0; delay_fps(240) )
    {
        x = ( x + 1 ) % 440;
        cleardevice();
        fillellipse(x + 100, 200, 100, 100);
    }
    //结束批量绘图
    EndBatchDraw();

    getch();

    closegraph();
    return 0;
}
```

#### 第03课 基础动画三，更丰富的变化与帧率 ####

```
#include "graphics.h"
#include <stdio.h>

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    setcolor(0x00FF00);
    setfillstyle(0xFF0000);

    //x,y记录当前位置，dx,dy记录速度的方向，r记录圆半径
    int x = 0, y = 0, dx = 1, dy = 1, r = 100;
    BeginBatchDraw();
    for ( ; kbhit() == 0; delay_fps(240) )
    {
        // 当前位置 + 速度
        x += dx;
        y += dy;
        //碰左
        if (x < r) dx = 1;
        //碰上
        if (y < r) dy = 1;
        //碰右
        if (x >= 800 - r) dx = -1;
        //碰下
        if (y >= 600 - r) dy = -1;

        cleardevice();
        fillellipse(x, y, r, r);
        char str[20];
        //调用GetFPS取得当前帧率
        sprintf(str, "帧率 %.02f", GetFPS());
        outtextxy(0, 0, str);
    }
    EndBatchDraw();

    getch();

    closegraph();
    return 0;
}
```

#### 第04课 基础动画四，半透明淡入淡出 ####

```
#include "graphics.h"

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    //x,y记录当前位置，dx,dy记录速度的方向，r记录圆半径
    int x = 0, y = 0, dx = 1, dy = 1, r = 100, alpha = 0, da = 1;

    // img 直接初始化为 w=r*2, h=r*2大小
    IMAGE img(r * 2, r * 2);

    setcolor(0x00FF00, &img);
    setfillstyle(0xFF0000, SOLID_FILL, &img);

    // 画在img上
    fillellipse(r, r, r, r, &img);

    setbkcolor(DARKGRAY);

    BeginBatchDraw();
    for ( ; kbhit() == 0; delay_fps(240) )
    {
        // 当前位置 + 速度
        x += dx;
        y += dy;
        //碰左
        if (x < 0) dx = 1;
        //碰上
        if (y < 0) dy = 1;
        //碰右
        if (x >= 800 - r * 2) dx = -1;
        //碰下
        if (y >= 600 - r * 2) dy = -1;

        // 改变alpha值
        alpha += da;
        if (alpha <= 0) da = 1;
        if (alpha >= 0xFF) da = -1;

        cleardevice();
        putimage_alphatransparent(NULL, &img, x, y, BLACK, alpha);
    }
    EndBatchDraw();

    getch();

    closegraph();
    return 0;
}
```

#### 第05课 基础动画五，对象封装，使代码更有条理 ####

```
#include "graphics.h"

//定义一个AniObj，即前一例里面的圆，相关属性写在这个结构体里
struct AniObj
{
    int x, y, r;
    int dx, dy;
    int alpha, da;
    PIMAGE img;
};

//初始化，设置坐标，速度方向，透明度，创建IMAGE等
void initobj(AniObj* obj)
{
    obj->x = 0;
    obj->y = 0;
    obj->r = 100;
    obj->dx = 1;
    obj->dy = 1;
    obj->alpha = 0;
    obj->da = 1;

    obj->img = new IMAGE(obj->r * 2, obj->r * 2);

    setcolor(0x00FF00, obj->img);
    setfillstyle(0xFF0000, SOLID_FILL, obj->img);

    fillellipse(obj->r, obj->r, obj->r, obj->r, obj->img);
}

//更新位置等相关属性
void updateobj(AniObj* obj)
{
    // 当前位置 + 速度
    obj->x += obj->dx;
    obj->y += obj->dy;
    //碰左
    if (obj->x < 0) obj->dx = 1;
    //碰上
    if (obj->y < 0) obj->dy = 1;
    //碰右
    if (obj->x >= 800 - obj->r * 2) obj->dx = -1;
    //碰下
    if (obj->y >= 600 - obj->r * 2) obj->dy = -1;

    // 改变alpha值
    obj->alpha += obj->da;
    if (obj->alpha <= 0) obj->da = 1;
    if (obj->alpha >= 0xFF) obj->da = -1;
}

//根据属性值绘画
void drawobj(AniObj* obj)
{
    putimage_alphatransparent(NULL, obj->img, obj->x, obj->y, BLACK, obj->alpha);
}

//释放这个对象时调用
void releaseobj(AniObj* obj)
{
    delete obj->img;
}

//现在来看看main函数，是不是意思很明了呢？
//这样以来，如果要修改动画，是完全不需要动main函数的
//main函数只成为了一个代码框架，详细的实现都在前面的结构和函数
int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    //声明AniObj对象
    AniObj obj;
    //初始化
    initobj(&obj);

    BeginBatchDraw();
    for ( ; kbhit() == 0; delay_fps(240) )
    {
        //更新位置
        updateobj(&obj);

        cleardevice();
        //绘画
        drawobj(&obj);
    }
    EndBatchDraw();

    //释放
    releaseobj(&obj);

    getch();

    closegraph();
    return 0;
}
```

#### 第06课 基础动画六，利用对象封装，显示多个对象 ####

```
#include "graphics.h"

//定义一个AniObj，即前一例里面的圆，相关属性写在这个结构体里
struct AniObj
{
    int x, y, r;
    int dx, dy;
    int alpha, da;
    PIMAGE img;
};

//初始化，设置坐标，速度方向，透明度，创建IMAGE等
void initobj(AniObj* obj)
{
    // random(n) 返回一个 0 到 n-1 之间的随机数
    obj->x = random(getwidth());
    obj->y = random(getheight());
    obj->r = random(20) + 20;
    obj->dx = (int)random(2) * 2 - 1;
    obj->dy = (int)random(2) * 2 - 1;
    obj->alpha = random(250) + 2;
    obj->da = random(2) * 2 - 1;

    obj->img = new IMAGE(obj->r * 2, obj->r * 2);

    setcolor(0x00FF00, obj->img);
    setfillstyle(0xFF0000, SOLID_FILL, NULL, obj->img);

    fillellipse(obj->r, obj->r, obj->r, obj->r, obj->img);
}

//更新位置等相关属性
void updateobj(AniObj* obj)
{
    // 当前位置 + 速度
    obj->x += obj->dx;
    obj->y += obj->dy;
    if (obj->x < 0) obj->dx = 1; //碰左
    if (obj->y < 0) obj->dy = 1; //碰上
    if (obj->x >= 640 - obj->r * 2) obj->dx = -1; //碰右
    if (obj->y >= 480 - obj->r * 2) obj->dy = -1; //碰下

    // 改变alpha值
    obj->alpha += obj->da;
    if (obj->alpha <= 0) obj->da = 1;
    if (obj->alpha >= 0xFF) obj->da = -1;
}

//根据属性值绘画
void drawobj(AniObj* obj)
{
    putimage_alphatransparent(NULL, obj->img, obj->x, obj->y, BLACK, obj->alpha);
}

//释放这个对象时调用
void releaseobj(AniObj* obj)
{
    delete obj->img;
}

#define MAXOBJ 30

int WinMain()
{
    setinitmode (0, 220, 142);
    initgraph(800, 600);

    randomize(); //初始化随机种子

    AniObj obj[MAXOBJ]; //定义对象数组
    int n;
    for (n = 0; n < MAXOBJ; ++n)
    {
        initobj(&obj[n]); //初始化
    }

    BeginBatchDraw();
    for ( ; kbhit() == 0; delay_fps(240) )
    {
        for (n = 0; n < MAXOBJ; ++n)
        {
            updateobj(&obj[n]); //更新位置
        }

        cleardevice();
        for (n = 0; n < MAXOBJ; ++n)
        {
            drawobj(&obj[n]); //绘画
        }
    }
    EndBatchDraw();

    for (n = 0; n < MAXOBJ; ++n)
    {
        releaseobj(&obj[n]); //释放
    }
    closegraph();
    return 0;
}
```

#### 第07课 基础动画七，使用非整数参数，随机色彩，使动画更自然 ####

```
#include "graphics.h"

//定义一个AniObj，即前一例里面的圆，相关属性写在这个结构体里
struct AniObj
{
    float x, y;
    int r;
    float dx, dy;
    int alpha, da;
    PIMAGE img;
};

//自定义函数，用来返回一个0 - m之间的浮点数
float myrand(float m)
{
    return (float)random(10000) * m / 10000.0f;
}

//定义速度基准值，base_speed是最低速度，base_speed+randspeed是最高速度
const float base_speed = 0.5f;
const float randspeed = 1.5f;

//初始化，设置坐标，速度方向，透明度，创建IMAGE等
void initobj(AniObj* obj)
{
    obj->x = (float)random(getwidth());
    obj->y = (float)random(getheight());
    obj->r = random(20) + 20;
    obj->dx = myrand(randspeed) + base_speed;
    obj->dy = myrand(randspeed) + base_speed;
    obj->dx = obj->dx * ((int)random(2) * 2 - 1);
    obj->dy = obj->dy * ((int)random(2) * 2 - 1);
    obj->alpha = random(250) + 2;
    obj->da = random(2) * 2 - 1;

    obj->img = new IMAGE(obj->r * 2, obj->r * 2);

    COLORREF col = HSVtoRGB(myrand(360.0f), 1.0f, 1.0f);
    setcolor(col, obj->img);
    setfillstyle(col, SOLID_FILL, NULL, obj->img);

    fillellipse(obj->r, obj->r, obj->r, obj->r, obj->img);
}

//更新位置等相关属性
void updateobj(AniObj* obj)
{
    // 当前位置 + 速度
    obj->x += obj->dx;
    obj->y += obj->dy;
    if (obj->x < 0) obj->dx = myrand(randspeed) + base_speed; //碰左
    if (obj->y < 0) obj->dy = myrand(randspeed) + base_speed; //碰上
    if (obj->x >= 640 - obj->r * 2) obj->dx = -(myrand(randspeed) + base_speed); //碰右
    if (obj->y >= 480 - obj->r * 2) obj->dy = -(myrand(randspeed) + base_speed); //碰下

    // 改变alpha值
    obj->alpha += obj->da;
    if (obj->alpha <= 0) obj->da = 1;
    if (obj->alpha >= 0xFF) obj->da = -1;
}

//根据属性值绘画
void drawobj(AniObj* obj)
{
    putimage_alphatransparent(NULL, obj->img, (int)obj->x, (int)obj->y, BLACK, obj->alpha);
}

//释放这个对象时调用
void releaseobj(AniObj* obj)
{
    delete obj->img;
}

#define MAXOBJ 30

int main()
{
    initgraph(640, 480);
    randomize(); //初始化随机种子

    AniObj obj[MAXOBJ]; //定义对象数组
    int n;
    for (n = 0; n < MAXOBJ; ++n)
    {
        initobj(&obj[n]); //初始化
    }

    BeginBatchDraw();
    for ( ; kbhit() == 0; delay_fps(120) )
    {
        for (n = 0; n < MAXOBJ; ++n)
        {
            updateobj(&obj[n]); //更新位置
        }

        cleardevice();
        for (n = 0; n < MAXOBJ; ++n)
        {
            drawobj(&obj[n]); //绘画
        }
    }
    EndBatchDraw();

    for (n = 0; n < MAXOBJ; ++n)
    {
        releaseobj(&obj[n]); //释放
    }
    closegraph();
    return 0;
}
```

#### 第08课 基础动画八，使用C++封装你的对象 ####

```
#include "graphics.h"

//看本文章前，你都看了前几篇了吧？觉不觉得似乎有一个固定模式？
//如果你有这个感觉，说明你真的看懂了
//封装一个图形对象，四大必要接口函数 初始化，逻辑更新，绘画（渲染），释放（析构）
//函数少了就绝对不正确，接口函数多了就说明你的封装可能还需要调整
//一般的应用下，就这四个接口就足够了，最少也必须有这四个，请你一定要记得
//另 不是说这个类只有这四个函数，可以有更多的函数方便你自己使用，但对外（对主循环函数）暴露使用的应该就这四个

const float base_speed = 0.5f;
const float randspeed = 1.5f;

//自定义函数，用来返回一个0 - m之间的浮点数
float myrand(float m)
{
    return (float)random(10000) * m / 10000.0f;
}

//定义一个AniObj类
class AniObj
{
public:
    //初始化，设置坐标，速度方向，透明度，创建IMAGE等
    AniObj()
    {
        x = (float)random(getwidth());
        y = (float)random(getheight());
        r = random(20) + 20;
        dx = myrand(randspeed) + base_speed;
        dy = myrand(randspeed) + base_speed;
        dx = dx * ((int)random(2) * 2 - 1);
        dy = dy * ((int)random(2) * 2 - 1);
        alpha = random(250) + 2;
        da = random(2) * 2 - 1;

        img = new IMAGE(r * 2, r * 2);

        COLORREF col = HSVtoRGB(myrand(360.0f), 1.0f, 1.0f);
        setcolor(col, img);
        setfillstyle(col, SOLID_FILL, NULL, img);

        fillellipse(r, r, r, r, img);
    }

    //更新位置等相关属性
    void updateobj()
    {
        // 当前位置 + 速度
        x += dx;
        y += dy;
        if (x < 0) dx = myrand(randspeed) + base_speed; //碰左
        if (y < 0) dy = myrand(randspeed) + base_speed; //碰上
        if (x >= 640 - r * 2) dx = -(myrand(randspeed) + base_speed); //碰右
        if (y >= 480 - r * 2) dy = -(myrand(randspeed) + base_speed); //碰下

        // 改变alpha值
        alpha += da;
        if (alpha <= 0) da = 1;
        if (alpha >= 0xFF) da = -1;
    }

    //根据属性值绘画
    void drawobj()
    {
        putimage_alphatransparent(NULL, img, (int)x, (int)y, BLACK, alpha);
    }

    //释放这个对象时调用
    ~AniObj()
    {
        delete img;
    }

private:
    float x, y;
    int r;
    float dx, dy;
    int alpha, da;
    PIMAGE img;
};


#define MAXOBJ 30

int main()
{
    initgraph(640, 480);
    randomize(); //初始化随机种子

    AniObj obj[MAXOBJ]; //定义对象数组
    int n;

    //为什么这里没有初始化？因为在类对象声明的时候就调用了构造函数初始化好了

    BeginBatchDraw();
    for ( ; kbhit() == 0; delay_fps(120) )
    {
        for (n = 0; n < MAXOBJ; ++n)
        {
            obj[n].updateobj(); //更新位置
        }

        cleardevice();
        for (n = 0; n < MAXOBJ; ++n)
        {
            obj[n].drawobj(); //绘画
        }
    }
    EndBatchDraw();

    //为什么这里没有释放？因为obj是数组对象，会在本过程结束后自动调用释放函数
    //但如果你是new出来的对象，那必须使用delete去删除

    closegraph();
    return 0;
}
```

#### 第09课 基础动画九，使用场景，更灵活地控制动画 ####

```
#include "graphics.h"

//开始这课前，先来规范一下函数接口声明
//逻辑更新，使用update
//绘画渲染，使用render
//本课要讲如何控制动画，动画的播放，暂停
//我们把动画封装在一个场景，由场景类来控制动画
//当然，现在开始就不是单纯的动画，还加入了用户交互的时候，接口就要增加了

const float base_speed = 0.5f;
const float randspeed = 1.5f;

//自定义函数，用来返回一个0 - m之间的浮点数
float myrand(float m)
{
    return (float)random(10000) * m / 10000.0f;
}

//定义一个AniObj类，这个与前一个除了函数名，和update加了返回值以外没有变化
class AniObj
{
public:
    //初始化，设置坐标，速度方向，透明度，创建IMAGE等
    AniObj()
    {
        x = (float)random(getwidth());
        y = (float)random(getheight());
        r = random(20) + 20;
        dx = myrand(randspeed) + base_speed;
        dy = myrand(randspeed) + base_speed;
        dx = dx * ((int)random(2) * 2 - 1);
        dy = dy * ((int)random(2) * 2 - 1);
        alpha = random(250) + 2;
        da = random(2) * 2 - 1;

        img = new IMAGE(r * 2, r * 2);

        COLORREF col = HSVtoRGB(myrand(360.0f), 1.0f, 1.0f);
        setcolor(col, img);
        setfillstyle(col, SOLID_FILL, NULL, img);

        fillellipse(r, r, r, r, img);
    }

    //释放这个对象时调用
    ~AniObj()
    {
        delete img;
    }

    //更新位置等相关属性
    int update()
    {
        // 当前位置 + 速度
        x += dx;
        y += dy;
        if (x < 0) dx = myrand(randspeed) + base_speed; //碰左
        if (y < 0) dy = myrand(randspeed) + base_speed; //碰上
        if (x >= 640 - r * 2) dx = -(myrand(randspeed) + base_speed); //碰右
        if (y >= 480 - r * 2) dy = -(myrand(randspeed) + base_speed); //碰下

        // 改变alpha值
        alpha += da;
        if (alpha <= 0) da = 1;
        if (alpha >= 0xFF) da = -1;
        return 0;
    }

    //根据属性值绘画
    void render()
    {
        putimage_alphatransparent(NULL, img, (int)x, (int)y, BLACK, alpha);
    }

    void onkey(int key)
    {
        //
    }

private:
    float x, y;
    int r;
    float dx, dy;
    int alpha, da;
    PIMAGE img;
};

class Scene
{
public:
    //初始化，参数为对象个数
    Scene(int nAniObj)
    {
        m_cntObj = nAniObj;
        m_pobj = new AniObj[m_cntObj];
        m_pause = 0;
        m_endscene = 0;
    }
    ~Scene()
    {
        delete [] m_pobj;
    }
    int update()
    {
        // 非暂停状态才更新
        if (m_pause == 0)
        {
            for (int n = 0; n < m_cntObj; ++n)
            {
                m_pobj[n].update();
            }
        }
        return m_endscene;
    }
    void render()
    {
        for (int n = 0; n < m_cntObj; ++n)
        {
            m_pobj[n].render();
        }
    }
    void onkey(int key)
    {
        if (key == 'P' || key == 'p') //按下P键就在播放与暂停之间转换
        {
            m_pause = !m_pause;
        }
        if (key == VK_ESCAPE) //如果是ESC键，就标记为退出场景，VK_ESCAPE是SDK定义的宏
        {
            m_endscene = 1;
        }
    }
private:
    AniObj* m_pobj;
    int m_cntObj;
    int m_pause;
    int m_endscene;
};

int main()
{
    initgraph(640, 480);
    randomize(); //初始化随机种子

    Scene scene(30); //定义场景，初始化参数为30

    BeginBatchDraw();
    for ( ; ; delay_fps(120) )
    {
        while (kbhit())
        {
            int key = getch();
            scene.onkey(key); //所有按键消息发送给scene
        }
        if (scene.update()) //如果update返回非0表示场景结束，这时退出主循环
        {
            break;
        }

        cleardevice();
        scene.render();
    }
    EndBatchDraw();

    closegraph();
    return 0;
}

//后记，scene对象里，已经有自己的对象列表，如果做成复杂一点的结构，
//还可以动态控制对象的个数，按对象的属性在更高层控制这个对象，
//比如已经越出屏幕就回收这个对象，单独控制一个对象的显隐等
//（当然显隐也可以由那个对象自己控制，但场景可以强制让其不显示而不由对象本身控制）
```

### 第三章 ###

## 一些示例 ##

### 打字游戏 ###

### 彩色流星雨 ###

```
#include "graphics.h"

// 星星总数
#define MAXSTAR 30

struct STAR
{
    float x, y;
    float lx, ly;
    float step;
    COLORREF col;
};

// int sc_w = 640, sc_h = 480;
int sc_w = 800, sc_h = 600;
STAR g_star[MAXSTAR];

void InitStar(STAR* star)
{
    star->x = (float)random(sc_w);
    star->y = 0;
    star->lx = star->x;
    star->ly = star->y;
    star->step = float(random(10000) / 1000.0) + 3.0f;
    star->col = HSVtoRGB(float(random(3600) / 10.0f), 1.0f, 1.0f);
}

void MoveStar(STAR* star, float dt)
{
    star->lx = star->x;
    star->ly = star->y;
    if (star->y >= sc_h)
    {
        InitStar(star);
    }
    star->y += star->step * dt;
}

void DrawStar(STAR* star)
{
    setcolor(star->col);
    line(int(star->lx), int(star->ly), int(star->x), int(star->y));
}

int WinMain()
{
    setinitmode (0, 220, 142);
    // initgraph (800, 600);

    int i;

    randomize();

    initgraph(sc_w, sc_h);

    for (i=0; i< MAXSTAR; ++i)
    {
        InitStar(g_star + i);
    }

    BeginBatchDraw();

    for (; kbhit() == 0; delay_fps(60))
    {
        /* cleardevice();
         *
         * 模糊度参数最好使用0-7F(4向模糊)之间的数值
         * 因为80 - FF(8向模糊)的话计算量会翻倍
         */
        imagefilter_blurring(NULL, 0x4F, 0x100);
        for (i=0; i< MAXSTAR; ++i)
        {
            MoveStar(g_star + i, 1.0f);
            DrawStar(g_star + i);
        }
    }

    EndBatchDraw();
   
    //getch();

    closegraph();
    return 0;
}
```

### 星空屏保 ###

屏幕保护程序只是一个全屏的动画程序然后改后缀成scr吗？错，显然不是。标准的屏幕保护程序，需要完成三个标准接口

这三个接口都是在命令行参数里接收的，所以你需要把你的主函数规范一下：

```
int main(int argc, char* argv)
```

然后，有三种不同的调用：

  1. 直接运行。这个时候argc == 1，是配置用的接口
  1. 带参数 "/s" 运行。这个时候argc == 2，并且argv[1](1.md)的内容是"/s" ，注意不要区分大小写，下同
  1. 带参数 "/p" 运行。这个时候argc > 2，并且argv[1](1.md)的内容是"/p"，并且argv[2](2.md)是一个窗口句柄，就是那个小预览窗口的，为10进制格式

于是，用新EGE接口，我们可以完成以下一个preinit函数（我拿星空程序做成屏保为例子）：

```
#include "graphics.h"
#include <time.h>
#include <stdio.h>
// 星星总数
#define MAXSTAR 2000

// 记录窗口宽高
int sc_w, sc_h;
int g_max;

struct STAR
{
    double x;
    int y;
    double step;
    int color;
}star[MAXSTAR];

STAR g_star[MAXSTAR];

// 初始化星星
void InitStar(int i)
{
    double speed = 0.006;
    star[i].x = 0;
    star[i].y = random(sc_h);
    star[i].step = randomf() * speed * 0.9 + speed * 0.1;
    star[i].color = (int)(star[i].step * 255 / speed + 0.5); // 速度越快，颜色越亮
    if (star[i].color > 255)
    {
        star[i].color = 255;
    }
    star[i].color = RGB(star[i].color, star[i].color, star[i].color);
}

// 移动星星
void MoveStar(int i, double dt)
{
    // 擦掉原来的星星
    putpixel((int)(star[i].x * sc_w), star[i].y, 0);
    // 计算新位置
    star[i].x += star[i].step * dt * 60;
    if (star[i].x > 1) InitStar(i);
    // 画新星星
    putpixel((int)(star[i].x * sc_w), star[i].y, star[i].color);
}

int preinit(int argc, char* argv[])
{
    setinitmode(INIT_NOBORDER | INIT_TOPMOST); // 指定初始化为无边框顶层窗口，并且窗口左上角坐标为(0, 0)
    g_max = MAXSTAR;
    if (argc < 2)
    {
        return -1;
    }
    else if (stricmp(argv[1], "/p") == 0) // 小窗口预览模式
    {
        HWND hwnd;
        sscanf(argv[2], "%d", &hwnd);
        attachHWND(hwnd);   // 新ege函数
        setinitmode(INIT_NOBORDER | INIT_CHILD | INIT_WITHLOGO); // 指定初始化为无边框子窗口
        g_max = 200;
        return 1;
    }
    else if (stricmp(argv[1], "/s")) // 非测试运行模式
    {
        return -1;
    }
    return 0; // 全屏模式
}

// 主函数
int main(int argc, char* argv[])
{
    int i, ms_x = -1, ms_y = -1;
    double dtime;
    int mode = preinit(argc, argv); // 记录初始化模式
    if (mode < 0)
    {
        MessageBoxA(NULL, "本屏幕保护程序无配置", "星空屏保", MB_OK);
        return 0;
    }
    randomize(); // 初始化随机种子
    initgraph(-1, -1); // 打开图形窗口，以全屏模式
    ShowMouse(mode);
    sc_w = getwidth();
    sc_h = getheight();

    // 初始化所有星星
    for(i = 0; i < g_max; i++)
    {
        InitStar(i);
        star[i].x = randomf();
    }
    // 绘制星空，按任意键或移动鼠标退出
    setfont(12, 6, "宋体");
    FlushMouseMsgBuffer(); // 清空鼠标消息，防对鼠标移动的判断产生干扰
    BeginBatchDraw();
    dtime = fclock();
    for(; kbhit(1) == 0; delay_fps(300)) //每秒画300帧，kbhit(1)是获取键盘任意键的消息，详见pdf
    {
        // 如果有鼠标消息
        if (MouseHit())
        {
            if (ms_x < 0)
            {
                MOUSEMSG msg = GetMouseMsg();
                ms_x = msg.x;
                ms_y = msg.y;
            }
            FlushMouseMsgBuffer();
            // 处理鼠标，移动超出范围就退出
            if (mode == 0) // 仅全屏模式才处理鼠标
            {
                int x, y;
                GetMousePos(&x, &y);
                x -= ms_x; y -= ms_y;
                if (x * x + y * y > 400) break;
            }
        }
        // 显示星星
        double dt = fclock() - dtime;
        dtime += dt;
        for(int i = 0; i < g_max; i++)
        {
            MoveStar(i, dt);
        }
        // 显示FPS（帧率）
        {
            char str[20];
            sprintf(str, "%8.2f FPS", GetFPS());
            outtextxy(0, 0, str); //显示fps
        }
    }
    EndBatchDraw();
    closegraph(); // 关闭图形窗口
    return 0;
}
```

### 数字雨 ###

### 变换线 ###

```
#include "graphics.h"
#include <stdio.h>
#include <time.h>
#include <stdlib.h>

int width = 640, height = 480;

struct point //定义点，包含坐标，速度
{
    double x;
    double y;
    double dx;
    double dy;
};

struct poly //定义多边形，包含点的个数，和点数组
{
    int n_point;
    point p[20];
};

struct polys //定义多边形队列组
{
    int n_poly;                 //多边形队列长度
    int color;                  //颜色
    int nextcolor, prevcolor;   //上一次的颜色，目标颜色
    int chtime, nowtime;        //过渡变化时间，当前时间
    int time;                   //距离一下次改变颜色的时间
    poly p[100];                //多边形数组
};

double rand_float(double dv, double db) //返回一个db 到 db+dv之间的随机浮点数
{
    return random(10000)*dv/10000 + db;
}

void movepoint(struct point* b) //根据点的速度属性移动这个点，如果移出屏幕则进行反弹计算
{
    double dv = 2.0, db = 1.0;
    double tw = width / 640.0, th = height / 480.0;
    if (b->x <0) b->dx = rand_float(dv, db) * tw;
    if (b->y <0) b->dy = rand_float(dv, db) * th;
    if (b->x >width) b->dx = -rand_float(dv, db) * tw;
    if (b->y >height) b->dy = -rand_float(dv, db) * th;
    b->x += b->dx;
    b->y += b->dy;
}

void movepoly(struct poly* p) //移动单个多边形，内部调用点的移动
{
    int i;
    for (i=0; i<p->n_point; ++i)
    {
        movepoint(&(p->p[i]));
    }
}

void movepolys(struct polys* p) //移动多边形队列，包含时间检测，颜色计算
{
    int i;
    for (i=p->n_poly-1; i>0; --i)
    {
        p->p[i] = p->p[i-1];
    }
    movepoly(p->p);
    ++(p->nowtime);
    if (--(p->time) <= 0)
    {
        p->prevcolor = p->color;
        p->nextcolor = HSVtoRGB(random(360), 1.0f, (float)rand_float(0.5, 0.5));
        p->time = random(1000);
        p->chtime = random(1000)+60;
        p->nowtime = 0;
    }
    if (p->nowtime >= p->chtime)
    {
        p->color = p->nextcolor;
    }
    else
    {
        double dr = p->prevcolor&0xFF, dg = (p->prevcolor>>8)&0xFF, db = (p->prevcolor>>16)&0xFF;
        double dt = 1 - p->nowtime / (double)(p->chtime);
        dr -= p->nextcolor&0xFF, dg -= (p->nextcolor>>8)&0xFF, db -= (p->nextcolor>>16)&0xFF;
        dr *= dt, dg *= dt, db *= dt;
        dr += p->nextcolor&0xFF, dg += (p->nextcolor>>8)&0xFF, db += (p->nextcolor>>16)&0xFF;
        p->color = ((int)dr) | ((int)dg<<8) | ((int)db<<16);
    }
}

void initpolys(struct polys* p, int npoly, int npoint) //初始化多边形队列组
{
    int i,j;
    p->n_poly = npoly;
    p->color = 0;
    p->time = 1000;
    p->prevcolor = p->color;
    p->nextcolor = HSVtoRGB(random(360), 1.0f, 0.5f);
    p->chtime = 1000;
    p->nowtime = 0;
    j = 0;
    p->p[j].n_point = npoint;
    for (i=0; i<npoint; ++i)
    {
        p->p[j].p[i].x = random(width);
        p->p[j].p[i].y = random(height);
        p->p[j].p[i].dx = (random(5)+1);
        p->p[j].p[i].dy = (random(5)+1);
    }
    for (j=1; j<npoly; ++j)
    {
        p->p[i] = p->p[i-1];
    }
}

void draw_poly(struct poly* p, int color) //绘制一个多边形
{
    int points[100];
    int i;
    for (i=0; i<p->n_point; ++i)
    {
        points[i*2  ] = (int)(p->p[i].x+.5f);
        points[i*2+1] = (int)(p->p[i].y+.5f);
    }
    points[i*2  ] = (int)(p->p[0].x+.5f);
    points[i*2+1] = (int)(p->p[0].y+.5f);
    setcolor(color);
    drawpoly(p->n_point+1, points);
}

void draw_polys(struct polys* p) //绘制多边形队列（只画第一个和最后一个，最后一个用于擦除）
{
    draw_poly(&(p->p[p->n_poly-1]),        0);
    draw_poly(&(p->p[          0]), p->color);
}

void drawfps() //绘制帧数
{
    static int  fps = 0, g_time;
    static char str[100] = "";
    setfillstyle(0x0);
    bar(0, 0, textwidth(str), textheight(str));
    setcolor(0xFFFFFF);
    outtextxy(0, 0, str);
   
    ++fps;
    if (clock() - g_time >= 500)
    {
        int nt = clock();
        sprintf(str, "帧率 %.2f fps", fps*1000.0 / (nt - g_time));
        fps = 0;
        g_time = nt;
    }
}

int WinMain()
{
    static struct polys p[10] = {{0}};
    int n_points[10] = {3,4,5,6,7};
    int n_poly[10] = {40,80,10,5,1};
    int n_polys = 2, i;
    int fps=0, n_time = 0;
    char str[100]={0};
    randomize();
    //图形初始化
    {
        int g = TRUECOLORSIZE, m = 0xFFFFFFFF;
        setinitmode(1, 0, 0);
        initgraph(&g, &m, "Mystify");
        width  = getmaxx();
        height = getmaxy();
    }
    //多边形对象初始化
    for (i=0; i< n_polys; ++i)
    {
        initpolys(&p[i], n_poly[i], n_points[i]);
    }
    setfont(12, 6, "宋体");
    //主循环
    for ( ; kbhit() != -1; delay_fps(60))
    {
        if (kbhit() > 0) //有按键按下就退出
        {
            break;
        }
        for (i=0; i< n_polys; ++i)
        {
            movepolys(&(p[i]));
        }
        for (i=0; i< n_polys; ++i)
        {
            draw_polys(&(p[i]));
        }
        drawfps();
    }
    closegraph();
    return 0;
}
```

### 拼图游戏 ###

### 俄罗斯方块 ###

## 其它资料 ##

  * 开发工具
    * [http://www.mingw.org/wiki/msys](MinGW.md)
      * [Msys-cn](http://code.google.com/p/msys-cn/)
      * [C\_Free](http://www.programarts.com/cfree_ch/index.htm)
        * [文档](http://www.programarts.com/cfree_ch/doc/help/hh_start.htm#UsingCF/CompilerSupport/MinGW/MinGW.htm)
      * [Code::Blocks](http://www.codeblocks.org/)
        * [Downloads Binaries](http://www.codeblocks.org/downloads/binaries)
        * [PATCH](http://forums.codeblocks.org/index.php?PHPSESSID=e6l7r5dmr646722r9el3uscsq5&board=20.0)
        * [中文包](https://translations.launchpad.net/codeblocks/trunk/+pots/codeblocks/zh_CN/+export)
    * VC6
  * 历史
    * BGI 图形库 for TC `Win-TC`
    * [Easyx](http://www.easyx.cn)
      * [vcgraphics](http://code.google.com/p/vcgraphics/)
    * `DEV-CPP`