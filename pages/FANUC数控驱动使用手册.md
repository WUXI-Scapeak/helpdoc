FANUC数控驱动
==========
第1章 概述
==========

边缘计算网关Edge模块主要执行数据收集和现场级数据策略(详情请查看公司官网关于Scaedge的介绍 https://www.scapeak.com/)。
发那科CNC以太网驱动OPCUA\_FocasTcpClient是安装在Edge模块内的通过OPCUA服务器采集发那科CNC数据的驱动。

1.1 软件介绍
------------

软件名称：MDC\_OPCUA\_SERVER（一般出厂默认安装）

软件说明：OPCUA数据采集服务

软件文件夹路径：/opt/scapeak/MDC\_OPCUA\_SERVER

软件路径：/opt/scapeak/MDC\_OPCUA\_SERVER/MDC\_OPCUA\_SERVER

Edge模块内置凌顶自主开发的 OPCUA
服务器MDC\_OPCUA\_SERVER，可以集成各种数据采集的驱动，发那科CNC以太网驱动。

1.2 驱动介绍
------------

驱动名称：OPCUA\_FocasTcpClient

驱动说明：OPCUA驱动发那科CNC以太网

驱动文件夹路径：

/opt/scapeak/MDC\_OPCUA\_SERVER/protocols/FocasTcpClient

驱动路径：

/opt/scapeak/MDC\_OPCUA\_SERVER/protocols/FocasTcpClient/libFocasTcpClient.so

第2章 硬件连接
==============

2.1 模块供电
------------

Edge模块供电（手册使用的是EdgePLUS，以下统一使用EdgePLUS）：

EdgePLUS可以使用24V直流电源供电，提供24V接线端子，或者使用5V电源，可以用电脑供电，USB线插在Debug口。一般推荐使用24V接线端子供电更加稳定。

2.2设备连接
-----------

1.查看、设置和修改FANUC数控系统IP地址：

以FANUC0i-TC系列为例：在FANUC数控面板上，SYSTEM按键——向右扩展找到ETHPRM——(OPRT)——PCMCIA。可以查看IP地址或者修改设置IP地址。

不同系列FANUC数控系统的IP地址查找可能有所差异，请您查看相关FANUC手册。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image4.jpeg" width="80%"/>



2.若FANUC数控系统有网口，使用以太网直接连接，如果没有网口则需要购买PCMCIA卡转成以太网：

一般用到FANUC数控系统、EdgePLUS、计算机和网线、PCMCIA卡。EdgePLUS有两个网口。例如：按照图示连接硬件。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image5.png" width="80%"/>



其中，Edge有两个网口，分别为Eth0和Eth1，这两个网口的可由用户设置IP地址，但是不能设置为同一网段。如果如图所示连接，则FANUC数控需要和Eth1在同一网段；计算机需要和Eth0在同一网段。

例如：根据FANUC数控的IP地址和计算机IP地址修改Edge的网口配置，包括IP地址、默认网关和子网掩码。

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image6.png" width="40%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image7.png" width="80%"/>

> 

3.使用交换机连接

如果您用交换机连接硬件，Edge只使用一个网口例如：Eth1,可以如下图所示进行连接。IP地址配置如下：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image8.png" width="80%"/>



第3章 EdgePLUS配置
==================

3.1 EdgePLUS的IP地址配置
------------------------

1.打开EdgePlant配置软件，在计算机网口的IP地址下搜索Edge模块。

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image9.png" width="60%"/>
}
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image10.png" width="80%"/>

> 

2.修改IP地址

> 如果您需要修改IP地址，可以按照您的需求修改IP地址，可参考硬件连接。修改完成先点击下载按钮再点击重启按钮。重启完成的标志是SYS灯重新常亮。
>
> 注意：您还可以选择硬件断电重启，即给EdgePLUS断电重启。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image11.png" width="40%"/>

> 

3.2 EdgePLUS配置变量
--------------------

1.选择应用软件——数据采集，Project\_Default右击新建一个组别。

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image12.png" width="80%"/>
}

2.组别名称：可以自定义修改。

组别启用：是，表示运行MDC\_OPCUA\_SERVER时，该组别变量有效。如果选择否，则表示该组别无效，所有变量均不读取。

如果配置文件中有组别不想使用，您可以右击该组别，选择删除，也可以组别启用选择否。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image13.png" width="80%"/>



3.新建连接，右击该组别（FANUC），新建一个连接

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image14.png" width="80%"/>

> 

4.选择连接驱动FANUC-CNC.TCP客户端。

> 按照如下配置驱动参数：
>
> 1)连接名称：可自定义修改；
>
> 2)连接启用：是（表示采集该连接配置的变量），否（表示不采集该连接的变量）；
>
> 3)驱动协议：发那科CNC以太网驱动；
>
> 4)驱动接口：Ethernet；
>
> 5)IP地址：发那科CNC的IP地址，可修改；
>
> 6)机床路径：8193；
>
> 7)通讯超时（毫秒）：设备连接超时，如果EdgePLUS与设备（FANUC数控）没有连接上，那么间隔多少毫秒重新尝试连接；
>
> 8)通讯间隔（毫秒）：所有变量读取一遍后的延时时间，设置为0就是最快速度读取。
>
> 9)勾选添加内部驱动就是添加设备（FANUC数控）是否在线和变量更新时间两个标签。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image15.png" width="80%"/>

> 
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image16.png" width="80%"/>

> 

5.新建标签：右击该连接，新建一个标签。您要采集每个变量都用一个标签来表示。

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image17.png" width="80%"/>

> 
>
> (1)根据要采集的变量的地址，分为主区域和子区域。
>
> (2)主区域包括：控制轴/主轴相关数据；程序相关数据；文件相关数据；刀具寿命管理数据；PMC可编程控制器数据区；系统相关数据。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image18.png" width="40%"/>

> 
>
> (3)每一个主区域包含相应子区域：
>
> 1)控制轴/主轴相关数据
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image19.png" width="60%"/>

> 
>
> 2)程序相关数据
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image20.png" width="60%"/>

> 
>
> 3)文件相关数据
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image21.png" width="60%"/>

> 
>
> 4)刀具寿命管理数据
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image22.png" width="60%"/>

> 
>
> 5)PMC可编程控制器数据区
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image23.png" width="60%"/>

> 
>
> 6)系统相关数据
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image24.png" width="60%"/>

> 
>
> (4)标签属性。
>
> 标签属性由每个区域决定，其中值可写和数据类型是每个标签都存在的属性。
>
> 1)值可写表示该变量能读能写，值可写属性可修改为是，其余变量区域默认为否，并且不可修改（灰色不可修改）。对于发那科CNC来说，目前只有PMC可编程控制器数据区和文件相关参数的轴相关参数可读可写。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image25.png" width="60%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image26.png" width="60%"/>

> 
>
> 2)数据类型：大部分数据区域的数据类型都是固定的，取决于该变量本身，不可修改（灰色不可修改）。只有少部分区域的数据可以选择变量类型。包括：文件相关数据的轴相关参数值；文件相关数据的轴相关设定值；PMC可编程控制器数据区；系统相关数据的轴相关诊断号（可选择8/16/32位整数或者32位浮点数）。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image27.png" width="60%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image28.png" width="60%"/>

> 
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image29.png" width="60%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image30.png" width="60%"/>

> 
>
> 对于PMC可编程控制器数据区如果指定位号，请选择数据类型为位值。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image31.png" width="60%"/>

> 
>
> 3)其他属性：其他属性取决于区域自身，常见属性包括轴号，刀具号等。可根据所选择的区域配置。
>
> (5)第一个标签建立成功
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image32.png" width="80%"/>

> 
>
> 具体变量配置还可以参照我公司提供的配置表。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image33.png" width="80%"/>

> 

6.测试过程中，为发那科CNC配置了如下变量。

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image34.png" width="60%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image35.png" width="60%"/>

> 
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image36.png" width="60%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image37.png" width="60%"/>

> 
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image38.png" width="60%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image39.png" width="60%"/>

> 
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image40.png" width="60%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image41.png" width="60%"/>

> 

3.3下载配置到EdgePLUS中
-----------------------

1.在项目——下载配置模块。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image42.png" width="80%"/>



<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image43.png" width="80%"/>



2.提示完成。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image44.png" width="80%"/>



3.4 启动MDC\_OPCUA\_SERVER
--------------------------

1.系统设置——系统——系统信息——进程列表。

> 如果您看到有/opt/scapeak/MDC\_OPCUA\_SERVER/MDC\_OPCUA\_SERVER进程，您可以双击重启该进程。

修改配置变量之后也需要重启进程。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image45.png" width="80%"/>



<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image46.png" width="80%"/>



> 如果您在进程列表中没有看到MDC\_OPCUA\_SERVER的进程，您需要将MDC\_OPCUA\_SERVER加入开机启动中。
>
> 选中该软件右击——添加开机启动。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image47.png" width="80%"/>
}
>
> 配置完成，点击下载配置，就可以将MDC\_OPCUA\_SERVER设置为开机启动。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image48.png" width="80%"/>

> 
>
> 2.然后重启EdgePLUS，您可以选择断电重启，也可以通过EdgePlant软件选择模块重启，如果重启成功，EdgePLUS的指示灯POW和SYS常亮。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image49.png" width="40%"/>

> 
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image50.jpeg" width="40%"/>

> 
>
> 3.重新搜索模块，您可以在系统设置——系统信息——进程列表看到MDC\_OPCUA\_SERVER的进程。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image51.png" width="80%"/>
}

3.5 OPCUA客户端展示
-------------------

1.读取：在应用软件——数据采集——客户端测试，软件会自动获取服务器地址。

> 1)点击连接，可以搜索到该FANUC数控，点击FANUC，可以看到配置的变量的数据。
>
> 2)点击订阅，数据会实时刷新。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image52.png" width="80%"/>



<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image53.png" width="80%"/>



2.写入：配置变量选择写值使能为是的变量可以写入。例如变量：C0无符号8位整数，值可写:是

> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image54.png" width="40%"/>

> 
>
> 1)您可以用客户端测试写入，或者您开发的OPCUA客户端软件进行写值。示例：将9值改为8。
>
> 2)修改方法：直接双击该标签值，写入新值
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image55.png" width="80%"/>

> 
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image56.png" width="80%"/>

> 

第4章 变量介绍
==============

4.1 变量区域说明
----------------

请查看我公司提供的FANUC数据整理表。有相关主区域、子区域和变量类型的介绍。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image57.png" width="80%"/>



4.2 常见PMC变量说明
-------------------

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image58.png" width="80%"/>



4.3 常见参数说明
----------------

> 注意：不同类型FANUC数控的参数可能有所差别，有些参数可能部分机床类型没有，请查看具体型号FANUC数控的参数。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image59.png" width="80%"/>
}

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fanuc/image60.png" width="80%"/>



如您需要帮助请联系无锡凌顶科技有限公司，IIOT物联网部门。咨询电话：400-8544-418、0510-85915898。邮箱：<public@scapeak.com>。官网：<https://www.scapeak.com/>
