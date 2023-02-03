

![image-20200729090535309](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200729090535309.png)

三菱系列驱动
====
# 1.FX系列
## 1)三菱PLC串口ProgSerial驱动
### 1、使用环境


本手册陈述用例应满足如下配置

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image1.png" width="80%"/>


### 2、驱动名称

【FX系列编程口通讯】

### 3、硬件连接


#### 3.1连接方式


【串口】连接

#### 3.2连接标准

三菱Fx的串口连接标准有【RS-232】、【RS-485】

#### 3.3连接步骤

> 取下三菱PLC串口扩展模块

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image2.png" width="80%"/>


> 观察串口扩展模块的连接标准

FX3U-48MR的串口连接标准为【RS-232】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image3.png" width="80%"/>


> 将通讯线与接线端子连接，并插入串口扩展模块中（如果是九针接线端子，接2，3，5口）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image4.png" width="40%"/>
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image5.jpeg" width="40%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image6.png" width="80%"/>


> 根据EdgePLUS接线说明，通讯线连接EgdePLUS的接线端子，通讯线接线与PLC一一对应。
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image7.png" width="80%"/>
> 

注：EdgePLUS的COM1与COM2口是两个RS232/485可切换的串口，COM3和COM4是两个RS232串口。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image8.jpeg" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image9.png" width="80%"/>


硬件连接实物图如下图所示
> USB线插入Debug口与电脑连通，以太网线插入Eth0口（ip地址：192.168.10.118）与电脑连通

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image10.jpeg" width="80%"/>


### 4、通讯参数配置
===============

> 修改接口配置，连接成功硬件后，点击EdgePlant.exe，选择接口配置

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image11.png" width="80%"/>


> 选择【串口】——【单模式串口】——【COM4】（根据EdgePLUS硬件串行端口设置），根据PLC的【数据位长度】、【校验】、【停止位】和【波特率】对应配置
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image12.png" width="80%"/>
> 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image13.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image14.png" width="80%"/>


> 修改完串口配置文件，点击【配置】——【下载模块配置】进行保存.

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image15.png" width="80%"/>


### 5、配置标签采集指定变量


> PLC数据区采集说明
>
> <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image16.png" width="80%"/>
> 
>
> 点击【应用软件】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image17.png" width="80%"/>


> 在【Project Default】中右击新建组别，在【NewGroup\_0】中新建一个连接

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image18.png" width="80%"/> 
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image19.png" width="80%"/>


> 选择【驱动库】——【三菱】——【FX系列编程口通讯】驱动，修改连接名称和通讯接口，点击确认。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image20.png" width="80%"/>


> 在连接下新建标签开始OPCUA配置

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image21.png" width="80%"/>


> 右击添加驱动标签

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image22.png" width="80%"/>


> 修改【标签名称】、【数据类型】、【地址选择】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image23.png" width="80%"/>


举例：配置数据寄存器D0的有符号16位整数。

> 数据类型选择【有符号16位整数】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image24.png" width="80%"/>


> 数据区域选择【数据寄存器D\[0\~511\]】，参考地址选择【0】，勾选上【写值使能】。点击【确认】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image25.png" width="80%"/>


> 配置完标签后，点击【项目】——【下载模块配置】，将配置文件下载入EdgePLUS中

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image26.png" width="80%"/>


> 重启MDC\_OPCUA\_SERVER

点击【系统设置】——【系统信息】——【系统】，点击【进程列表】，双击运行【/opt/scapeak/MDC\_OPCUA\_SERVER/MDC\_OPCUA\_SERVER】，点击【重启进程】完成重启

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image27.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image28.png" width="80%"/>


若在“进程列表”中未找到“MDC\_OPCUA\_SERVER”软件，请到“软件管理”中右击“MDC\_OPCUA\_SERVER”添加为开机自启，然后点击“软件列表”，下载软件参数，最后重启模块

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image29.png" width="80%"/>


### 6、数据读写演示

> 读取OPCUA客户端数据

点击【应用软件】——【数据采集】——【客户端测试】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image30.png" width="80%"/>


点击【连接】——【Project\_Default】——【NewGroup\_0】——【FX3U-48MR】——【D0】——【订阅】，显示读取的D0数据。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image31.png" width="80%"/>


> 修改OPCUA客户端数据

举例：目前读到的D0当前值为0，修改为100

双击D0标签值区域，修改为100，按Enter提交。观察编程软件D0当前值，发现已经由0修改为100，修改成功。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image32.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slprog/image33.png" width="80%"/>


## 2)三菱PLC以太网FxENET驱动使用手册
### 1、使用环境

本手册陈诉用例应满足如下配置

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image1.png" width="80%"/>


### 2、驱动名称


【FX系列ENET模块以太网驱动】

### 3、硬件连接

#### 3.1 连接方式


【以太网口】连接

#### 3.2 连接步骤

> 将以太网扩展模块通电（24V电压）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image2.png" width="80%"/> 

> 查询PLC模块的IP地址（FX3U-48MR的IP为192.168.1.220）
>
> 将以太网扩展模块通过以太网线连接到EdgePLUS的Eth1以太网接口（Eth1的IP为192.168.1.118）
>
> 将Eth0以太网接口（Eth0的IP为192.168.10.118）通过以太网线与电脑连起来
>
> USB线插入Debug口与电脑连通

硬件连接实物图如下图所示

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image3.png" width="80%"/>


### 4、配置标签采集指定变量

PLC数据区采集说明

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image4.png" width="80%"/>


> 点击【应用软件】——【数据采集】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image5.png" width="80%"/>


> 在【Project Default】中右击新建组别，在【NewGroup\_0】中新建一个连接

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image6.png" width="80%"/> 
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image7.png" width="80%"/>


> 选择【驱动库】——【三菱】——【FX系列ENET模块通讯】驱动，修改连接名称和IP地址，此IP地址设置为PLC的IP，点击确认。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image8.png" width="80%"/>


> 在连接下新建标签开始OPCUA配置。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image9.png" width="80%"/>


> 右击添加驱动标签。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image10.png" width="80%"/>


> 修改【标签名称】、【数据类型】、【地址选择】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image11.png" width="80%"/>


举例：配置数据寄存器D0的有符号16位整数。

> 数据类型选择【有符号16位整数】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image12.png" width="80%"/>


> 数据区域选择【数据寄存器D\[0\~511\]】，参考地址选择【0】，勾选上【写值使能】。点击【确认】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image13.png" width="80%"/>


> 配置完标签后，点击【项目】——【下载模块配置】，将配置文件下载入EdgePLUS中

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image14.png" width="80%"/>


> 重启MDC\_OPCUA\_SERVER

点击【系统设置】——【系统信息】——【系统】，点击【进程列表】，双击运行【/opt/scapeak/MDC\_OPCUA\_SERVER/MDC\_OPCUA\_SERVER】，点击【重启进程】完成重启

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image15.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image16.png" width="80%"/>


若在“进程列表”中未找到“MDC\_OPCUA\_SERVER”软件，请到“软件管理”中右击“MDC\_OPCUA\_SERVER”添加为开机自启，然后点击“软件列表”，下载软件参数，最后重启模块。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image17.png" width="80%"/>


### 5、数据读写演示

> 读取OPCUA客户端数据

点击【应用软件】——【数据采集】——【客户端测试】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image18.png" width="80%"/>


点击【连接】——【Project\_Default】——【NewGroup\_0】——【FX3U-48MR】——【D0】——【订阅】，显示读取的D0数据。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image19.png" width="80%"/>


> 修改OPCUA客户端数据

举例：目前读到的D0当前值为0，修改为100

双击D0标签值区域，修改为100，按Enter提交。观察编程软件D0当前值，发现已经由0修改为100，修改成功。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image20.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slfx/image21.png" width="80%"/>


## 3)三菱PLC以太网Melsec1E驱动
### 1、使用环境

本手册陈诉用例应满足如下配置

  **操作系统**   **Windows 7/8/8.1/10**
  -------------- ------------------------------------------------------------------------------------------------
  **应用软件**   EdgePlant
  **硬件**       EdgePLUS一个、三菱FX系列PLC一个（这里使用FX3U-48MR）、24V电源模块一个、USB线一条、以太网线两条

### 2、驱动名称

【三菱Q/A/FX系列以太网驱动】

### 3、硬件连接

#### 3.1 连接方式

【以太网口】连接

#### 3.2 连接步骤

> 将以太网扩展模块通电（24V电压）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image1.png" width="80%"/> 

> 查询PLC模块的IP地址（FX3U-48MR的IP为192.168.1.220）
>
> 将以太网扩展模块通过以太网线连接到EdgePLUS的Eth1以太网接口（Eth1的IP为192.168.1.118）
>
> 将Eth0以太网接口（Eth0的IP为192.168.10.118）通过以太网线与电脑连起来
>
> USB线插入Debug口与电脑连通

硬件连接实物图如下图所示

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image2.png" width="80%"/>


### 4、OPCUA的配置
==============

PLC数据区采集说明

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image3.png" width="80%"/>


> 点击【应用软件】——【数据采集】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image4.png" width="80%"/>


> 在【Project Default】中右击新建组别，在【NewGroup\_0】中新建一个连接

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image5.png" width="80%"/> 
<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image6.png" width="80%"/>


> 选择【驱动库】——【三菱】——【Melsec1E.TCP客户端】驱动，修改连接名称和IP地址，此IP地址设置为PLC的IP，点击确认。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image7.png" width="80%"/>


> 在连接下新建标签开始OPCUA配置。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image8.png" width="80%"/>


> 右击添加驱动标签

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image9.png" width="80%"/>


> 修改【标签名称】、【数据类型】、【地址选择】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image10.png" width="80%"/>


举例：配置数据寄存器D0的有符号16位整数。

> 数据类型选择【有符号16位整数】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image11.png" width="80%"/>


> 数据区域选择【数据寄存器D\[0\~511\]】，参考地址选择【0】，勾选上【写值使能】。点击【确认】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image12.png" width="80%"/>


> 配置完标签后，点击【项目】——【下载模块配置】，将配置文件下载入EdgePLUS中。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image13.png" width="80%"/>


> 重启MDC\_OPCUA\_SERVER

点击【系统设置】——【系统信息】——【系统】，点击【进程列表】，双击运行【/opt/scapeak/MDC\_OPCUA\_SERVER/MDC\_OPCUA\_SERVER】，点击【重启进程】完成重启

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image14.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image15.png" width="80%"/>


若在“进程列表”中未找到“MDC\_OPCUA\_SERVER”软件，请到“软件管理”中右击“MDC\_OPCUA\_SERVER”添加为开机自启，然后点击“软件列表”，下载软件参数，最后重启模块。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image16.png" width="80%"/>


### 5、数据读写演示

> 读取OPCUA客户端数据

点击【应用软件】——【数据采集】——【客户端测试】

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image17.png" width="80%"/>


点击【连接】——【Project\_Default】——【NewGroup\_0】——【FX3U-48MR】——【D0】——【订阅】，显示读取的D0数据。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image18.png" width="80%"/>


> 修改OPCUA客户端数据

举例：目前读到的D0当前值为0，修改为100

双击D0标签值区域，修改为100，按Enter提交。观察编程软件D0当前值，发现已经由0修改为100，修改成功。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image19.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm1/image20.png" width="80%"/>


## 4)三菱PLC以太网Melsec3E驱动使用手册
### 1、使用环境

本手册陈诉用例应满足如下配置

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image1.png" width="80%"/>


### 2、驱动名称

【FX系列Melsec3E模块以太网驱动】

### 3、硬件连接

#### 3.1 连接方式

【以太网口】连接

#### 3.2 连接步骤

> 查询PLC模块的IP地址（FX5U-32M的IP为192.168.1.220，FX5U-32M的IP请看附录1）
>
> 将PLC通过以太网线连接到EdgePLUS的Eth1以太网接口（Eth1的IP为192.168.1.118）
>
> 将Eth0以太网接口（Eth0的IP为192.168.10.118）通过以太网线与电脑连起来
>
> USB线插入Debug口与电脑连通

硬件连接实物图如下图所示

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/slm3/image2.png" width="80%"/>


### 4、配置标签采集指定变量（PLC数据区采集说明）

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


### 5、数据读写演示

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


## 2.Q系列

### 如何开始1个新工程？

* 新建1个组别 默认第1个组别的名称是 _NewGroup_0_
* _组别名称_ 可自定义，例如本例以Mitsubishi的Q06HCPU示范，可更名为 __Q06H__

* ![image-20200729140853084](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200729140853084.png)





### MelsecUSB

#### 硬件连接及通讯参数配置

* 硬件连接实物图
如下图所示，Q06HCPU与EdgePLUS通过USB线缆建立物理连接。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731134611206.png" alt="image-20200731134611206" style="zoom: 50%;" />



* 新建1个连接
* 选择 _三菱Melsec.USB通讯_  
* 勾选 _内部驱动标签_ ，点击确认
* _连接名称_ 更名为 __MelsecUSB__
    ![image-20200729101118992](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200729101118992.png)
* 配置USB接口
* 如图示，选择图示位置 _驱动参数_  _设备位置_  __功能按钮__

    ![image-20200729101416160](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200729101416160.png)

* 点击 **更新**，展开列表，可显示当前已连接至EdgePLUS并识别的PLC

* 点击图示 MITSUBISHI ，单击 **确定** ，即可自动适应并完成USB配置
     <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200729102040754.png" alt="image-20200729102040754" style="zoom: 67%;" />

#### USB可扩展功能

EdgePLUS的USB驱动支持USB集线器，因此用户可通过外接USB集线器，实现对多个PLC访问。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731170203188.png" alt="image-20200731170203188" style="zoom:50%;" />

#### 配置标签采集指定变量
* 新建1个标签

    <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/屏幕截图(577).png" alt="屏幕截图(577)" style="zoom:67%;" />

* 欲读取PLC中的D0，将_标签名称_手动输入为__D0__
* 选择_数据类型_为__有符号16位整数__
* 在弹出框中保持如图所示配置
  * 数据区域 **数据寄存器|D**
  * 参考地址 **0** ==（输入框的数值进制为十进制）==
  * 勾选**写值使能** ，对PLC允许写入的软元件可通过EdgePLUS的OPCUA服务实现写值。
    ![image-20200729141804153](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200729141804153.png)
* 依次点击**项目** **下载模块配置** ，即可将当前配置烧写进模块
     <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/屏幕截图(579).png" alt="屏幕截图(579)" style="zoom:75%;" />
* 依次操作如图所示步骤，找到进程列表中的MDC_OPCUA_SERVER进程并鼠标左键双击，点击**重启进程**，待进程重启完成后本次配置生效
    <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200729171750016.png" width="80%"/> 
  
* 至此，EdgePLUS可通过MelsecUSB读写PLC中的D0。





### Melsec4C

#### 硬件连接及通讯参数配置

* 硬件连接实物图

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731141227762.png" alt="image-20200731141227762" style="zoom: 50%;" />

  * 本例使用了EdgePLUS的COM1（多模式串口）

* PC通过GX Works2 对PLC编程的端口配置

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731142232850.png" alt="image-20200731142232850" style="zoom:50%;" />

* 使用EdgePLUS的COM1（多模式串口）采集PLC数据的端口配置参数应与上图一致。

| Options    | Value      | Remark |
| ---------- | ---------- | ------ |
| 波特率     | BPS_115200 |        |
| 数据位长度 | CS_8       |        |
| 校验       | ODD        | 奇校验 |
| 停止位       | 1        |        |

 <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731141911032.png" alt="image-20200731141911032" style="zoom: 50%;" />

* 配置Melsec4C驱动选择COM1

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731141534425.png" alt="image-20200731141534425" style="zoom: 50%;" />


* 至此，Melsec4C通讯配置完成，标签配置请参照前文**MelsecUSB**->**配置标签采集指定变量**





### Melsec3E

#### 通过QJ71E71-100 以太网模块进行3E帧通讯

##### 硬件连接及通讯参数配置

* 硬件连接实物图

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731154026816.png" alt="image-20200731154026816" style="zoom:50%;" />
  
    * PLC的以太网模块通过网线与EdgePLUS的Eth1建立物理连接

###### 例1，PLC IP：192.168.1.101/24

* 通讯参数

  * 本例PLC的以太网模块相关配置参数

  | Options  | Value            | Remark                           |
  | -------- | ---------------- | -------------------------------- |
  | 网络类型 | 以太网           |                                  |
  | IP地址   | 192.168.1.101/24 | "/24"，即子网掩码为255.255.255.0 |
  | 网络号   | 1                |                                  |
  | 站号     | 3                | PLC的站号是3                     |
  | 协议     | TCP              | 推荐设置                         |
  | 打开方式 | MELSOFT连接      | 推荐设置                         |
  
  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731154911645.png" alt="image-20200731154911645" style="zoom:50%;" />
  
  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731160153843.png" alt="image-20200731160153843" style="zoom:50%;" />
  
  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200813164146504.png" alt="image-20200813164146504" style="zoom:50%;" />
  
  
  
  * EdgePLUS应保持的配置参数
  
  | Options  | Value         | Remark                                       |
  | -------- | ------------- | -------------------------------------------- |
  | IP地址   | 192.168.1.101 | 即PLC的以太网模块地址                        |
  | 网络编号 | 01            | 此处输入框数据的进制为16进制                 |
  | PLC编号  | 03            | 此处输入框数据的进制为16进制                 |
  | IO编号   | FF.03         | 通讯协议默认                                 |
  | 站编号   | 02            | EdgePLUS的站号，此处输入框数据的进制为16进制 |

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731161058922.png" alt="image-20200731161058922" style="zoom:50%;" />

* 至此，Melsec3E通讯配置完成，标签配置请参照前文**MelsecUSB**->**配置标签采集指定变量**

###### 例2，PLC IP：192.168.10.222/24

* 通讯参数
  * 本例PLC的以太网模块相关配置参数

  | Options  | Value             | Remark                           |
  | -------- | ----------------- | -------------------------------- |
  | 网络类型 | 以太网            |                                  |
  | IP地址   | 192.168.10.222/24 | "/24"，即子网掩码为255.255.255.0 |
  | 网络号   | 10                |                                  |
  | 站号     | 3                 | PLC的站号是3                     |
  | 协议     | TCP               | 推荐设置                         |
  | 打开方式 | MELSOFT连接       | 推荐设置                         |
  
  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200813094226637.png" alt="image-20200813094226637" style="zoom:50%;" />

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731160153843.png" alt="image-20200731160153843" style="zoom:50%;" />
  
  * EdgePLUS应保持的配置参数
  
  | Options  | Value          | Remark                                             |
  | -------- | -------------- | -------------------------------------------------- |
  | IP地址   | 192.168.10.222 | 即PLC的以太网模块地址                              |
  | 网络编号 | 0A             | 0A(H)即10(D),此处输入框数据的进制为16进制          |
  | PLC编号  | 03             | 此处输入框数据的进制为16进制                       |
  | IO编号   | FF.03          | 通讯协议默认                                       |
  | 站编号   | 02             | 自定义EdgePLUS的站号，此处输入框数据的进制为16进制 |

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200813094605764.png" alt="image-20200813094605764" style="zoom:50%;" />

* 至此，Melsec3E通讯配置完成，标签配置请参照前文**MelsecUSB**->**配置标签采集指定变量**

#### 通过内置以太网口进行3E帧通讯

* 说明

本驱动适用的PLC若选用内置以太网口进行3E通讯，由于其上位机软件无“站号”等相关参数配置选项，请根据目标PLC通讯协议设定。

* 硬件连接实物图

略

* 本例PLC的应保持的配置

| Options    | Value      | Remark |
| ---------- | ---------- | ------ |
| IP地址  | 192.168.1.130 | 自定义 |
| 协议 | TCP    |        |
| 打开方式   | MC协议    |  |
| 本站端口号  | 5200    | 自定义 |



<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200818164200127.png" alt="image-20200818164200127" style="zoom:50%;" />

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200818164051664.png" alt="image-20200818164051664" style="zoom:50%;" />

* EdgePLUS应保持的配置参数

| Options  | Value         | Remark                    |
| -------- | ------------- | ------------------------- |
| IP地址   | 192.168.1.130 | 即PLC的内置以太网口IP地址 |
| 网络编号 | 00            | 推荐缺省值                |
| PLC编号  | FF            | 推荐缺省值                |
| IO编号   | FF.03         | 通讯协议默认              |
| 站编号   | 00            | 推荐缺省值                |

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200818164703221.png" alt="image-20200818164703221" style="zoom:50%;" />


### Melsec1E
#### 硬件连接及通讯参数配置
* 硬件连接实物图

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731154026816.png" alt="image-20200731154026816" style="zoom:50%;" />

* 通讯参数配置

  | Options | Value         | Remark                 |
  | ------- | ------------- | ---------------------- |
  | IP地址  | 192.168.1.101 | 即PLC的以太网模块地址  |
  | PLC编号 | FF            | 通讯协议规定的固定参数 |
  

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200731163155044.png" alt="image-20200731163155044" style="zoom:50%;" />

* 至此，Melsec1E通讯配置完成，标签配置请参照前文**MelsecUSB**->**配置标签采集指定变量**

### 软元件的允许访问范围



#### 1.通过QnA兼容3E/3C/4C/4E帧通信

* 基本型CPU

 <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200803092354427.png" alt="image-20200803092354427" style="zoom:67%;" />

* 高性能型QCPU、过程CPU、冗余CPU、QnACPU

 <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200803092446486.png" alt="image-20200803092446486" style="zoom:67%;" />

* 通用型QCPU、LCPU

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200803092520473.png" alt="image-20200803092520473"  />

* 安全CPU

 ![image-20200803092552317](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200803092552317.png)



#### 2.通过QnA兼容1E帧通信

* 软元件列表(无限制CPU 模块)

![image-20200803092854532](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200803092854532.png)

![image-20200803092932258](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200803092932258.png)

* 软元件列表(带限制CPU 模块)
* ![image-20200803093024416](https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/scaedge/image-20200803093024416.png)

# FAQ

* Melsec1E协议不支持访问三菱Q系列PLC的ZR软元件
* 数据类型  **日期时间** 为缺省状态，此手册对应的SCAEdge不支持此数据类型

