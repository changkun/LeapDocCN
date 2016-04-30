# 菜单设计指南

无论从菜单的易用性上还是只是整个程序的使用体验来说，向用户提供更直观的控制方式确保最终用户简单地进行控制，这对于开发完善的程序来说是极其重要的。更需要注意的是，很多时候这些人是第一次与你的软件进行互动，如果连在菜单上的简单交互体验都觉得非常混乱和费力，他们很可能就会开始不喜欢你的软件，甚至不会再使用你的软件了。所以菜单设计方面显然需要花更多的心思来做得更好！

<!--
Presenting users with intuitive options and controls – whether in the form of dedicated menus or simply throughout an experience – is an incredibly important component of developing deep applications and ensuring users ultimately feel in control. What’s more, many times these are the first interactions someone will have with your software. If a user’s initial experience with basic menu selection is confusing, frustrating or laborious, they might give up on the experience even before getting to the heart of your application. Clearly it’s worth spending some time to get this right!-->

尽管到目前为止很多已有的最佳实践可以应用到 LeapMotion 的开发上，但是这仍然没有让我们认为现在已经可以把桌面和移动菜单的交互转移到三维上，使用 LeapMotion 来进行所有的交互。所以当你在设计实现你的程序菜单时如果遇到交互问题，可以参考我们在开发者社区中建立的一些指南来增强您的应用程序的体验。

<!--
Yet while some existing best practices can be easily applied to Leap Motion-enabled apps, there’s no reason to think that what works best in current desktop or mobile menus will be immediately transferable to three dimensional interactions. In working through some of these issues ourselves and seeing solutions from developer community we’ve established a few guidelines to consider when implementing menus and settings into your app experiences.-->

## 菜单交互
使用菜单这个行为会在我们的应用程序中经常被重复，因为这是可能是所有功能连结的中介。因此菜单的交互需要让用户感觉更加自然和可靠，不需要让大多数用户为了操作去学习复杂的手势。为了避免用户使用菜单时出现沮丧情绪，宁可用最基础可靠的方法也不要用太过新颖独特的创意。

<!--Menu Interactions¶
Interacting with a menu are actions that are often repeated and likely to be gating factors to other functionality – so clearly they need to feel natural, be incredibly reliable and not require too much of the user in learning a new or complicated sign language. To avoid user frustration, it is always better to err on the side of basic yet stable approaches while continuing to refine more innovative ones.-->

## 菜单设计与布局

无论如何，你必须让你的菜单保持可用性、易读性和简单性的交互来适应你的作品。在不同的按钮中间必须留有空隙方便用户选择而不会很容易就错误点击到另一个。

<!--Menu Design and Layout¶
However you organize your menu to accommodate your experience and artwork, keep the usability, legibility and simplicity of interaction in mind. Be sure to space the buttons appropriately so that its easy for a user to select and tap a particular button without accidentally mis-tapping another.-->


![](../../images/menu_left_align_withInfo.jpg)
在这个示例菜单中你可以看到工作中的最佳实践应该是什么样子的。

1. 应该保持按钮足够大，易于辨认而且有一个高亮/被点击的状态
2. 高亮的按钮可以使用对比（反向）颜色使得按钮中的文字更加清晰易读
3. 退出按钮在菜单界面中应该特别容易被找到
4. 如果菜单使用了手势，那么这个手势必须非常简单，推荐是在区域中设置简单的敲击。

<!--In this example menu you can see a number of best practices at work.
Buttons are large, well organized and include a clear highlight/depressed state
Buttons use high contrast colors and the text/font are very legible
The Exit button is easily accessible and clearly indicated
Required gestures are displayed using easy to read iconography. The recommended gesture for menus is the touch-zone or “poke”.
-->

## 近邻高亮
另一种可以简化你的菜单设计的方法是你对菜单提供一种基于亲近而选择高亮的主题。这样做可以让离指针最近的菜单选项高亮，而不用必须将指针保持在选项上。在下面这个例子中，五个选项都被用外框线标明如何选择并使他们工作，当前用户的指针在左上角，所以左上角的选项亮了，这时候只需要执行点击手势 Play 按钮就会被触发，这种预测行为的办法可以降低用户的学习成本和挫败感。

<!--Proximity-Based Highlighting
Another way of simplifying the menu experience for your users is to provide a proximity-based highlighting scheme. This would highlight the closest item to the user’s cursor, without having to actually be over it. In the example below, the five possible actions are outlined to show how this might work. The user’s cursor is in the upper left quadrant so therefore the Play button is lit. Performing a tap gesture would activate the Play button. Anticipating what the user might want in these contexts can save time and eliminate frustration.-->

![](../../images/Menus_Zones.jpg)

把菜单布局和亲近高亮原则结合起来就能做出易于使用的菜单，但是通常来说这并不能做出好看并且易于让 LeapMotion 程序来使用的菜单。以下这些例子使用放射状或者网格状的菜单，希望能加深您对菜单交互这个课题的理解。这些例子使用点击（z轴）来作为激活交互方案。除此之外他们也包括了当每一个选项被选中时清晰的高亮反馈，当你在不同选项之间选择的时候会伴随着音效的提醒。最后用光标的变化来表示手指在z轴上的变化，让用户知道自己正在点击这个选项。

<!--Example of Proximity-Based Highlighting Scheme
Combining layout and proximity highlighting can result in some easy to use, not to mention great looking, Leap Motion enabled menus. Here are some examples using a radial and grid based menu generator we’ve provided to help you understand and interact with these concepts. These examples are using the tap-zone API (z-axis poke) for the activation method. Additionally they include clear visual feedback when highlighting and selecting each cell as well as audio feedback as you navigate from cell to cell and upon cell selection. Note the change in the cursor state as you translate the z-axis, showing your proximity to the “tap”.-->

## 放射状菜单
以下这些放射状菜单展现了如何快速把一堆选项用排列成戒指或者派这样的形状。当你需要选择这种菜单中的某一项的时候，你只需要将指标选择这块区域的某一点就能选中这一项，其实就是通过扩大选项面积来减少选中难度。而菜单最中央的区域你可以用来做为一个最重要的区域，也可以仅仅作为非选择区域。

你可以在[这里](https://developer.leapmotion.com/leapjs/examples/menu_radial_generator.html)找到在线示例。

<!--Radial Menus¶
The following radial menus show how you can navigate a number of items quickly and accurately by arranging their layout in a ring or pie. The movement required to target one of the cells is extremely slight which reduces the amount of latency and physical strain. The menus with a central cell could use that area for the most important item in the menu or as a “neutral zone”.

You can find the live code example here.-->

![5 Cell Radial Menu with Center Target](../../images/Radial_002.png)

![6 Cell Symmetrical Radial Menu](../../images/Radial_005.png)

![7 Cell Radial Menu with Center Target](../../images/Radial_006.png)

![4 Cell Symmetrical Radial Menu with 2 Columns](../../images/Radial_008.png)

## 网格菜单
和放射状菜单相似，使用列/排布局的栅格菜单也能让用户轻松选中对应的选项。

你可以在[这里](https://developer.leapmotion.com/leapjs/examples/menu_grid_generator.html)找到在线示例。

<!--Grid Menus¶
Similar to the radial menus, these grid based menus provide a simple method of accessing items with a minimum of effort, but using a column/row/grid based layout.

You can find the live code example here.-->

![](../../images/Grid001.png)

![](../../images/Grid002.png)

![](../../images/Grid003.png)

![](../../images/Grid005.png)

## 菜单访问与退出

有鉴于此，应该用简单易用的方式来设置访问菜单及退出应用程序的方法。

* 对于很多游戏和应用来说，当用户把手从检测范围内离开的时候，应该显示一个类似『Continue, Main Menu, Quit』的对话框
* 在菜单上，『返回』按钮，『设置』按钮应该做得很显眼
* 『Exit』 或者 『Quit』 之类的离开按钮同样应该做得显眼
* 离开按钮应该是彻底关闭程序，而不应该是返回菜单或者其他什么功能
* Mac上的 `Command-Q` 或者 Windows上的 `Alt-F4` 也要能起到退出的功能
* 同时要保持你的菜单对于鼠标来说也是可以访问的

<!--Menu Access and Exit
With this in mind, accessing these menus as well as exiting your application should be handled in the same, simple and foolproof manner.

For most games and applications, removing your hands from the field of view should pause the interaction and display a “Continue, Main Menu, Quit” dialog
Providing an explicit “Settings” or “Menu” button is another option
There should be an explicit “Exit” or “Quit” button
The Escape key should exit the app (on Mac and Windows)
The Command-Q (Mac) or Alt-F4 (Window) should also exit
May want to also make your menus accessible via mouse as well-->

![](../../images/DeadMotion.jpg)

第一人称射击游戏中，当用户从检测范围移开手的时候，应该像上图一样把所有运动和游戏参数暂停。

<!--The first-person shooter, Dead Motion Prologue, displays this menu when a user removes their hands from the field of view.-->

## 反馈，反馈，反馈！

无论你选择什么方式来让用户使用你的产品，你都要保证在用户操作的过程中有足够的提示和反馈来返回给用户，让用户知道自己的操作没有错误，从而不会在操作过程中因为过高的学习成本而产生沮丧情绪。用户在操作过程中必须立刻知道哪个元素是可以被交互的 —— 类似 『点击按钮来选择一篇文章』 这种简单的提示应该在菜单设计中加入。

<!--Feedback. Feedback. Feedback.¶
For any selection approach you utilize, giving users proper cues and feedback is integral to ensuring they feel in complete control. It should first be immediately clear what elements are interactive – and it never hurts to give users unobtrusive graphical or textual cues, e.g. a simple illustration and “Tap to select an article.”-->

一旦用户开始和菜单中的选项交互，流畅自然的视觉反馈和听觉反馈就应该贯穿着整个过程，比如鼠标在按钮上方时时应该马上高亮，滑块的滑动应当更加流畅等等。你对用户进行了更多的引导，他们就更容易完成各项操作。

<!--Once interacting with the element, it should respond fluidly with appropriate visual and auditory feedback. Buttons should be highlighted when hovered over and should respond with a “click” and indent as they are depressed; sliders should move freely; etc. The more information you can give to help orient the user and signal their selections, the easier it will be for them to complete each task.-->

![](../../images/FrogDissection_lit.jpg)

Frog Dissection 在按钮被选择时使用变大和变亮的方式来告诉用户按钮正在被选中。

<!--Frog Dissection uses large buttons that highlight and magnify when indicated and a simple z-axis poke gesture to tap/select.-->

![](../../images/SkyMuffins.jpg)

Sky Muffins 这个应用在你指向选择按钮的时候使用 『填充』 的方式来告诉用户按钮正在被选中。

<!--Sky Muffins uses buttons that “fill up” as you push forward on the z-axis. Filling the button selects it. This can be done quickly based on the speed of your push.-->

像文章前面建议的那样，这两个应用用了 Leap Motion Touch Zone 方面的 API 来处理点击按钮的相关反馈。关于这个API更多的内容，请查看[触摸仿真](../devguide/Leap_Touch_Emulation.md)和[ LeapMotion 的点击识别 API](http://adamleaps.tumblr.com/post/59536096658/recognizing-taps-with-the-leap-motion-api)这篇博文，而这篇文章主要告诉我们如何从一个开发者的角度来更好地使用这个API。

<!--As recommended previously, these two applications use the Leap Motion Touch Zone API to handle the button “tap”. For more on the implementation of this API, please review this section of our documentation and this excellent blog post from one of our developers on how to implement touch zones.-->