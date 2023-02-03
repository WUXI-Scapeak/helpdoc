 EdgePLUS通过RS422串口采集三菱FX系列PLC
=======================================

PLC型号：FX3U-48MR

驱动：三菱FX系列编程口驱动

一、功能和应用
--------------

三菱FX系列的编程口一般都是RS422串口，EdgePLUS的COM1和COM2口是多模式串口，RS422/RS485/RS232三个模式可任意切换。当这两个串口处于RS422模式时，同时选用三菱FX系列编程口驱动，就可以对三菱FX系列的PLC进行数据采集。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image1.jpeg" width="80%"/>


二、通讯线连接
--------------

EdgePLUS的COM1/COM2口连接三菱FX系列编程口的接线方式如下表：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image2.png" width="80%"/>


三、EdgePLUS配置
----------------

### 1. EdgePLUS接口配置

根据三菱PLC设置的串口信息用EdgePlant配置软件对EdgePLUS的串口进行配置（本次采用的串口是COM2），配置完成后点击“配置”按钮，下载模块配置。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image3.png" width="80%"/>


### 2. 驱动选择

#### a) 点击“Project\_Default”，新建一个组别（组别名称可以自定义）.

#### b) 点击“NewGroup\_0”，新建一个连接（连接名称可自定义），选用FX系列编程口通讯驱动，进行数据采集.

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image4.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image5.png" width="80%"/>


### 3. 变量配置

#### a) 点击“Connection\_0”，添加驱动标签。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image6.png" width="80%"/>


#### b) 根据需要采集的PLC点表地址，击连接“Connection\_0”，新建一个标签（需要采集的变量配置），变量配置完成后，点击“项目”，下载模块配置。eg：\[采集地址：D264，类型：无符号整数\]。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image7.png" width="80%"/>


#### c) 下载完成需要采集的变量配置后，双击重启“MDC\_OPCUA\_SERVER”软件。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image8.png" width="80%"/> 

#### d) 若在“进程列表”中未找到“MDC\_OPCUA\_SERVER”软件，请到“软件管理”中右击“MDC\_OPCUA\_SERVER”添加为开机自启，然后点击“软件列表”，下载软件参数，最后重启模块。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image9.png" width="80%"/>


### 4. 查看数据

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image10.png" width="80%"/>


四、PLC数据区采集说明
---------------------

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/fx3u/image11.png" width="80%"/> 

注：FX1S无32位双向计数器，只有在使用累计型定时器才需要复位。
