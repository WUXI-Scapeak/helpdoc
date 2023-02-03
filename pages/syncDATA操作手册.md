数据库同步使用手册（syncDATA）
============

一、设备连接
============

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image1.jpeg" width="80%"/>


EdgePLUS通过网线分别连接PC和PLC，EdgePLUS通过USB接口连接PC通电。

二、使用流程及相关配置
============

1.首先进入网路配适器，如下图：

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image2.png" width="80%"/>


其中1为路径（可通过cortana直接搜索），进入以太网配置PC的IP。

2.点击属性（1），然后选择Internet协议版本4，设置其为使用下面的IP地址，IP地址可以自己设置。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image3.png" width="80%"/>


3.打开EdgePlant，选择以太网端口连接EdgePLUS，在下图的步骤3中进行Eth1和Eth0网口的配置，将PLC和EdgePLUS，PC和EdgePLUS分别放在同一网段下。（连接PLC和PC的网口）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image4.png" width="80%"/>


点击应用软件中的数据采集，会显示下图信息，在3中的目录下可以创建新的节点用来存储需要的PLU的相关数据（同步的数据），4是PLC的IP，可自行设置（注意要和EdgePLUS在同一网段下）。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image5.png" width="80%"/> 

然后通过系统设置中的软件管理进行软件安装，这里需要安装的是下面的MES\_DATA\_SERVER（数据存储）和syncDATA\_MsSQL（数据同步）。（注意：syncDATA\_MsSQL的安装路径为/opt/scapeak/syncDATA\_MsSQL，MES\_DATA\_SERVER的安装路径为/opt/scapeak/MES\_DATA\_SERVER）。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image6.png" width="80%"/> 

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image7.png" width="80%"/>


安装完后，在系统信息的软件列表进行列表更新，然后在4.数据存储中可以看到安装的软件，右键将两个软件加入开机自启中，并且下载配置并重启（注意添加一个软件就要下载重启一次）。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image8.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image9.png" width="80%"/> 

软件安装完后，在EdgePlant中进行下图的步骤1，下载模块配置，再进行客户端测试，将其中的服务器地址和选择的标签id的信息复制下来。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image10.png" width="80%"/>


然后再选择下图中的1进行MES\_DATA\_SERVER的配置（可产考我司网站上MES\_DATA\_SERVER的操作手册），在2中进行数据库、数据表和数据表节点的创建,注意：在创建节点时，要创建一个自增主键ID，名称改为ID，自增主键ID必须放在第一个节点的位置（update模式下不能有自增主键ID），其他的信息都不用更改。还有一个固定数值字段，名称为syncFlag，字段声明为INT，数据格式符为0，字段数据源为数据格式符，这个节点的位置不用固定（上述两个节点在insert模式下是必须要存在的）。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image11.png" width="80%"/>


数据表类型一般使用定时记录表，并且自动创建和自动删除根据你的实际需要进行选择。

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image12.png" width="80%"/>


然后进入应用软件修改上图1中的数据库同步软件配置，在2中SourceDb标签中设置源数据库的信息（要被同步的数据库）。DbType：源数据库（默认MYSQL），DbName：数据库名称，User：默认为scaedge，Password：默认为scapeak，Host：默认为127.0.0.1，SyncMode：软件执行模式（insert（存储）或者update（更新））（注意：insert使用对象为定时记录表和事件记录表，update针对的对象为定时更新表），Port：端口号（默认为0），DataClear：是否在同步后将Edge中的MYSQL数据库中的已同步的数据删除（建议YES，确保Edge的内存不会被占用满），CopyAllTables：是否同步mysql数据库中所有的表，在选为YES后，下面的TableName的表名就可写可不写（此节点推荐NO，手动填写自己需要同步的表，以确保同步表的正确定，减少EdgePLUS的运行资源的占用），在TableName节点中的Table后面添加一个数据库中的你需要同步的表名（表明与表明间用空格分隔），如下图中所示。在DeatDb标签中设置目标数据库的信息（数据同步到的目标数据库）。DbType：：目标数据库（MYSQL或者MSSQL），DeleteOldTable：是否在启动时删除原来的表（每一次启动都会被默认为NO，如需删除原来的表，请在运行软件前手动设置为YES）。（注意：数据库要给一定的权限，比如表的建立，TCP的连接，端口的开放并且要提前建立目标数据库（用于存放同步表）。）

<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image13.png" width="80%"/>


<img src="https://scapeakstorage.blob.core.chinacloudapi.cn/helppic/syncdata/image14.png" width="80%"/>


然后回到系统设置的软件管理，鼠标右键1中的内容，将其加入开机启动（2中）（注意：一次只能将一个软件加入开机启动，加入一个软件后需要点击2中的“下载配置”），将软件加入开机启动后，点击3的重启模块，完成设置。

注意：请不要随意修改MES中的标签（添加或者删除），这样会破坏同步后的表的结构，软件会自动停止同步并退出，如果修改，请将原来已经同步的表保存下来，然后将DeleteOldTable手动设置为YES。

如果只是在某一个数据库中添加或删除一个表，只需在TableName节点中进行相应的修改即可。
