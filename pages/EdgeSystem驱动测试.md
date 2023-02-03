EdgeSystem驱动测试
==================

1、搜索模块
-----------

在EdgePlant软件上搜索模块，“网络接口”处选择正确的网段后会在下方的菜单栏中出现已连接的模块。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image1.png" width="60%"/>}

2、配置文件
-----------

打开“应用软件”的“数据采集”页面；

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image2.png" width="80%"/>


在左侧的项目栏中依次新建组别、连接、标签，新建连接时选择“Edge.系统集成”，然后依次添加标签；

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image3.png" width="80%"/>


把配置下载到模块中，点击项目栏左上角的“项目”下拉菜单，选择“下载模块配置”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image4.png" width="80%"/>


3、开机启动
-----------

下载完成后，在系统设置的软件管理页面中，把MDC\_OPCUA\_SERVER设为开机自启。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image5.png" width="80%"/>


4、查看日志
-----------

重启模块，查看MDC\_OPCUA\_SERVER的运行日志，在软件管理列表中选中MDC\_OPCUA\_SERVER，然后点击上方的运行日志；

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image6.png" width="80%"/>


日志没有报错信息，各个标签都添加成功，MDC\_OPCUA\_SERVER正在运行中，说明OPCUA正常。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image7.png" width="80%"/>


5、查看数据
-----------

用dataFEED软件查看OPCUA采集的数据。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image8.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image9.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/edgesys/image10.png" width="80%"/>

