# ImageList

属性：

* [is_empty](#is_empty)

方法：

* [append()](#append)

## ***class*** **Leap.ImageList**
ImageList 类继承自 Python 数组用来表示一系列 Image 对象。用于分析当前帧的图像都包含在了列表当中。一个设备中有两副图像。左边相机的图像 id 为0，而右边的为 1。

通过调用 `Frame.images()`来获取一个 ImageList 对象。

<!--
The ImageList class extends the Python array to represent a list of Image objects. All images used to analyze the current frame are included in the list. There are two images from a single device. The image from the left stereo camera has the id of zero; the image from the right has the id of one.

Get a ImageList object by calling Frame.images().
-->

*New in version 2.1.0.*

----

### 构造函数
*classmethod* **ImageList**()
构造一个图像的空列表。

<!--Constructs an empty list of devices.-->

*New in version 2.1.0.*

----

### 属性
#### is_empty
类型：boolean

返回一个列表是否为空。

<!--Reports whether the list is empty.-->

*New in version 2.1.0.*

----

### 方法
#### append(*other*)
添加一个指定的 ImageList 成员到 ImageList 中。

参数：**other**(ImageList) - 一个 ImageList 对象包含 Image 对象会添加到 ImageList 的末尾。

<!--Appends the members of the specifed ImageList to this ImageList.

Parameters:	other (DeviceList) – A ImageList object containing Image objects to append to the end of this ImageList.-->

*New in version 1.0.*