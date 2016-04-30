# Device

属性：

* horizontal_view_angle
* vertical_view_angle
* range
* serial_number
* is_valid

方法：

* distance_to_boundary()

## ***class*** **Leap.Device**

Device 表示了一个物理连接的设备。

Device 类包括了一个特定连接的设备信息，如视野、设备 id和校准位置等。

注意，Device 对象是可以无效的，这意味着它不包含任何有效的设备信息，不与一个物理设备通信。测试有效性的方法是使用`Device.is_valid`属性。