OPCUA\_ModbusSerialMaster 
==========================

EdgePLUS一共有6个串口，COM1和COM2是RS232/RS4885/RS422可切换的多功能串口，COM3和COM4是RS232串口，COM5和COM6是RS485串口。下面以COM5为例进行说明，ModSim模拟从站设备，Device
IP表示设备站地址。

1、设备连接
-----------

根据出厂的EdgePLUS侧方的表格，COM5对应的是RS485通讯。EdgePLUS的16位孔接A，17位孔接B，20位孔接GND。将通讯线与电脑连接，通过ModSim从站模拟器来进行测试。

2、串口设置
-----------

将EdgePLUS的以太网口与电脑连接，打开EdgePLANT软件，通过“网络接口”搜索EdgePLUS，EdgePLUS和电脑需要在同一网段下才能搜索到。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image1.png" width="80%"/>


双击搜索到的模块，在功能栏中选择“接口配置”，在配置中点击“串口”进入串口设置界面，在“单模式串口”下选择“COM5”，可以在右侧属性栏中对COM5的属性值进行修改。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image2.png" width="80%"/>


修改完成后选择“配置”选项中的“下载模块配置”，跳出弹框信息“下载完成”之后重启模块，串口信息修改起效。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image3.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image4.png" width="80%"/>


在电脑端打开ModSim从站模拟器，点击“File”-“New”新建一个文件，然后点击“Connection”-“Connect”，选择通讯线与电脑连接的COM口。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image5.png" width="80%"/> 

在弹框中选择与EdgePLUS串口属性一致的选项，然后点击“OK”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image6.png" width="80%"/>


若连接成功，则窗口不会跳动“\*\*\*NOT CONNECTED!\*\*\*”的字样。

3、配置变量
-----------

在右侧功能栏中的“应用软件”里找到“数据采集”，点击“数据采集”出现数据采集服务-MDC\_OPCUA\_SERVER配置界面。在项目栏中右击“Project\_Default”新建一个组别。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image7.png" width="80%"/>


“组别名称”和“组别说明”可以任意修改，“组别启用”可以选择“是”和“否”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image8.png" width="80%"/>


右击组别新建一个连接，选择“Modbus串口主站”驱动，在右侧“连接配置”中可以修改“连接名称”和“连接说明”，可以选择是否启用连接。在“驱动参数”中，“通讯接口”选择EdgePLUS上使用的COM口，“Modbus站点地址”输入ModSim上对应的“Device
ID”的值。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image9.png" width="80%"/> 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image10.png" width="80%"/> 

右击连接新建一个标签，在右侧的“标签配置”栏可以修改“标签名称”、“标签别名”和“标签说明”，也可以选择是否启用标签。在“数据点位”栏里可以设置变量的数据类型和地址。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image11.png" width="80%"/> 

4、Modbus数据区
---------------

Modbus数据区域有离散输入Input（位）、离散输出Coil线圈（位）、输入寄存器Input
Register（字/两个字节）和保持寄存器Holding
Register（字/两个字节），对应ModSim的“MODBUS Point Type”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image12.png" width="80%"/> 

以1开头的数字对应离散输入Input数据区，以0开头的数字对应离散输出Coil数据区，以3开头的数字对应输入寄存器Input
Register数据区，以4开头的数字对应保持寄存器Holding Register数据区。

例如，想读取Modbus地址为40021的值，“数据类型”选择“有符号16位整数”，在“地址选择”的属性中，“数据区域”选择“保持寄存器”，“参考地址”输入“20”，参考地址是协议偏移地址，从0开始计算，要在Modbus地址的基础上减1，“字节次序设置”为“21”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image13.png" width="80%"/>


5、下载配置到EdgePLUS
---------------------

当所有变量都配置完成之后，点击“项目”下拉框，选择“下载模块配置”，在提示的弹框中选择“确定”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image14.png" width="80%"/> 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image15.png" width="80%"/>
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image16.png" width="40%"/>


读取模块配置：从EdgePLUS中读取配置文件到EdgePLANT

下载模块配置：把EdgePLANT中编写的配置文件下载到EdgePLUS

打开配置文件：从电脑上打开一个配置文件到EdgePLANT

保存配置文件：把EdgePLANT上编写的配置文件保存到电脑上

下载完成后，重启MDC\_OPCUA\_SERVER进程。跳出弹框点击“确定”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image17.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image18.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image19.png" width="40%"/>


6、客户端测试
-------------

EdgePLANT的“客户端测试”功能可以测试数据是否采集成功。在“应用软件”的“数据采集”界面的右上角，点击“客户端测试”即可。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image20.png" width="80%"/>


输入正确的服务器地址，点击“连接”，选择要读取的标签，可以在右侧的标签列表中看到“标签值”。读取到的标签值与ModSim从站模拟器中的值一致。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image21.png" width="80%"/>
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image22.png" width="80%"/>


7、查看日志
-----------

有两种方法可以查看驱动运行日志。

方法一：在“系统设置”的“软件管理”中找到运行的驱动名称“OPCUA\_ModbusSeriaMaster”，选中后双击或者点击右上角的“运行日志”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image23.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image24.png" width="80%"/>


方法二：在“应用软件”的“数据采集”界面，选中需要查看的驱动连接，右上角的“日志”标志亮起，点击“日志”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image25.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbuscom/image26.png" width="80%"/>

