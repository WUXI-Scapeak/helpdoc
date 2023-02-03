EdgPLUS通过USB采集
================

第一章、功能和应用
================

> EdgePLUS有两路USB串口，可以通过USB对PLC设备进行数据采集。当USB接口不够用的时候可以通过连接USB扩展器对接口进行扩展。本案例使用USB扩展器扩展出的USB口对OMRON
> PLC数据进行采集。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image1.jpg" width="80%"/>
> 

第二章、通讯线连接
==============

> 注：USB扩展器连接的设备过多时，需要对USB扩展器进行外部供电操作。

第三章、EdgePLUS配置
================

3.1 驱动选择
------------

> a）点击“Project\_Default”，新建一个组别（组别名称可以自定义）
>
> b）点击“NewGroup\_0”，新建一个连接（连接名称可自定义），选用SYSMAC.USB通讯驱动，进行数据采集，**需要指定USB端口路径**【当只需要用到EdgePLUS一个USB口直接采集设备数据时，才可以用自动检测】，操作如下：
>
> 点击进入USB设备选择。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image2.png" width="80%"/>
> 
>
> 点击更新按钮，在“连接到Edge模块的USB设备”下寻找OMRON-PLC所连接的USB口，找到后点击“确定”按钮。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image3.png" width="80%"/>
> 
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image4.png" width="80%"/>
> 

3.2 变量配置
-------------

> a）点击连接“Connection\_0”，添加驱动标签

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image5.png" width="80%"/> 

> b）根据需要采集的PLC表地址，点击连接“Connection\_0”，新建一个标签（需要采集的变量配置），变量配置完成后，点击“项目”，下载模块配置。eg：\[采集地址：D264，类型：无符号整数\]

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image6.png" width="80%"/> 

> c）下载完成需要采集的变量配置之后，双击重启
> “MDC\_OPCUA\_SERVER”软件

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image7.png" width="80%"/> 

> d）若在“进程列表”中未找到“MDC\_OPCUA\_SERVER”软件，请到“软件管理”中右击“MDC\_OPCUA\_SERVER”添加为开机自启，然后点击“软件列表”，下载软件参数，最后重启模块。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image8.png" width="80%"/>


3.3 查看数据
-------------

> a）点击“客户端测试”——“连接”——“Connection\_0”，可查看采集到的数据是否与PLC中的值一致。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image9.png" width="80%"/>


第四章、PLC数据区采集说明
=======================

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/omlusb/image10.png" width="80%"/>

