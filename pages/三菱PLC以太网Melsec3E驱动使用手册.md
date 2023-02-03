1、使用环境
===========

本手册陈诉用例应满足如下配置

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image1.png" width="80%"/>


2、驱动名称
===========

【FX系列Melsec3E模块以太网驱动】

3、硬件连接
===========

3.1 连接方式
------------

【以太网口】连接

3.2 连接步骤
------------

> 查询PLC模块的IP地址（FX5U-32M的IP为192.168.1.220，FX5U-32M的IP请看附录1）
>
> 将PLC通过以太网线连接到EdgePLUS的Eth1以太网接口（Eth1的IP为192.168.1.118）
>
> 将Eth0以太网接口（Eth0的IP为192.168.10.118）通过以太网线与电脑连起来
>
> USB线插入Debug口与电脑连通

硬件连接实物图如下图所示

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image2.png" width="80%"/>


4、配置标签采集指定变量（PLC数据区采集说明）
============================================

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image3.png" width="80%"/> 

> 点击【应用软件】——【数据采集】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image4.png" width="80%"/>


> 在【Project Default】中右击新建组别，在【NewGroup\_0】中新建一个连接

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image5.png" width="80%"/> 
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image6.png" width="80%"/>


> 选择【驱动库】——【三菱】——【Melsec3E.TCP客户端】驱动，修改连接名称、IP地址、通讯端口（查看PLC，请看附录1）、网络编号、PLC编号和站编号，此IP地址设置为PLC的IP，点击确认。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image7.png" width="80%"/>


> 在连接下新建标签开始OPCUA配置。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image8.png" width="80%"/>


> 右击添加驱动标签。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image9.png" width="80%"/>


> 修改【标签名称】、【数据类型】、【地址选择】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image10.png" width="80%"/>


举例：配置数据寄存器D0的有符号16位整数。

> 数据类型选择【有符号16位整数】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image11.png" width="80%"/>


> 数据区域选择【数据寄存器D】，参考地址选择【0】，勾选上【写值使能】。点击【确认】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image12.png" width="80%"/>


> 配置完标签后，点击【项目】——【下载模块配置】，将配置文件下载入EdgePLUS中

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image13.png" width="80%"/>


> 重启MDC\_OPCUA\_SERVER

点击【系统设置】——【系统信息】——【系统】，点击【进程列表】，双击运行【/opt/scapeak/MDC\_OPCUA\_SERVER/MDC\_OPCUA\_SERVER】，点击【重启进程】完成重启

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image14.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image15.png" width="80%"/>


若在“进程列表”中未找到“MDC\_OPCUA\_SERVER”软件，请到“软件管理”中右击“MDC\_OPCUA\_SERVER”添加为开机自启，然后点击“软件列表”，下载软件参数，最后重启模块。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image16.png" width="80%"/>


5、数据读写演示
===============

> 读取OPCUA客户端数据

点击【应用软件】——【数据采集】——【客户端测试】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image17.png" width="80%"/>


点击【连接】——【Project\_Default】——【Melsec3E】——【FX5U】——【D0】——【订阅】，显示读取的D0数据。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image18.png" width="80%"/>


> 修改OPCUA客户端数据

举例：目前读到的D0当前值为0，修改为100

双击D0标签值区域，修改为100，按Enter提交。观察编程软件D0当前值，发现已经由0修改为100，修改成功。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image19.png" width="80%"/> 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image20.png" width="80%"/>


附录1
=====

> 通过以太网将GXWorks3与PLC连接
>
> 硬件连接如下图所示

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image21.png" width="80%"/> 

> 打开【GXWorks3】
>
> 点击【工程】——【新建】——系列选择【FX5CPU】——机型选择【FX5U】——点击【确定】
>
> 点击【在线】——【当前连接目标】——【直接连接设置】——【以太网】——点击【确定】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image22.png" width="80%"/> 

> 点击【在线】——【从可编程控制器中读取】，选择【参数+程序】——【执行】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image23.png" width="80%"/>


> 选择【工程】——【参数】——【FX5UCPU】——【模块参数】——【以太网端口】，查看PLC的IP地址

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image24.png" width="80%"/>


> 点击【基本设置】——【对象设备连接配置设置】，可以查看SLMP通讯的端口号

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image25.png" width="80%"/> 
