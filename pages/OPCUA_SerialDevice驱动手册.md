**OPCUA\_SerialDevice功能简介**
=======================

OPCUA\_SerialDevice是凌顶自主研发的MDC\_OPCUA\_SERVER驱动。使凌顶Edge模块中的MDC\_OPCUA\_SERVER功能软件能够**无协议采集**所有串行设备数据。最大可采集不超过1024字节长度数据帧。若**有协议**则需要根据采集协议报文进行自我协议解析。

1.  **OPCUA\_SerialDevice运用场景**

> 常用于连接读码器、扫描枪等串行设备，获取串行设备数据、扫描次数统计、扫码长度计算等。配合Edge内部OPCUA\_DX\_SERVER功能软件，实现将采集到的串行设备数据传输到PLC、CNC设备中。

1.  **测试仪器准备**

<!-- -->

1.  KOB串口调试工具：本实验准备了一个KOB（RS422/485
    USB转串口工具），选用的是RS485模式，参数如下图所示

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image1.png" width="30%"/>
> 

1.  凌顶Edge边缘计算网关及配套软件:准备了一个凌顶[]{#_Hlk86827103
    .anchor}Edge[]{#_Hlk87024010 .anchor}PLUS来测试

    a.  EdgePLUS与KOB的接线如下图所示

> **EdgePLUS COM1 KOB**
>
> A+ ———— A+
>
> B- ———— B-
>
> GND ———— GND

1.  交换机、网线、电源模块、导线若干

<!-- -->

1.  **OPCUA\_SerialDevice使用方法**

<!-- -->

1.  参照Edge用户手册：[*https://tanghuang-liu.github.io/\#/*](https://tanghuang-liu.github.io/#/)熟练掌握EdgePlant的操作使用

2.  配置EdgePLUS模块的COM1的模式及相关参数进行配置，如下图所示

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image2.png" width="100%"/>
> 

1.  配置好COM1的模式及相关参数，点击“配置”-“下载模块配置”, 如下图所示：

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image3.png" width="100%"/>
> 

1.  删除模块内部无关配置，右键“Group1”-“删除组别”；右击“Project\_Default”-“新建一个组别”【注：由于小季这边是先搭建测试环境，在截图写手册的，没有操作这一步】

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image4.png" width="100%"/>
> 

1.  按照下图所示操作步骤，右键“Group1”-“新建一个连接”，选择合适驱动

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image5.png" width="100%"/>
> 

1.  选择合适驱动“串口设备”，修改配置，确认：如下图所示

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image6.png" width="100%"/> 

1.  点击“扫描枪”，“新建一个标签”；建立三个类型功能变量；如下图所示

    a.  ReadData功能：接受到串口数据内容（数据类型：字符串）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image7.png" width="100%"/>


a.  ReadDataLength：接受到串口数据内容的长度（数据类型：UInt16）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image8.png" width="100%"/>


a.  ReadCount：接受到串口数据内容的次数（数据类型：UInt16）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image9.png" width="100%"/>


1.  点击“项目下载”（临时保存一下）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image10.png" width="100%"/> 

1.  按下图步骤，“3处”软件，“添加开机自启”，下载配置，然后重启模块

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image11.png" width="100%"/> 

1.  实验效果：

    a.  第一次使用：串口工具发送（ABC123abcABC123abc!）：在EdgePlant自带的客户端测试功能中查看结果如下图:

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/osd/image12.png" width="100%"/>


1.  **应用加深**

<!-- -->

1.  参考：用Edge网关快速实现PLC获取扫描枪数据 提供MES交互接口——OPCUA
    Server：[*https://blog.csdn.net/qq\_36700574/article/details/121142915*](https://blog.csdn.net/qq_36700574/article/details/121142915)

