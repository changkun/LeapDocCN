# 用户体验设计指南

我们建议你遵循下面的则例以确保你的应用具有良好的可用性。

<!-- The following user experience guidelines comprise our recommendations to ensure that your Leap-enabled application is easy to learn and use.-->

* **象征性的符号是很难学习并且记住的** 
  - 避免强迫用户去学习复杂的交互手势。

<!--Keep in mind that symbology can be difficult to learn and memorize.

Avoid forcing users to learn complex hand gestures to interact with your application.-->

* **相反，应从现实世界中的实际交互行为来吸取灵感** 
  - 近似自然的物理交互行为能够使得你的应用使用起来更加直观和自然，同时还能降低用户的学习成本。

<!--Instead, draw inspiration from physical interaction and real-world behaviors.

The more physically inspired interactions are, the less training a person needs and the more intuitive and natural your application feels.-->
  
* **不要被现实世界所限制，这个应用是你说了算** 
  - 交互并不一定需要总是和它原来的方式相同。它可以被想象为任何方式。为什么用户必须伸手去抓一个东西？而不是让这个东西自己过来？给它们一些『动力』！

<!--Don’t feel constrained by the limitations or inconveniences of the real-world — this is your world.

Interaction doesn’t have to be the way it has always been. It can be any way we imagine it to be. Why force the user to reach all the way out and grab an object? Why not have the object reach back? — Give them “the force”!-->
  
* **用户应该能够感觉到它们的意图被增强了而不是被限制或者掩盖了。**
  - 比如，当用户使用鼠标时，它们一般习惯自己的动作被放大（换句话说，他们不想为了把指针在屏幕上移动 10 英寸而真的把鼠标移动那么多）。对于手势的交互而言，增强或者夸张反馈能获得更好的效果。注意，有些人回避其他人更敏感，所以这些增强属性应该能够有用户来自己定义。

<!--The user should feel as if their intent is amplified rather than subdued or masked.

For example, users often like their movements to be amplified when using a mouse (i.e. they don’t need 10 inches of mouse movement to move 10 inches on screen). For gestural interactions, amplifying or exaggerating responses can have an even more positive result. Keep in mind that some people are more sensitive than others, so link this exaggeration to a sensitivity setting for users to modify this effect to their preference.-->
  
* **专注于对用户的行为给予反馈，他们得到的反馈越多，你软件的交互也就更加明确。**
  - 比如，用户需要明确知道他们确实是『按下』了一个按钮，当他们可以知道他们的手放在按钮的上方或者已经按下了多少的时候，交互的过程会更加高效。

<!--Concentrate on giving the user dynamic feedback to their actions. The more feedback they have, the more precisely they can interact with your software.

For example, the user will need to know when they are “pushing” a button, but can be more effective if they can see when they are hovering over a button, or how much they are pressing it.-->
  
* **屏幕视觉效果（比如手、工具或者反馈的表示）应该是简洁、功能导向的、无干扰的信息。**
  - 用户不应该被画面中的工具或环境影响而分神。装饰品也不应该分散干扰你主要想展示的内容。

<!--On screen visuals (such as representations of hands, tools, or digital feedback) should be simple, functional, and non-intrusive.

The user should not be distracted from the task by their tools or environment. Decoration should not distract from your purpose.-->
  
* **破坏性或者不可逆转的操作动作要被设计得比执行无破坏性操作动作更加刻意**
  - 惊喜的手势应该留给惊喜的操作。相反地，像关闭应用程序或删除文件这类不可逆转的操作应该对应一个更加刻意的动作。当不确定时，应该让用户进行反复确认，比如弹出一个提示框。

<!--Require more deliberate action for destructive or non-reversible acts than for harmless ones.

Subtle gestures should be reserved for subtle actions. Conversely, an act such as closing an application or deleting a file can be a non-reversible event requiring a more deliberate action. Double check with the user when unsure, such as a prompt for confirmation.-->
  
* **在导航和交互之间要有一个清晰明确的划分，除非两者都非常简单或者其中一个是自动控制（或者有辅助）的。在复杂的情况中混淆两者只会给用户带来困扰和迷惑。**
  - 比如，用户在一个 3D 环境中定位他的视角的同时再去移动另一个物体是非常困难的。但是，如果视角的改变是随着用户的移动自动变换，那移动另一个物体就简单多了。并且，在大量数据中导航时，用户希望自己的视角可以方便地变动；而在高亮某一部分数据时，他们则希望自己的视野能够被固定。

<!--Provide a clear delineation and specific sense of modality between acts of navigation and interaction, unless both are simple or one is handled automatically (or with assistance). Mixing the two in a complex situation can lead to confusion or disorientation.

For example, moving an object while having the user simultaneously position their viewing angle inside a 3D environment is inherently difficult. However, if the viewing angle moves automatically in response to the user’s movement, then working with the object is easier. Likewise, when navigating a large data set the user will want the view to move easily, but when highlighting a portion of the data the view should remain still.-->
  
* **总之，想想用户在没有任何指导和教程的情况下使用你的程序。**
  - 竟可能的使用户只需要利用他们的第一直觉就能作对。如果可以，多构建一些完成同样任务的不同途径。

<!--Overall, imagine that your user is faced with no instructions or tutorials on how to use your application.

Strive at all costs to make their first intuitive guesses the right ones. Where appropriate, create more than one proper way to do something.-->