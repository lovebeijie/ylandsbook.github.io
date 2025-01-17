[TOC]

# 自定义UI

《艾兰岛》新的UI系统相较于原来的UI系统而言，是一个巨大的飞跃！有过旧UI系统使用体验的开发者，大部分都对它没有任何好感，以致于在过去的一段时间里，开发者只能使用UI做简单的文字展示，做出来的UI比较简陋，也没有任何交互可言。

从0.14版本开始，新的UI系统被集成到了《艾兰岛》编辑器中。“灵活，快速和可视化”是新UI系统的特色。简单来说，对于开发者而言，就是有三个特点：效率高，效果好，易于使用。

* 创建速度快

  新UI系统秉承《艾兰岛》编辑器无需代码编写的特点，通过直接将逻辑块拖入场景，就可以简单而快速的在游戏中建立起一套UI界面。并且，新UI系统预定义了按钮，图片，文字输入框常用UI控件，使创建UI更加轻松。

  ![创建快速-预定义控件](img/%E5%88%9B%E5%BB%BA%E5%BF%AB%E9%80%9F-%E9%A2%84%E5%AE%9A%E4%B9%89%E6%8E%A7%E4%BB%B6.png)

* 直观、易于使用

  对于UI控件，开发者可以直接使用鼠标在UI视图里编辑它们的大小，位置。而无需编写任何代码，以“按钮”为例：

  ![按钮随意拖动位置](img/%E6%8C%89%E9%92%AE%E9%9A%8F%E6%84%8F%E6%8B%96%E5%8A%A8%E4%BD%8D%E7%BD%AE.gif)
  
  <center>上图：使用鼠标编辑UI控件的位置（以按钮为例）</center>
  ![按钮随意设置大小](img/%E6%8C%89%E9%92%AE%E9%9A%8F%E6%84%8F%E8%AE%BE%E7%BD%AE%E5%A4%A7%E5%B0%8F.gif)
  
  <center>上图：使用鼠标编辑UI控件的大小（以按钮为例）</center>
  
* 效率高效果好

  新UI系统经过一系列优化，能够被快速的绘制，此外能够自动兼容PC与移动平台，适配不同的屏幕分辨率。开发者只需要关注实现，而无需分散精力去优化兼容性与执行效率。

##  UI系统基础

通过前面的介绍，想必开发者已经对《艾兰岛》新推出的UI系统，有了一个简单的了解了。

从这里开始，将带着大家对新UI系统进行深入了解，内容涉及UI系统的基础，内容较为分散，主要分以下3个部分：

* UI逻辑，是UI系统提供的一个"**逻辑对象**"，用于承载UI系统提供的所有UI控件，而这些控件必须绘制在这个窗口上。
* 为UI控件提供在”逻辑对象“上的**可视化**布局支持，一个鼠标选中UI控件默认就打开UI控件的拖拉缩放功能（类似Unity3D中的Rect Tool工具）和 位置变换设置功能。
* 让UI控件在游戏试图中可见的UI组件

## UI逻辑

UI逻辑是《艾兰岛》新UI系统里的逻辑，UI系统中的所有UI控件都应该被”绘制“在它的上面，也就是说所有的UI控件都应该是它的子对象。

新UI系统同时提供了二个UI逻辑：**自定义HUD，自定义窗口**， 同时去掉了原来的**UI 面板**逻辑（之前做的UI，在0.14版本里能够继续使用）。自定义HUD与自定义窗口二者之间有相同的地方，也有区别：

1. 区别

   ![HUD与窗口区别](img/HUD%E4%B8%8E%E7%AA%97%E5%8F%A3%E5%8C%BA%E5%88%AB.png)

   * 在窗口编辑界面上，自定义HUD多了原声UI(道具快捷兰，提示信息)的占位提示

   * 自定义窗口 比 自定义HUD 多了 **按钮，文本输入框** 二个UI控件

   * 自定义窗口 左上角多了一个关闭按钮。

   * 脚本编辑中，事件数量不同：

     * 自定义HUD在脚本事件中，只有**游戏开始时，创建时，唤醒时**三个事件

     * 自定义窗口，脚本事件默认会多3个事件，并且根据窗口编辑时拖入UI控件的类型与数量，会在事件中增加对应的事件。下图是将所有UI控件都拖入自定义窗口后事件实例：

       ![自定义窗口事件区别](img/%E8%87%AA%E5%AE%9A%E4%B9%89%E7%AA%97%E5%8F%A3%E4%BA%8B%E4%BB%B6%E5%8C%BA%E5%88%AB.png)

2. 相同点

   * 逻辑对象属性一致
   * 都包含空节点，文本，图片UI控件，并且这三个控件在脚本事件中，都没有事件；
   * 对控件都支持可视化布局
   * UI绘制显示顺序逻辑都一致
   * UI的父节点子节点关系逻辑一致。

### 创建自定义UI/HUD

在**编辑器-->添加游戏逻辑**，用鼠标左键，首先点击**自定义HUD**或**自定义窗口**逻辑，再在游戏场景中点击，即可在游戏场景中创建。

![创建自定义UI](img/%E5%88%9B%E5%BB%BA%E8%87%AA%E5%AE%9A%E4%B9%89UI.png)

### UI编辑器

#### 编辑器布局

鼠标点击放置在场景中的”自定义窗口“或”自定义HUD“，依次点击：**对象属性--> 用户界面 编辑按钮**，将会打开UI自定义编辑界面，如下图：

![UI编辑器介绍](img/UI%E7%BC%96%E8%BE%91%E5%99%A8%E4%BB%8B%E7%BB%8D.png)

<center>自定义HUD与自定义窗口 的UI编辑界面整体布局一致，只在右上角控件数量，以及中间画布有所区别</center>
#### 画布坐标介绍

##### 画布中心点

UI编辑区域，即“画布”的中心坐标点位于画布中心。

![画布中心点](img/%E7%94%BB%E5%B8%83%E4%B8%AD%E5%BF%83%E7%82%B9.png)

##### 画布比例设置

在UI编辑界面，点做左上角**齿轮**按钮，打开编辑器设置，可调整屏幕比例，默认比例为16：9。

同时还可以设置是否显示画布右上角的关闭按钮。

![画布比例调整](img/%E7%94%BB%E5%B8%83%E6%AF%94%E4%BE%8B%E8%B0%83%E6%95%B4.gif)

### UI的绘制顺序

自定义HUD与自定义窗口中的UI控件在游戏运行时的绘制顺序，是与它们在**自定义UI管理器**视图里的排列顺序一致的。也就是说在UI编辑窗口的第一个子对象最先被绘制，接着绘制下一个子对象，一次类推，如下图所示：

![控件绘制顺序](img/%E6%8E%A7%E4%BB%B6%E7%BB%98%E5%88%B6%E9%A1%BA%E5%BA%8F.png)

<center>窗口子对象UI控件绘制顺序，与自定义UI管理器视图里的排列顺序一致</center>
==注意：如果两个UI控件发生重叠，那么先被绘制的UI控件，会被后绘制的UI控件覆盖==

为了修改各UI控件的绘制顺序，开发者可以采用以下方法：

**在定义UI管理器中鼠标右键菜单中选择向上或向下移动，改变它们在自定义UI管理器中的排列顺序** 

![变更绘制顺序](img/%E5%8F%98%E6%9B%B4%E7%BB%98%E5%88%B6%E9%A1%BA%E5%BA%8F.png)

### UI的绘制模式

UI的绘制模式，概念是来自Unity3D的UGUI种，UGUI一共有三种绘制模式（Render Mode），第一种就是Screen Space - Overlay，《艾兰岛》新UI系统的绘制模式就是Unity的第一种。

在此种绘制模式下，UI控件会被绘制在游戏场景的最上层，而且在UI编辑视图或游戏视图发生变化的时候，UI控件会随之一同发生改变，如下图所示。

![UI绘制模式](img/UI%E7%BB%98%E5%88%B6%E6%A8%A1%E5%BC%8F.png)

## UI控件的创建

### 向画布中添加组件

1. **在画布上添加一级控件**：

   * 在没有选中其他控件前提下，点击UI编辑器右上角控件按钮

   * 如果当前有选中某个UI控件，按”**ESC** 或者 鼠标单击**画布** 空白处，可取消选中。再单机右上角UI控件，可生成一级UI控件

     ![添加一级UI](img/%E6%B7%BB%E5%8A%A0%E4%B8%80%E7%BA%A7UI.gif)

2. **添加子组件**

   * 鼠标先选中某个UI控件，再生成新的UI控件，可在原来的UI控件下生成子控件。

   * 连续单机右上角UI控件按钮，新生成UI控件将会成为前一个UI控件的子控件。

   * 在画布中，鼠标单机右键，点击**添加新设置**，可直接在选中的UI控件下添加子UI控件

     ![添加子控件](img/%E6%B7%BB%E5%8A%A0%E5%AD%90%E6%8E%A7%E4%BB%B6.gif)

### 更改UI控件父子级关系

在自定义UI管理器中，鼠标右键单击UI控件，打开菜单，可将改变当前UI控件的父节点。

![更改UI控件父子级关系](img/%E6%9B%B4%E6%94%B9UI%E6%8E%A7%E4%BB%B6%E7%88%B6%E5%AD%90%E7%BA%A7%E5%85%B3%E7%B3%BB.gif)

### 删除组件

* 自定义UI管理器中或画布中，选中UI控件，按键盘“DELETE”键删除；
* 自定义UI管理器中或画布中，通过鼠标右键菜单中的删除选项删除；

## UI控件的布局

在UI编辑窗口上”绘制“的UI控件，除了要考虑前面介绍的绘制顺序外，还要考虑它们的布局问题，以及当布局不符合开发者预期时的处理方法。为此，本节介绍如何用鼠标快速操作UI控件的能力，以及通过可视化**位置布局**工具，让UI控件有了”自适应“的能力。

### 鼠标快速操作UI

新UI编辑界面，在**自定义UI管理器**列表中，或者在**画布**中，单机已创建的UI控件，即可在“**画布**”中直接操作UI控件。

对UI控件可以展开下列操作：

* **改变位置**：将鼠标置于UI控件矩形框的内部，按下鼠标左键任意拖动，即可改变UI控件的位置，如下图：

  ![改变控件位置](img/%E6%94%B9%E5%8F%98%E6%8E%A7%E4%BB%B6%E4%BD%8D%E7%BD%AE.gif)

* **改变大小**：将鼠标箭头移到UI控件边上，或四角的圆点，按下鼠标左键拖动，即可改变UI控件的大小，如下图：

  ![改变控件大小](img/%E6%94%B9%E5%8F%98%E6%8E%A7%E4%BB%B6%E5%A4%A7%E5%B0%8F.gif)

### 可视化位置布局工具

可视化位置布局工具是新UI系统为UI控件提供的新工具，该工具位于UI编辑器左侧，默认是关闭的，只在选中UI控件时打开。

![UI控件通用属性](img/UI%E6%8E%A7%E4%BB%B6%E9%80%9A%E7%94%A8%E5%B1%9E%E6%80%A7.png)

#### 基本属性

1. **位置X，位置Y：** 当前UI控件相对于父节点的坐标位置。当UI控件是一级控件时，则是相对于**画布**的相对位置

   如果UI控件是子控件，则子控件的X，Y值将永远是相对于父节点的坐标

2. **宽度，高**：用于表示UI控件的长和宽，1920*1080分辨率下的像素单位

#### UI控件可视化对齐与拉伸工具

![可视化位置布局工具](img/%E5%8F%AF%E8%A7%86%E5%8C%96%E4%BD%8D%E7%BD%AE%E5%B8%83%E5%B1%80%E5%B7%A5%E5%85%B7-1567424400200.png)

1. 对齐工具：绿色框部分

   此处预先定义了父节点的原点（0，0）点位置——即每个小正方形的 **×** 图形，开发者可以直接从预定义的白色小圆圈相对于×的位置，来设定UI控件位置。

   如下图，设置按键1右侧边沿中心点相对于父节点图案2右侧中心点距离100像素处。（这个解释也是优化过的，实际其实是将按键1的锚点设置到父节点右侧中间位置，并让按键1的中心点距离锚点100像素）

   此时按键1的位置是绝对与图案2的，因此，无论图案2在画布里的位置如何变化，按键1的位置将一直是相对与图案2靠右距离100像素处。

   ![对齐工具示例](img/%E5%AF%B9%E9%BD%90%E5%B7%A5%E5%85%B7%E7%A4%BA%E4%BE%8B.png)

   ![对齐设置](img/%E5%AF%B9%E9%BD%90%E8%AE%BE%E7%BD%AE-1567427599030.gif)

2. 拉伸工具：红色框部分

   在选中UI控件，点选其中要给拉升方块后，UI控件将自动拉升。此时，UI控件的属性也会变化：

   * 横向拉升，位置X，宽度属性替换为左，右属性。左、右数值表示UI控件在左右方向与父节点的距离。

     ![横向拉升](img/%E6%A8%AA%E5%90%91%E6%8B%89%E5%8D%87.png)

   * 竖直拉升，位置Y属性，高度属性替换为 顶部与底部属性。顶部与底部数值表示UI控件在上下方向与父节点的距离

     ![竖直拉升](img/%E7%AB%96%E7%9B%B4%E6%8B%89%E5%8D%87.png)

   * 完全拉升，位置X，位置Y，宽，高 替换为 左，右，顶部，底部属性。

     ![完全拉升](img/%E5%AE%8C%E5%85%A8%E6%8B%89%E5%8D%87.png)

==编者注：此工具借鉴了Unity3D的 Rect Transform组件中的锚点，中心点属性，但在这里，进行非常大的精简优化，初衷是避免开发者陷入锚点，中心点位置关系的理解。如果你有兴趣，可以去Unity3d文档里，翻阅UGUI关于锚点的相关说明==

## 可交互的UI组件

### 空节点控件

空节点控件，顾名思义，控件内在UI中默认时隐藏的，在交互过程中玩家不会看到这个控件。空节点控件主要用于将一类功能相同的控件归到一起，空节点起到分组的作用。

空节点控件像是一个容器，类似HTML里的div，GUI里的panel，UGUI里的Panel，可以包含其他的控件。

在布局上，可以先用空节点对UI界面进行区域划分，或者层级划分；并从整体上进行位置布局。然后所有功能相同的控件，都以空节点为父节点，进行绝对定位。这样，后续只需要拖动空节点，就能整个拖动一个功能组。

![空节点实例](img/%E7%A9%BA%E8%8A%82%E7%82%B9%E5%AE%9E%E4%BE%8B.gif)

### 文字控件

该控件用于向玩家显示不可交互的文本信息。玩家无法修改、删除其中的文本，只能从中了解信息。

注意：文本控件中值包含可见的文字，它的背景是透明的。

![文本控件属性](img/%E6%96%87%E6%9C%AC%E6%8E%A7%E4%BB%B6%E5%B1%9E%E6%80%A7.png)

**文本控件基本属性**

1. 水平对齐、垂直对齐：负责设置字符构成的段落的格式，
2. 尺寸：设置文本字符的大小
3. 颜色：设置文本字符的颜色
4. 文本：设置文字的颜色

注意：当文本内容超出文本控件宽度时，文本内容会自动折行，当文本内容行数超出文本控件高度时，文字内容将会溢出文本控件，不会将文本控件高度撑开。如果文本控件是子控件，也不会将父节点控件撑开。

### 图片控件

图片控件用于向玩家显示不可交互的图片信息，可作为UI界面的装饰。

新UI系统给图片预设了图片集，不能导入外部图片素材。

![图片控件属性](img/%E5%9B%BE%E7%89%87%E6%8E%A7%E4%BB%B6%E5%B1%9E%E6%80%A7.png)

**图片控件基本属性**

1. 图案：预设了99个图片，这些图片的默认尺寸是128×128像素

   ![图案](img/%E5%9B%BE%E6%A1%88.png)

2. 还原默认尺寸：可快速将拉升的图片尺寸还原为128×128

3. 颜色：设置图片颜色

4. 类型：用于设置图片显示类型，可选的属性值有：简单，切片，平铺，填充：

   * 简单：将直接显示图片空间中，默认情况下，如果图片控件的大小与图片大小不一致时，后者将经过拉申处理来符合前者的大小，但如果此时勾选了**锁定比例**，那么图片在经过缩放处理时，长宽的比例将保持恒定。
   * 切片：图片将被看作时由9个切片组成，而图片控件将只显示中间切片的边缘，若对整个UI做缩放操作时，四个角的切片将不做缩放操作。
   * 平铺：使整个图片填满整个图片控件，在保持图片尺寸不变的前提下不断重复，就像在铺地板砖一样。
   * 填充：此类型与简单相似，但提供了几种呈现方式。

   ![图片类型](img/%E5%9B%BE%E7%89%87%E7%B1%BB%E5%9E%8B.gif)

### 按钮控件

按钮控件用于向玩家提供在UI界面上进行点击交互的方式。默认提供的UI只有颜色填充，开发者需要在UI控件上添加相应信息，以说明按钮的作用，一般可以直接设置按钮图片，或者给按钮添加文本控件。

![按钮控件属性](img/%E6%8C%89%E9%92%AE%E6%8E%A7%E4%BB%B6%E5%B1%9E%E6%80%A7.png)

**按钮控件基本属性**

1. 图案：预设了99个图片，这些图片的默认尺寸是128×128像素

2. 可交互的：设置按钮是否可点击

3. 正常颜色，突出颜色，按下后颜色，禁用颜色：用于显示按钮状态提示，分别是点击前默认颜色，鼠标移上去的颜色，鼠标点击的颜色，禁用按钮颜色。

   ![按钮点击颜色状态](img/%E6%8C%89%E9%92%AE%E7%82%B9%E5%87%BB%E9%A2%9C%E8%89%B2%E7%8A%B6%E6%80%81-1567432737369.gif)

### 文本框控件

文本框控件用于向用户提供信息输入交互。

![文本框属性](img/%E6%96%87%E6%9C%AC%E6%A1%86%E5%B1%9E%E6%80%A7.png)

**文本框控件属性**

1. 可交互：设置文本输入框是否可用

2. 正常颜色，突出显示颜色，按下后颜色，禁用颜色，输入颜色，占位符颜色：分别对应文本框输入前，鼠标移上去获得焦点，鼠标点击时颜色，禁止使用颜色，输入时的颜色。

3. 输入文本：默认文本

4. 占位符文本：提示性文本

   ![文本输入演示](img/%E6%96%87%E6%9C%AC%E8%BE%93%E5%85%A5%E6%BC%94%E7%A4%BA.gif)
