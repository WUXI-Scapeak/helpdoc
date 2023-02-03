**Edge模块**
==========
**SinumerikTcpClient西门子数控驱动**

**用户手册**

——无锡凌顶科技有限公司

> 发布者：IIOT物联网部门
>
> 发布日期：2020
>
> 发布版本：V1.0
>
> 公司网址：www.scapeak.com

第1章 功能和应用 
================

OPCUA\_SinumerikTcpClient驱动为Edge模块中专门针对Siemens
Sinumerik系列驱动系统开发的数据通讯驱动。

1.1 功能及特点 
--------------

1.支持西门子全系列数控系统，如840Dsl，828D，840D，810D，808D，802D等。

2.在如840Dsl等网口通讯的设备上，可达到数毫秒级别的数据通讯频率。在如840D等串口通讯的设备上，受串口通讯波特率的设置影响，一般可达数百毫秒级别的通讯频率。

3.可以同时读取数控系统NC及PLC的数据，分别用到对应的数据采集驱动。

1.2 软件依赖项 
--------------

MDC.OPCUA.SERVER

MDC
OPCUA服务器是所有Edge模块均内置的基础软件，用于实现设备数据采集（设备变量地址值读写）。Edge模块内置的OPCUA服务器是一个高性能OPCUA服务器，支持众多PLC和CNC设备的数据采集，并且采用多线程技术可同时服务于数十台设备和整条产线的数据采集。OPCU服务器内部的大部分通讯驱动经过精心设计和优化，实现了多变量智能分析合并采样和高速并发数据吞吐，目的是减少通讯次数、提高通讯效率。如在西门子SIMATIC-S7系列PLC和SINUMERIK系列CNC的以太网接口上能达到2\~6毫秒的稳定高速数据采集。

OPCUA服务器的采集变量数量没有任何限制，其所支持的设备连接数和产品系列以及我们提供给客户的特别授权相关。

第2章 硬件连接 
==============

2.1 网口设备连接 
----------------

如840Dsl、828D的网口通讯设备，只需要将设备和Edge模块连接到同一个局域网内，即可实现数据通讯。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image3.png" width="80%"/>


1.固定设备IP地址

修改设备IP地址，通常使用“公司网络”来连接工厂局域网。通常网口设备的网络设置在“菜单/调试/扩展键/网络”目录下。

注意，一般设备修改完IP地址，都需要重新启动设备才能够生效。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image4.png" width="80%"/> 

2.按照上述网络架构，将设备和Edge模块连接至同一局域网内。

3.确保Edge和设备网络通讯正常。使用EdgePlant软件，修改通讯参数和软件配置文件。详见本手册第三章。

2.2 串口设备连接 
----------------

如840D、810D的串口通讯设备，需要用到SCANET6-NCU工业以太网通讯处理模块，将设备的串口转换为网口，再将SCANET和Edge连接到同一个局域网内，即可实现通讯。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image5.png" width="80%"/>


1.安装SCANET模块到机床的MPI通讯接口。注意安装时候需要设备整体断电进行操作。

一般设备NCU模块上都会标有MPI接口标志，将SCANET
的S7总线接口接到MPI接口上。部分型号设备的MPI接口本身不供电或电压不稳定，建议给SCANET外接24V直流电，以保证通讯的稳定性。

若设备MPI接口已经被占用，可将原先的通讯线拔下，按上述方法先安装SCANET模块，再将原来的通讯先接到SCANET的扩展总线接口上。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image6.png" width="80%"/> 

2.按照上述网络架构，将SCANET和Edge模块连接至同一个局域网内。

3.确认模块安全安装，接线正确，设备重新上电。等待机床正常启动结束，查看SCANET上的BUS等（绿灯）是否常量，常量表示该接口可用。如果BUS灯闪烁，需要寻找其他MPI接口或PROFIBUS接口。

4.在浏览器中输入SCANET IP地址查看通讯状况。

确认S7总线状态为，当前波特率稳定，并能够检测到设备主从站地址。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image7.png" width="80%"/>


S7通讯协议模式一般为MPI主从站，S7总线波特率建议根据上述检测到的波特率设置为固定值。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image8.png" width="80%"/>


此处可以修改SCANET模块的IP地址、子网掩码、默认网关。

通讯目标PLC地址由槽号决定：该参数一般改成“是”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image9.png" width="80%"/>


5.确保Edge和SCANET网络通讯正常，使用EdgePlant软件，修改通讯参数和软件配置文件。详见本手册第三章。

第3章 EdgePlant配置 
===================

3.1 查看配置 
------------

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image10.png" width="80%"/>


将电脑网卡和Edge模块的任意网口连接，运行EdgePlant软件。根据所使用的网卡，搜索并连接到Edge模块。选择“应用软件”，选择“数据采集”，打开MDC\_OPCUA\_SERVER软件的配置。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image11.png" width="80%"/>


读取模块配置：读取Edge中现有配置文件

下载模块配置：将修改后的配置文件下载至Edge，每次修改配置后需要重新下载配置

打开模块配置：打开本地电脑上的xml 配置文件

保存模块配置：将当前xml 配置文件保存到本地电脑

3.2 软件运行 
------------

### 3.2.1 程序开机自启 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image12.png" width="80%"/>


在“系统设置/软件管理/数据采集”菜单下，找到“MDC\_OPCUA\_SERVER”软件，复制“文件路径”，打开“开机启动”菜单。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image13.png" width="80%"/>


新建配置，自定义“软件名称”，将上述复制的“文件路径”粘贴到“软件路径”，设置启动延时，通常为“1000毫秒”，最后下载配置。

此时每次重启Edge或者重新上电，系统启动后，MDC OPCUA
SERVER程序都会自动运行。

### 3.2.2 程序重启 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image14.png" width="80%"/>


选择“系统设置/系统信息/系统/进程列表”，在进程列表下找到“MDC\_OPCUA\_SERVER”进程，双击打开进程，可以选择“重启进程”或“终止进程”。

每次修改完软件配置并下载配置文件后，都需要按此步骤重新运行程序，新的配置文件才会生效。

3.3 新建设备连接 
----------------

1.在默认项目下，右键新建一个组别。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image15.png" width="80%"/> 

2.在设备组下，右键新建一个连接。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image16.png" width="80%"/>


3.选择“SINUMERIK.TCP客户端”驱动，此驱动专用于西门子数控系统通讯。

勾选左下角“添加驱动内部标签”，新建的连接会默认添加如下两个变量。

@DeviceOnline：设备通讯在线：检测设备是否正常连接通讯

@ItemUpdatedTime：标签更新时间：在同一连接下，所有变量刷新一次所需时间

连接名称：自定义一个设备名称

连接启用：选择是否建立和该设备的连接

IP地址：指定所需连接的设备的固定IP地址

通讯端口：西门子默认通讯端口102

访问终结点：通常网口设备使用“0D.03”，串口设备使用“03.03”

通讯超时：默认设置为 10000

通讯间隔：根据所需的采集频率来设置，一般无需修改。采集频率同样受设备本身的通讯性能限制

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image17.png" width="80%"/> 

4.选择新建的设备，右键新建一个标签。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image18.png" width="80%"/>


5.标签属性如下

标签名称：自定义一个变量名，支持中文

标签启用：选择是否读取该变量

写值使能：选择是否打开变量写入功能，注意需要该变量本身支持写入

标签说明：自定义对变量的描述说明

数据类型：选择完变量地址，会自动更新数据类型

地址选择：选择一个西门子NC变量进行读取。详细变量说明参考《第4章
变量配置说明》

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image19.png" width="80%"/>


3.4 查看数据 
------------

EdgePlant配置软件自带OPCUA Client功能，可以查看当前正在读取的数据。

在“应用软件/数据采集”页面下，选择右上角“客户端测试”，打开OPCUA客户端。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image20.png" width="80%"/>


选择默认搜索到的OPCUA
SERVER连接，在左侧列表中选择需要监控的变量节点，即可查看当前读取的变量值。打开“订阅”功能，可以持续刷新最新读取的数值。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image21.png" width="80%"/>


3.5 故障诊断 
------------

EdgePlant可以查看程序运行信息。若数据读取异常，可以通过调试信息来分析错误原因。

在“系统设置/软件管理”的软件列表中，找到使用的“OPCUA\_SinumerikTcpClient”驱动，在右侧“软件信息”菜单中，将“日志级别”修改为“调试”。打开“运行日志”查看软件运行信息。若无法判断错误原因，可将此运行日志复制出来，连同软件配置文件一同发送至凌顶，获取技术支持。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image22.png" width="80%"/> 

第4章 变量配置说明 
==================

4.1 变量说明 
------------

所有能够配置的西门子变量遵循西门子官方发布的变量手册。

### 4.1.1 变量参数 

在规定区域内，NC变量通常会以结构或数组结构的形式保存。因此访问NC变量时，必须在地址中进行以下参数的配置：

1.标签区域；2.模块；3.变量/列号；4.行号

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image23.png" width="80%"/>


### 4.1.2 变量区域 

NC变量是以数据块形式存在的，主要有以下数据区域：

N：含有适用于整个数控系统的所有变量。如：系统数据、G功能组

B：含有适用于运行方式组的所有变量。如：运行状态数据

C：含有适用于各个通道的所有变量。如：全局状态数据

T：含有适用于机床上刀具的所有变量。如：刀具补偿、刀具监控数据

A：包含适用于每根进给轴或主轴的机床数据和设定数据。

V/H：包含了适用于每个驱动的机床数据或作为服务参数的机床数据。

### 4.1.3 变量类型

NC变量通常可以分为三种：

1.单行NC变量

只由一个单独的值构成，读取该类变量需要配置标签区域、模块、列号。

该类变量通常包括了系统基本信息，状态数据，基本变量等。

2.多行NC变量

这种NC变量一般定义为一维数组，读取该类变量需要配置标签区域、模块、列号、行号。

该类变量需要修改行号，例如轴相关数据，不同的行号代表了不同的伺服轴。

3.多行及多列NC变量

这种NC变量一般定义为二维数组，读取该类变量需要配置标签区域、模块、列号、行号。

该类变量需要同时修改行号及列号，通常用于刀具相关的数据。

### 4.1.4 变量注意事项 

1.在西门子变量定义中，存在多个变量最终表示相同含义的情况，如果一个变量无法正常读取数据，可以换一个相同含义的变量尝试读取。

2.由于西门子数控系统版本、型号各不相同，越早的型号支持的变量类型越少，所以存在部分型号系统无法读取部分变量的情况。具体每个型号支持的变量类型，需要查阅对应型号的西门子官方变量手册。

4.2 配置说明 
------------

部分常用变量可以参考凌顶的《Siemens数控常用变量配置手册》，剩余变量需要查找《Siemens变量和接口信号》手册。

### 4.2.1 常用变量配置 

1.在凌顶提供的《Siemens数控常用变量配置手册》中，找到需要采集的变量。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image24.png" width="80%"/> 

2.根据“区域、模块、列号、行号”这四个参数，在EdgePlant软件中新建变量。手册中已给出对应变量的列号，可直接在参数中输入列号。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image25.png" width="80%"/>


3.手册中的“读写”参数为“r”表示该变量只读不可写，参数为“rw”表示该变量可读可写。根据变量属性选择“写值使能”，选择“是”则可以在OPCUA客户端中做数据反写。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image26.png" width="80%"/>


4.变量全部添加完成，下载配置文件，重启MDC\_OPCUA\_SERVER程序。详细步骤参考本手册《3.2
软件运行》。

5.对于部分变量，读取的值不同，代表不同含义，可以参考手册的备注信息。例如本例中的程序状态变量，1-5不同的值，表示不同的程序运行状态。

### 4.2.2 其他变量配置 

若凌顶提供的变量手册中，没有所需要的变量，则需要到西门子官方手册《Siemens变量和接口信号》中查找。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image27.png" width="80%"/>


1.在手册中找到需要读取的变量。确定区域和模块。

2.找到需要采集的变量，记住变量名称。

3.查看变量的读写属性。

4.查看变量是否支持多行号。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image28.png" width="80%"/>


根据上面查找到的变量属性，在EdgePlant软件中配置变量。注意由于从西门子手册中查找的变量无法确定其“列号”，需要在配置软件中的“变量”列表中去根据变量名称手动选择。

4.3 常用变量说明 
----------------

### 4.3.1轴相关变量 

例1：MCS机床坐标

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image29.png" width="80%"/>


按照手册中查找到的参数配置如下变量。由于该变量为多行NC变量类型，因此可以改变行号来读取不同轴的MCS机床坐标值。

行号为1，代表1号轴；行号为2，代表2号轴；以此类推。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image30.png" width="80%"/>


例2：轴负载率

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image31.png" width="80%"/>


按照手册中查找到的参数配置如下变量。由于该变量为多行NC变量类型，因此可以改变行号来读取不同轴的负载率。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image32.png" width="80%"/>


### 4.3.2刀具相关变量 

由于西门子数控系统的刀具管理中，存在“内部编号”变量，因此西门子刀具数据多为“多行多列NC变量”类型，需要同时配置行号及列号，才能正确读取刀具相关数据。

以下通过“刀具剩余寿命”变量，举例说明通用的西门子刀具数据读取方法。

1.首先读取系统中的刀具数量。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image33.png" width="80%"/>


2.接着读取刀具标识符（刀具名称）、刀具编号（内部编号）。上面读取的刀具数量可以指定以下两个参数的最大行号。相同行号读取的刀具名称和内部编号，对应的是同一把刀具。根据刀具名称，确定需要读取的刀具的内部编号。

> 例如：刀具名称为107的刀具，其内部编号对应为77。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image34.png" width="80%"/> 

3.根据上述读到的内部编号，指定需要读取的刀具的列号。此处的行号4，固定代表刀具剩余加工件数变量。

> 例如：要读取107号刀具的剩余加工件数，则指定这边的列号为77，行号为4。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image35.png" width="80%"/>


4.一般根据手册中配置的变量，都是刀具1号刀沿的数据。如果需要读取刀具2号刀沿数据，需要先读取以下变量，得知当前系统为每把刀具定义了多少个刀具寿命类型的数据。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/numerical/image36.png" width="80%"/>


5.假设以上变量读取值为9，那么当前系统中没把刀具定义了9个刀具寿命类型数据。若要读取2号刀沿的“剩余工件数”变量，需要指定变量的列号为77，行号为（2-1）\*9+4=13，即用公式“（刀沿号-1）\*9
+ 1号刀沿该变量行号”计算所需指定的行号值。

6.以上为读取刀具剩余寿命值的方法，其余刀具数据读取方式类似，但用到的变量以及指定的列号、行号都不相同，需要根据手册中的参数进行配置。

4.4 PLC变量 
-----------

若要读取数控系统中的PLC数据，则需要用到Edge模块的“西门子PLC以太网驱动”。

读取及配置方式，与连接普通西门子S7系列PLC的方式相同，可以参考凌顶提供的《西门子PLC驱动手册》

数控系统的PLC地址同样可以参考西门子官方手册《Siemens变量和接口信号》。
