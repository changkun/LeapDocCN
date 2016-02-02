# DeviceList

属性：

* [is_empty](#is_empty)

方法：

* [append()](#append)

## ***class*** **Leap.DeviceList**
DeviceList 继承自 Python 数组来表示一系列 Device 对象。

通过调用`Controller.devices()`来获得一个 DeviceList 对象。现在，这个列表只包含一个设备，无论你连了多少个设备到电脑上。

<!--The DeviceList class extends the Python array to represent a list of Device objects.

Get a DeviceList object by calling Controller.devices(). Currently, the list will only contain one device, no matter how many are attached to a computer.

-->

*New in version 1.0.*

----

### 构造函数
*classmethod* **DeviceList**()
构造一个设备的空列表。

<!--Constructs an empty list of devices.-->

*New in version 1.0.*

----

### 属性
#### is_empty
类型：boolean

返回一个列表是否为空。

<!--Reports whether the list is empty.-->

```python
if not controller.devices.is_empty:
    device = controller.devices[0]
```

*New in version 1.0.*

----

### 方法
#### append(*other*)
添加一个指定的 DeviceList 成员到 DeviceList 中。

参数：**other**(DeviceList) - 一个 DeviceList 对象包含 Device 对象会添加到 DeviceList 的末尾。

<!--Appends the members of the specifed DeviceList to this DeviceList.

Parameters:	other (DeviceList) – A DeviceList object containing Device objects to append to the end of this DeviceList.-->

*New in version 1.0.*