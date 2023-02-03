
**Edge模块**
==========

**MES DATA SERVER数据存储服务**

**用户手册**

第1章 概述 
==========

MES.DATA.SERVER是一个数据存储服务软件，可根据配置文件自动创建数据库和表单并自动完成数据的持续性导入。MES.DATA.SERVER采用C语言开发，并运行在实时Linux系统中，具备极高的实时性和很低的CPU占用率。软件会根据配置文件自动创建数据库，可以是位于Edge模块中的内置数据库，也可以是本地MES数据库，也可以是云端数据库，支持MYSQL和MariaDB。

1.1 特点 
--------

无数量限制的数据库和表单配置。可以同时向多个数据源输送数据，譬如在Edge本地数据库存储数据，同时向远程MES系统和云端输送备份。

能从网络上的多个OPCUA服务器获取数据。将多个来源的设备数据汇聚到一张表，譬如一个Edge模块通过电表采集空压机的用电消耗，另一个Edge模块和空压机的PLC通讯获取空压机的输出流量。我们可以把用电量和流量放到一张表中来进行分析。

1.2 软件功能 
------------

能够自动连接到多个OPCUA服务器以获取过程数据。

支持Edge模块内部数据库和网络上的数据库，支持MYSQL/MariaDB，数据文件格式为MyISAM，UTF-8字符。

支持三种类型的表单创建，并支持创建多个表单。

定时采样表：按照设定的时间间隔定时插入一条数据记录，用于过程数据的定时采集；

实时更新表：当数据发生变化时自动更新唯一的一条数据记录，用于数据看板展示；

事件记录表：当数据发生变化时（事件发生）自动插入一条记录，用于记录报警事件或跟踪工艺设定数据变更；

> 支持对定时记录表和事件记录表的记录数进行限制（先进先出）。

1.3 软件依赖项 
--------------

MDC.OPCUA.SERVER

MES.DATA.SERVER从OPCUA服务器中获取设备过程数据，因此如果需要获取Edge模块所连接设备的运行数据，MDC
OPCUA服务器必须首先运行。OPCUA服务器也可以位于外部服务器上，目前仅支持匿名登陆。当OPCUA服务器被断开后软件会自动尝试连接。

MYSQL/MariaDB数据库

Edge模块内部默认安装了MYSQL/MariaDB数据库实例。数据库文件也可以位于外部服务器上，目前支持MYSQL/MariaDB，即MES.DATA.SERVER可以在网络上的服务器上自动创建MYSQL/MariaDB数据库文件，只要服务器上已安装MYSQL/MariaDB数据库的实例即可。

1.4 应用架构 
------------

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image2.png" width="80%"/>


第2章 EdgePlant配置 
===================

2.1 查看配置 
------------

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image3.png" width="80%"/>


运行EdgePlant软件，根据所使用的网卡，搜索并连接到模块；选择“应用软件”；选择“数据存储”，打开MES
DATA SERVER软件的配置。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image4.png" width="80%"/>


读取模块配置：读取Edge中现有配置文件

下载模块配置：将修改后的配置文件下载至Edge，每次修改配置后需要重新下载配置

打开模块配置：打开本地电脑上的xml配置文件

保存模块配置：将当前xml配置文件保存到本地电脑

2.2 软件运行 
------------

### 2.2.1 程序开机自启 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image5.png" width="80%"/>


在“系统设置/软件管理/数据储存”菜单下，找到“MES DATA
SERVER”软件，复制“文件路径”，打开“开机启动”菜单。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image6.png" width="80%"/>


新建配置，自定义“软件名称”，将上述复制的“文件路径”粘贴到“软件路径”，设置启动延时，通常为“1000毫秒”，最后下载配置。

此时每次重启Edge或者重新上电，系统启动后，MES DATA
SERVER程序都会自动运行。

### 2.2.2 程序重启 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image7.png" width="80%"/>


选择“系统设置/系统信息/系统/进程列表”，在进程列表下找到“MES\_DATA\_SERVER”进程，双击打开进程，可以选择“重启进程”或“终止进程”。

每次修改完软件配置并下载配置文件后，都需要按此步骤重新运行程序，新的配置文件才会生效。

2.3 数据源定义 
--------------

数据源定义用于指定整个配置文件的外部数据源，可以定义多个OPCUA
SERVER连接。（Mes.Data.Server从外部数据源获取数据并插入到指定的表单中）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image8.png" width="80%"/> 

右键“数据源定义”，添加OPCUA服务器。自定义“服务器名称”，终结点格式为“opc.tcp://ip地址:端口号”，如果使用Edge的内置OPCUA服务器，终结点中的IP地址，需要设置为当前电脑所连接Edge模块的网口IP地址。

Edge模块的IP地址，可以在EdgePlant软件左下角查看。如此时电脑通过Edge的Eth0连接，终结点设置为“opc.tcp://192.168.10.118:4840”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image9.png" width="80%"/>


2.4 数据库服务器连接 
--------------------

数据库服务器连接用于配置数据库服务器，也就是数据库的实例。

### 2.4.1 数据服务配置 

右键添加数据库服务器连接。“服务器IP”为数据库实例所在的远程计算机的IP地址，注意通过网络访问需要开启3306端口。指定一个能够远程访问，并拥有足够数据库操作权限的账号密码，用于连接远程数据库。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image10.png" width="80%"/>


### 2.4.2 数据库配置 

右键创建数据库，自定义数据库名称。指定“自动创建”，如果数据库不存在是否自动创建。指定“自动删除”，如果数据库已存在，则是否先删除。

程序运行首先会执行“自动删除”，再执行“自动创建”。因此，如果不想要删除原来的数据库，则避免多个数据库名称重复，或者指定“自动删除”为“否”。“自动创建”必须设置为“是”。在数据库服务器连接下，可以定义多个数据库。如果需要，可以将多张表划分到不同的数据库中。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image11.png" width="80%"/>


### 2.4.3 数据表配置 

右击数据库创建数据表，目前支持三种类型的数据表。

**实时更新表**：表中只有一条记录，每间隔一定时间就更新所有字段的值。用于在线显示当前过程数据。

**定时记录表**：周期性记录表，每间隔一定时间就向表中插入一条记录。用于记录历史过程数据。

**事件记录表**：事件触发记录表，每间隔一定时间就依次检查一遍每个事件是否满足，如果该事件满足则插入一条记录。用于当某事件发生时插入一条信息，如报警信息和产线动作记录。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image12.png" width="80%"/> 

指定“自动创建”，如果数据表不存在是否自动创建。指定“自动删除”，如果数据表已存在，则是否先删除。处理逻辑和数据库一样。

设定“时间常数”，指示不同类型数据表更新/插入/检查事件的事件间隔，单位为毫秒。

设定“记录限定数”，适用于定时记录表和事件记录表。等于0代表无限制，大于0为记录的限定数。当超过限定数时插入一条新记录会删除一条旧记录。删除的旧记录是按照ID字段排序的，因此当该参数大于0时要求表必须定义一个名为ID的自增字段。

每个Table表都是独立和并行执行的，相互之间没有关联。表在被更新和插入时都会依次处理所有定义的字段。

### 2.4.4 字段配置 

右键数据表，创建字段。

可以选中字段上下移动，调整数据表格式。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image13.png" width="80%"/>


字段名称、字段别名：即数据表中的字段名称和注释。

字段声明：不局限于INT、VARCHAR、FLOAT之类的简单类型，任何Mysql的CREATE语句能识别的字段定义都可以。

数据格式符、字段数据源、OPCUA标签需要配合设置：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image14.png" width="80%"/> 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image15.png" width="80%"/>


### 2.4.5 OPC标签值字段配置 

用于从OPCUA服务器读取一个变量值，并转换成需要的数据类型写入数据库。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image16.png" width="80%"/>


打开“OPCUA标签选择”对话框，选择“已配置的数据源”，在“节点空间浏览”中选择需要链接的节点。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image17.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image18.png" width="80%"/> 

### 2.4.6 列表值字段 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image19.png" width="80%"/>


该字段仅当“数据格式符”为“ListValue”时才允许定义。其余配置和OPC标签值字段配置相同。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image20.png" width="80%"/>


列表值字段用于配置列表属性。

列表配置可以定义多个，没有限制。

值范围：将变量值与每一个列表值范围（数值范围，整数或浮点数）进行对比，如果匹配则解析该数据源数值作为字段的值。波浪线\~前面的数值为最小值（大于等于），\~后面的数值为最大值（小于等于），没有\~则认为是数值匹配（等于）。

数据格式符：指定该参数的文本，作为字段值写入数据库。

列表数据源：如果选择“数据格式符”，则直接取“数据格式符”参数从指定的值，如果选择“OPCUA服务器”，则取“OPCUA标签”中定义的值。

OPCUA标签：可直接复制列表值字段中选择的OPCUA标签。

### 2.4.7 事件节点 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image21.png" width="80%"/>


事件记录表中可以配置多个Event节点，每个Event节点定义一个发生的事件。一个表内可以定义多个Event节点，这些Event节点将被单独扫描处理，每个满足触发条件的Event都将引起插入一条完整的记录。

触发类型：支持对位值的跳变检查，“上升沿触发”代表0-1上升沿跳变，“下降沿触发”代表1-0下降沿跳变。支持值变化检查，当Event节点值发生变化，即触发事件。

复位触发信号：目前仅可设置为“无”或者“复位触发信号”，当设置为"复位"时，当事件发生后自动复位事件对应的OPCUA变量（即“OPCUA标签”定义的变量）。

事件关联文本：用来标注一个纯字符串的事件文本，可用于插入到字段中。

### 2.4.8 事件文本字段 

只有在事件记录表中可以创建该字段。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image22.png" width="80%"/>


将触发事件的文本填充到这个字段：即将上述“EVENT事件节点”中定义的“事件关联文本”，填充到字段中。这样，对于不同的事件就可以记录不同的内容，譬如记录所有报警的表或者设备的所有动作。

### 2.4.9 常用字段举例 

**自增主键字段（自增字段必须设置为主键）**

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image23.png" width="80%"/> 

**日期时间字段**

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image24.png" width="80%"/>


**固定数值字段**

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image25.png" width="80%"/> 

**固定字符串字段**

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image26.png" width="80%"/> 

**OPC标签值字段**

将OPCUA整数变量值填充到整数字段：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image27.png" width="80%"/> 

将OPCUA浮点数变量值填充到单精度字段（格式化为3位小数）：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image28.png" width="80%"/>


将OPCUA整数变量值填充到字符串字段，%d前后加单引号：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image29.png" width="80%"/>


将OPCUA整数变量值转换为16进制数值填充到字符串字段：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image30.png" width="80%"/>


将OPCUA字符串变量值填充到字符串字段，%s前后加单引号：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image31.png" width="80%"/> 

**列表值字段**

例：当OPCUA变量值为1，该字段写入“列表值=1”；当OPCUA变量大于2，该字段写入“列表值=2”。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image32.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image33.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/mes/image34.png" width="80%"/>


2.5 配置注意事项 
----------------

MES.DATA.SERVER能够满足大多数的数据记录需求，目的也是通过配置快速实现信息化项目上的数据存储。注意使用上的限定：

每次修改配置都需要重新下载配置文件，并重启MES DATA
SERVER进程后，新的配置文件才会生效。

单条SQL语句被限制在16K字符长度，如果表单的字段很多，软件生成的SQL语句超过16K字符的长度将导致出错。

SQL语句中单个字段的创建、插入和更新字符串不能大于256个字符，所以尽量把字段名设置的短一点。

ServerName、ServerHost、AccountUser、AccountPassword、DatabaseName被限制在64个字符，EndpointUrl被限制在256个字符。

TableName、EventName、FieldName、FieldAlias、FieldType、ListName、DataRange、DataSource被限制在64个字符。

ItemNode、DataFormat、EventText被限制在256个字符。尽量把OPCUA变量名设置的短一点。
