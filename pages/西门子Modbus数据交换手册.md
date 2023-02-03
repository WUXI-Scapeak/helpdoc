# Simatic_Modbus_TcpDX使用手册

------


## 1 需求应用

在实现自动化控制中，常常会有这样的需求：在一个复杂的自动化产线调试项目中，在PLC执行到某个动作节点时候，要和单个/多个Modbus-RTU设备进行数据交互，<span style="text-align:left;color:orangered;">希望有个快速工具能够实现PLC给一个触发信号，PLC内部数据就能立马写入Modbus-RTU设备中；或者PLC给一个触发信号，Modbus-RTU设备的数据就马上读到PLC中了。</span>Simatic_Modbus_TcpDX能快速实现这个功能。

## 2 应用架构

### 2.1 应用架构

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/幻灯片1.JPG" width="80%"/>

### 2.2 架构说明

- 串口服务器把RFID读头的RS485接口转成以太网口，并把SCAEdge与SIEMENS PLC接入同一个局域网络里面；
- 按照实际SIEMENS PLC的触发需求，在SCAEdge内部配置好；
- 启用Simatic_Modbus_TcpDX软件即可。

## 3 应用举例

### 3.1 准备测试设备

- RFID读头2个
- 记忆体2个（后续简称：“卡片、卡”）
- SIEMENS S7-200 SMART PLC 1个（IP:192.168.1.50）
- 2口的串口服务器（MOXA）1个
- SCAEdge 1个
- 5口交互机1个
- 24V电源模块1个
- 若干网线和导线

### 3.2场景描述

- 两个RFID读头<span style="display:block;text-align:left;color:orangered;">固定</span>在2个工位上：RFID1，RFID2；

- 每个读头对应一个卡片：卡1、卡2；

- 在现场加工过程中，卡1、卡2的位置会交替变换；

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/image-20211228142343738.png" width="80%"/>

- 数据交互模式如下表所述：

<table border="1"><tr><td><span class="pydocx-center">MOXA的IP</span></td><td><span class="pydocx-center">RFID序号</span></td><td><span class="pydocx-center">功能</span></td><td><span class="pydocx-center">触</span><br /><span class="pydocx-center">发</span><br /><span class="pydocx-center">位</span></td><td><span class="pydocx-center">响</span><br /><span class="pydocx-center">应</span><br /><span class="pydocx-center">位</span></td><td><span class="pydocx-center">错</span><br /><span class="pydocx-center">误</span><br /><span class="pydocx-center">位</span></td><td><span class="pydocx-center">卡片</span><br /><span class="pydocx-center">起始</span><br /><span class="pydocx-center">地址</span></td><td><span class="pydocx-center">卡片长度<br />（1卡片长度</span><br /><span class="pydocx-center">=</span><br /><span class="pydocx-center">2个PLC字节）</span></td><td><span class="pydocx-center">PLC地址范围</span></td></tr><tr><td rowspan="5"><span class="pydocx-left">192.168.1.48</span></td><td rowspan="3"><span class="pydocx-center">RFID 1</span><br /><span class="pydocx-center"> (MOXA Port1)</span></td><td><span class="pydocx-left">读取RFID2写入数据</span></td><td><span class="pydocx-center">0.0</span></td><td><span class="pydocx-center">0.1</span></td><td><span class="pydocx-center">0.2</span></td><td><span class="pydocx-center">0</span></td><td><span class="pydocx-center">20</span></td><td><span class="pydocx-center">VB160-VB199</span></td></tr><tr><td><span class="pydocx-left">把PLC数据→卡片</span></td><td><span class="pydocx-center">1.0</span></td><td><span class="pydocx-center">1.1</span></td><td><span class="pydocx-center">1.2</span></td><td><span class="pydocx-center">0</span></td><td><span class="pydocx-center">10</span></td><td><span class="pydocx-center">VB100-VB119</span></td></tr><tr><td><span class="pydocx-left">清空卡片数据</span></td><td><span class="pydocx-center">2.0</span></td><td><span class="pydocx-center">2.1</span></td><td><span class="pydocx-center">2.2</span></td><td><span class="pydocx-center">0</span></td><td><span class="pydocx-center">20</span></td><td><span class="pydocx-center">VB200-VB239</span></td></tr><tr><td rowspan="2"><span class="pydocx-center">RFID 2</span><br /><span class="pydocx-center">(MOXA Port2)</span></td><td><span class="pydocx-left">读取RFID1写入数据</span></td><td><span class="pydocx-center">3.0</span></td><td><span class="pydocx-center">3.1</span></td><td><span class="pydocx-center">3.2</span></td><td><span class="pydocx-center">0</span></td><td><span class="pydocx-center">10</span></td><td><span class="pydocx-center">VB120-VB139</span></td></tr><tr><td><span class="pydocx-left">把PLC数据→卡片</span></td><td><span class="pydocx-center">4.0</span></td><td><span class="pydocx-center">4.1</span></td><td><span class="pydocx-center">4.2</span></td><td><span class="pydocx-center">10</span></td><td><span class="pydocx-center">10</span></td><td><span class="pydocx-center">VB140-VB159</span></td></tr></table>

### 3.3 测试设备参数

#### 3.3.1 RFID参数配置：默认保持不变

- Device Id：2
- Baud：115200bps
- Word：8
- Parit：NONE
- Stop：1

#### 3.3.2 MOXA参数配置：修改默认参数

- 修改电脑IP，MOXA的默认IP:192.168.127.254 子网掩码：255.255.255.0。浏览器输入MOXA IP地址进行配置，初始密码:moxa

- 在“Network Settings"，修改MOXA的默认IP，本手册选用IP：192.168.1.48

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/image-20211228130225310.png" width="80%"/>

- 在“Serial Settings”，配置串口参数（根据RFID的基本参数）

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/image-20211228130601139.png" width="80%"/>

- 在“Operating Settings”，配置MOXA工作模式“TCP Server Mode”。注：下图“Force transmit 建议设置成20ms”

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/image-20211228130759510.png" width="80%"/>

- 保存退出，并重启。

#### 3.3.3 SCAEdge参数配置

- 修改SCAEdge的IP地址，改成：192.168.1.49

- 把编写的配置文件“Simatic_Modbus_TcpDX_Project.xml”，下载到模块

  - 打开SCAEdge的配置软件——EdgePlant
  - 进入“边缘应用软件管理界面”，点击“安装”
  - 选择安装目录“/opt/scapeak/Simatic_Modbus_TcpDX/”
  - 找到本地PC上“Simatic_Modbus_TcpDX_Project.xml”所在位置
  - 勾选“可执行、可注册”，开始安装

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/image-20211228145029408.png" width="80%"/>

- 把Simatic_Modbus_TcpDX工功能添加开机自启

  - 在“边缘应用软件管理——2.自动化控制”找到“Simatic_Modbus_TcpDX”软件名称
  - 鼠标右键点击“添加开机启动”；

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/image-20211228145503699.png" width="80%"/>

  - 点击下“载配置”

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/image-20211228145426863.png" width="80%"/>

  - 下载成功，重启Edge模块。

### 3.4 如何编写“Simatic_Modbus_TcpDX_Project.xml”文件

- 新建一个TXT文本，重命名为“Simatic_Modbus_TcpDX_Project”，扩展名TXT改成xml

- 本案中，“Simatic_Modbus_TcpDX_Project.xml”内容如下：

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!-- Simatic_Modbus_TcpDX Project File, WUXI LingDing Tech Co.,Ltd, 2019 -->
  <Simatic_Modbus_TcpDX>
  	<SimaticPLC Name="PLC50" IpAddr="192.168.1.50" DstTsap="" DBNo="1" Timeout="1000" Interval="10" Comment="SMART200" >
  		<ModbusSlave Name="48-1" TcpServerIpAddr="192.168.1.48" TcpServerPort="4001" ModbusAddr="2" Timeout="1000" Comment="rfid scaner2">
  			<Read Name="48-1R1" RequestBit="0.0" ResponseBit="0.1" ErrorBit="0.2" ModbusReg="holdreg" RegOffset="0" RegCount="20" SimaticAddr="160" />
  			<Write Name="48-1W1" RequestBit="1.0" ResponseBit="1.1" ErrorBit="1.2" ModbusReg="holdreg" RegOffset="0" RegCount="10" SimaticAddr="100" />
  			<Write Name="48-1W2" RequestBit="2.0" ResponseBit="2.1" ErrorBit="2.2" ModbusReg="holdreg" RegOffset="0" RegCount="20" SimaticAddr="200" />
  		</ModbusSlave>
  		<ModbusSlave Name="48-2" TcpServerIpAddr="192.168.1.48" TcpServerPort="4002" ModbusAddr="2" Timeout="1000" Comment="rfid scaner2">
  			<Read Name="48-2R1" RequestBit="3.0" ResponseBit="3.1" ErrorBit="3.2" ModbusReg="holdreg" RegOffset="0" RegCount="10" SimaticAddr="120" />
  			<Write Name="48-2W1" RequestBit="4.0" ResponseBit="4.1" ErrorBit="4.2" ModbusReg="holdreg" RegOffset="10" RegCount="10" SimaticAddr="140" />
  		</ModbusSlave>
  	</SimaticPLC>
  </Simatic_Modbus_TcpDX>
  ```

- “Simatic_Modbus_TcpDX_Project.xml”文件说明（未说明部分为默认配置）

  - PLC参数配置

  ```xml
		<SimaticPLC Name="PLC+IP地址的最后1位" IpAddr="PLC的IP地址" DstTsap="" DBNo="DB的块好（V区=1）" Timeout="1000" Interval="10" Comment="SMART200" >
  ```

  - 单个RFID读头的读写功能框架配置
  
  ```xml
  		<ModbusSlave Name="读头序号" TcpServerIpAddr="MOXA的IP地址" TcpServerPort="MOXA 的Port端口号" ModbusAddr="RFID的站地址" Timeout="1000" Comment="rfid scaner2">
                                    内部编写读写模式，参照下面2点
              						`RFID读头的读模式  
                                      `RFID读头的写模式  
    		</ModbusSlave>
  ```
  
  - RFID读头的读模式  
  
  ```xml
  <!-- 读RFID操作定义，触发位(PLC置位请求读取数据)，响应位（SCAEdge完成读取后置位1），错误位（SCAEdge读取失败置位1），读取的Modbus寄存器起始地址，读取寄存器个数，读取的数据存放到西门子PLC的起始地址（VB1001） -->
  			<Read Name="读头序号" RequestBit="触发位" ResponseBit="响应位" ErrorBit="错误位" ModbusReg="holdreg" RegOffset="卡片起始地址" RegCount="卡片长度" SimaticAddr="PLC起始地址" />
  ```
  
  - RFID读头的写模式  
  
  ```xml
  <!-- 写RFID操作定义，触发位(PLC置位请求读取数据)，响应位（SCAEdge完成读取后置位1），错误位（SCAEdge读取失败置位1），读取的Modbus寄存器起始地址，读取寄存器个数，读取的数据存放到西门子PLC的起始地址（VB1001） -->
  			<Write Name="读头序号" RequestBit="触发位" ResponseBit="响应位" ErrorBit="错误位" ModbusReg="holdreg" RegOffset="卡片起始地址" RegCount="卡片长度" SimaticAddr="PLC起始地址" />
  ```
  
- 参照整体配置文件，编写“Simatic_Modbus_TcpDX_Project.xml”

### 3.5 在10 s内，获取所需的“Simatic_Modbus_TcpDX_Project.xml”

- 根据案例需求，配置好“demo.xlsx”内容

  <img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/siemens_modbus/image-20211228155909716.png" width="80%"/>

- 可以问季工要xml文件生成工具，能够一键生成xml文件。

## 4 联系我们

拨打我们的24小时免费咨询热线：400-8544-418

发送电子邮件，咨询具体解决方案：[support@scapeak.com](mailto:public@scapeak.com)

工作时间的咨询电话：0510-8591-5808，0510-8591-5898