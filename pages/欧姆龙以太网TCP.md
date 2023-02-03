EdgPLUS通过以太网采集
================

第一章、功能和应用
================

> EdgePLUS有两路百兆以太网口，内置多种以太网驱动协议，适用于对市面上主流的PLC设备和CNC设备进行数据采集。本案例讲述的是用EdgePLUS对具有以太网口的OMRON
> PLC进行数据采集：
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image1.jpg" width="80%"/>
> 

第二章、通讯线连接
==============

1.  修改OMRON PLC的IP和EdgePLUS同网段，或者修改EdgePLUS的IP与OMRON
    PLC同网段，本案例中修改EdgePLUS的IP为1网段，连接EdgePLUS的ETH1口。

2.  修改电脑的IP为10网段，连接EdgePLUS的ETH0口。

第三章、EdgePLUS配置
================

3.1 EdgePLUS接口配置
---------------------

> a）根据OMRON PLC的
> IP用EdgePlant配置软件对EdgePLUS的以太网口进行配置（本次采用的以太网口是Eth1），使EdgePLUS的IP与OMRON
> PLC在同一网段。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image2.png" width="80%"/>
> 
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image3.png" width="40%"/>
> 

3.2 驱动选择
-------------

> a）点击“Project\_Default”，新建一个组别（组别名称可以自定义）
>
> b）点击“NewGroup\_0”，新建一个连接（连接名称可自定义），选用SYSMAC.TCP客户端驱动，进行数据采集，并修改驱动参数的IP地址为OMRON
> PLC的IP。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image4.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image5.png" width="80%"/>


3.3 变量配置
-------------

> a）点击连接“Connection\_0”，添加驱动标签

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image6.png" width="80%"/> 

> b）根据需要采集的PLC表地址，点击连接“Connection\_0”，新建一个标签（需要采集的变量配置），变量配置完成后，点击“项目”，下载模块配置。eg：\[采集地址：D264，类型：无符号整数\]

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image7.png" width="80%"/> 

> c）下载完成需要采集的变量配置之后，双击重启
> “MDC\_OPCUA\_SERVER”软件

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image8.png" width="80%"/> 

> d）若在“进程列表”中未找到“MDC\_OPCUA\_SERVER”软件，请到“软件管理”中右击“MDC\_OPCUA\_SERVER”添加为开机自启，然后点击“软件列表”，下载软件参数，最后重启模块。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image9.png" width="80%"/>


3.4. 查看数据
-----------------

> a）点击“客户端测试”——“连接”——“Connection\_0”，可查看采集到的数据是否与PLC中的值一致。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image10.png" width="80%"/>


第四章、PLC数据区采集说明
=======================

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omltcp/image11.png" width="80%"/>

