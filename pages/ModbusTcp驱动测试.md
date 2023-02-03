OPCUA\_ModbusTcpClient 
=======================

EdgePLUS有2个以太网口，Eth1和Eth2。Eth1的默认IP为192.168.1.118，Eth2的默认IP为192.168.10.118。测试中用ModSim模拟从站设备，Device
IP表示设备站地址。

1、设备连接
-----------

EdgePLUS的网口，一个连接设备，进行数据采集，一个连接电脑，通过EdgePLANT进行配置。要求每个网口和连接的设备网段一致。

2、修改IP地址
-------------

将EdgePLUS的一个以太网口与电脑连接，打开EdgePLANT软件，通过“网络接口”搜索EdgePLUS，EdgePLUS和电脑需要在同一网段下才能搜索到。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image1.png" width="80%"/>


有两种方式修改EdgePLUS的IP地址。

方法一：在EdgePLANT的左下方有“模块属性”栏直接对两个以太网接口配置进行修改，修改完成后点击“重启模块”按钮将模块进行重启，修改后的IP重启后生效。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image2.png" width="80%"/>


方法二：在“系统设置”的“接口配置”中，有以太网配置界面，点击“以太网LAN”，找到需要修改的以太网接口，然后在右侧的属性栏中进行修改。修改完成后点击左上角“配置”下拉框，选择“下载模块配置”，跳出弹框点击“确定”。重启模块后IP修改生效。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image3.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image4.png" width="80%"/> 
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image5.png" width="40%"/>


读取模块配置：从EdgePLUS中读取配置文件到EdgePLANT

下载模块配置：把EdgePLANT中编写的配置文件下载到EdgePLUS

打开配置文件：从电脑上打开一个配置文件到EdgePLANT

保存配置文件：把EdgePLANT上编写的配置文件保存到电脑上

3、配置变量
-----------

在右侧功能栏中的“应用软件”里找到“数据采集”，点击“数据采集”出现数据采集服务-MDC\_OPCUA\_SERVER配置界面。在项目栏中右击“Project\_Default”新建一个组别。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image6.png" width="80%"/>


“组别名称”和“组别说明”可以任意修改，“组别启用”可以选择“是”和“否”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image7.png" width="80%"/>


右击组别新建一个连接，选择“Modbus.Tcp客户端”驱动，“IP地址”填写连接设备的IP，“站点地址”对应ModSim上的“Device
Id”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image8.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image9.png" width="80%"/>


右击连接新建一个标签，在右侧的“标签配置”栏可以修改“标签名称”、“标签别名”和“标签说明”，也可以选择是否启用标签。在“数据点位”栏里可以设置变量的数据类型和地址。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image10.png" width="80%"/> 

4、Modbus数据区
---------------

Modbus数据区域有离散输入Input（位）、离散输出Coil线圈（位）、输入寄存器Input
Register（字/两个字节）和保持寄存器Holding
Register（字/两个字节），对应ModSim的“MODBUS Point Type”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image11.png" width="80%"/> 

以1开头的数字对应离散输入Input数据区，以0开头的数字对应离散输出Coil数据区，以3开头的数字对应输入寄存器Input
Register数据区，以4开头的数字对应保持寄存器Holding Register数据区。

例如，想读取Modbus地址为40021的值，“数据类型”选择“有符号16位整数”，在“地址选择”的属性中，“数据区域”选择“保持寄存器”，“参考地址”输入“20”，参考地址是协议偏移地址，从0开始计算，要在Modbus地址的基础上减1，“字节次序设置”为“21”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image12.png" width="80%"/>


5、下载配置到EdgePLUS
---------------------

当所有变量都配置完成之后，点击“项目”下拉框，选择“下载模块配置”，在提示的弹框中选择“确定”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image13.png" width="80%"/> 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image14.png" width="80%"/>
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image15.png" width="40%"/>


下载完成后，重启MDC\_OPCUA\_SERVER进程。跳出弹框点击“确定”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image16.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image17.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image18.png" width="40%"/>


6、客户端测试
-------------

EdgePLANT的“客户端测试”功能可以测试数据是否采集成功。在“应用软件”的“数据采集”界面的右上角，点击“客户端测试”即可。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image19.png" width="80%"/>


输入正确的服务器地址，点击“连接”，选择要读取的标签，可以在右侧的标签列表中看到“标签值”。读取到的标签值与ModSim从站模拟器中的值一致。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image20.png" width="80%"/>
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image21.png" width="80%"/>


7、查看日志
-----------

有两种方法可以查看驱动运行日志。

方法一：在“系统设置”的“软件管理”中找到运行的驱动名称“OPCUA\_ModbusTcpClient”，选中后双击或者点击右上角的“运行日志”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image22.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image23.png" width="80%"/>


方法二：在“应用软件”的“数据采集”界面，选中需要查看的驱动连接，右上角的“日志”标志亮起，点击“日志”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image24.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/modbustcp/image23.png" width="80%"/>

