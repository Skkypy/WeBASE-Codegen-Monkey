
# WEBASE-MONKEY

[![License](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![Gitter](https://badges.gitter.im/webase-monkey/webase-monkey.svg)](https://gitter.im/webase-monkey/community)
[![Stargazers over time](https://starcharts.herokuapp.com/WeBankFinTech/webase-monkey.svg)](https://starcharts.herokuapp.com/WeBankFinTech/webase-monkey)


> 道生一，一生二，二生三，三生万物。
> 万物负阴而抱阳，冲气以为和。
> 人之所恶，唯孤、寡、不谷，而王公以为称。
> 故物或损之而益，或益之而损。
> 人之所教，亦我而教人。
> 强梁者不得其死——吾将以为教父。
> —— 老子

## 1. 组件介绍

### 1.1 数据导出组件： WEBASE-BEE
WEBASE-BEE 是一个基于[FISCO-BCOS](https://github.com/FISCO-BCOS/FISCO-BCOS)平台的数据导出工具。

数据导出组件WEBASE-BEE的目的在于降低获取区块链数据的开发门槛，提升研发效率。研发人员几乎不需要编写任何代码，只需要进行简单配置，就可以把数据导出到指定的存储介质上，比如DB、ES、MQ、Hadoop等，并提供相关服务接口获取数据，以满足业务场景需求。

WEBASE-BEE可以导出区块链上的基础数据，如当前块高、交易总量等。
如果正确配置了FISCO-BCOS上运行的所有合约，WEBASE-BEE可以导出区块链上这些合约的业务数据，包括event、构造函数、合约地址、执行函数的信息等。

WEBASE-BEE提供了基于Restful的API，支持通过http的方式调用这些接口。

### 1.2 代码自动生成组件：WEBASE-MONKEY
WEBASE-BEE易于使用，且功能强大；但是仍有一定的开发门槛。为了更进一步地提升研发效率，我们开发了WEBASE-MONKEY。

只需要在一个配置文件中进行少量简单的配置，同时按照要求提供相关的智能合约信息；当前版本可支持自动生成WEBASE-BEE。

### 1.3 使用场景和解决方案
区块链的数据存储在区块链上，需要使用智能合约暴露的接口来进行调用。由于智能合约暴露的接口的限制，区块链上不适合进行复杂的数据查询、大数据分析和数据可视化等工作。因此，我们致力于提供一种智能化、自动化的数据导出和备份的解决方案。

#### 案例 数据可视化后台系统
- 背景

某互联网小贷公司基于FISCO-BCOS开发了区块链借条业务系统，客户之间的借贷合同信息和证明材料都会在脱敏后保存到区块链上。该公司的运营人员需要获得当前业务进展的实时信息和摘要信息。

- 解决方案

该公司使用webase-monkey迅速生成了webase-bee的代码，并根据实际需求进行了定制化开发，在一天之内投入到线上使用。

导出到db的数据接入到了该公司的统一监控平台，该公司PM可以在业务后台系统上获得该业务的实时进展，该公司运维人员可以在公司运维监控室的大屏幕实时监控业务系统的状态。

#### 案例 区块链业务数据对账系统
- 背景

某公司基于FISCO-BCOS开发了区块链的业务系统，需要将本地数据与链上的数据进行对账。

- 解决方案
该公司使用webase-monkey迅速生成了webase-bee的代码，并根据实际需求进行了定制化开发。通过在智能合约中设计的各类event，相关的业务数据都被导出到数据库中；从而实现轻松对账的需求。

#### 案例 区块链业务数据查询系统
- 背景

某互联网公司基于FISCO-BCOS开发了区块链的业务系统，但是发现智能合约对业务报表的支持不佳。但是，公司的一线业务部门要求实时查看各类复杂的业务报表。

- 解决方案

该公司使用webase-monkey迅速生成了webase-bee的代码，并根据实际需求进行了定制化开发，区块链上的数据可以实时导出到数据库中。利用webase-bee自带的Restful API，该公司的报表系统实现了和区块链数据的对接，可以获得准实时的各类业务报表。

### 1.4 特性介绍

#### 自动生成数据导出组件
只需用户提供智能合约编译后的Java代码和相关的底层链、数据库的基本信息，webase-monkey就能帮助你自动生成一个区块链数据导出的组件。现阶段，支持将数据导出到Mysql数据库中。

#### 支持自定义导出数据内容
可以支持导出区块链的基本信息、智能合约的函数、Event等信息。可以对导出的数据库表、字段进行定制。也可以修改导出数据字段的长度。

#### 内置Restful API，提供常用的查询功能
自带常用的Restful API，支持查询块高、块信息、Event信息和函数信息等。

#### 支持多数据源，支持读写分离和分库分表
为了应对海量数据的导出，webase-bee数据导出组件支持可配置的多数据源存储，读写分离和分库分表：数据可以存储到多个表中，也可以存储到多个库中。同时，内置的Restful API可以自动无感知地返回正常的数据。

#### 支持多活部署，多节点自动导出
webase-bee数据导出组件支持多活部署，可自动进行分布式任务调度。

#### 支持区块重置导出
webase-bee数据导出组件基于区块高度进行导出，并支持指定高度重新导出数据。


## 2. 快速开始

### 2.1 前置依赖
在使用本组件前，请确认系统环境已安装相关依赖软件，清单如下：

| 依赖软件 | 说明 |备注|
| --- | --- | --- |
| Bash | 需支持Bash（理论上来说支持所有ksh、zsh等其他unix shell，但未测试）|
| Java | >= Oracle JDK[1.8] |JAVA安装可参考附录2|
| Git | 下载的安装包使用Git | Git安装可参考附录3|
| MySQL | >= mysql-community-server[5.7] | MySQL安装可参考附录4|
| zookeeper | >= zookeeper[3.4] | 只有在进行集群部署的时候需要安装，zookeeper安装可附录5|


### 2.2 部署步骤

#### 2.2.1 获取安装包

##### 2.2.1.1 下载代码库

首先请clone或下载本代码库。下载完成后，进入本项目：

```shell
git clone https://github.com/WeBankFinTech/webase-monkey.git 
cd webase-monkey
git checkout -b dev origin/dev
```

##### 2.2.1.2 进入安装路径

安装文件的路径位于：

```shell
cd src/main/install_scripts/
```

进入，获得如下的目录结构，其中Evidence.java为合约示例。

```
├──install_scripts
    └── config
    	└── contract
            └── Evidence.java
    	└── resources
    	    └── application.properties
    └── generate_bee.sh
```
#### 2.2.2 配置安装包

##### 2.2.2.1 配置合约文件

请注意，请确保你使用的Web3SDK的版本大于等于**V1.2.0**。

找到你的业务工程（你要导出数据的那条区块链中，往区块链写数据的工程），复制合约产生的Java文件：请将Java文件**复制到./config/contract目录**下（请先删除目录结构中的合约示例Evidence.java文件）。

如果你的业务工程并非Java工程，那就先找到你所有的合约代码。不清楚如何将Solidity合约生成为Java文件，请参考： [合约代码转换为java代码](https://fisco-bcos-documentation.readthedocs.io/zh_CN/v1.0.1/docs/web3sdk/advanced/gen_java_code.html?highlight=compile.sh)

请注意:  **请勿使用数据库SQL语言的保留字来定义合约内部的变量、函数名定义**，否则会导致数据库无法成功建表。如定义一个变量名为key或定义一个函数为select或delete等。

##### 2.2.2.2 配置密钥文件

复制密钥相关的配置文件：请将你的配置文件**复制到./config/resources目录**下。配置文件包括：
-     ca.crt
-     client.keystore     

##### 2.2.2.3 配置应用

修改application.properties文件：该文件包含了所有的配置信息。
以下配置信息是必须要修改的，否则跑不起来：

```
# 节点的IP及通讯端口。
system.nodeStr=[NODE_NAME]@[IP]:[PORT]
# 最新版本的FISCO-BCOS平台中的NODE_NAME可以为任意值。

# 数据库的信息，暂时只支持mysql； serverTimezone 用来设置时区，characterEncoding 用来设置字符集
system.dbUrl=jdbc:mysql://[IP]:[PORT]/[database]?characterEncoding=utf8&useSSL=false&serverTimezone=GMT%2b8
system.dbUser=[user_name]
system.dbPassword=[password]

# 合约Java文件的包名
monitor.contractPackName=[编译Solidity合约时指定的包名]
```

更多配置详情可参考附件1：配置参数。

#### 2.2.3 生成代码并运行程序

##### 2.2.3.1 选择一：直接在本机运行

```
chmod +x generate_bee.sh
sh generate_bee.sh 
```

当前目录下会生成webase-bee工程代码。数据导出组件将直接启动，对应的执行日志会打印到终端上。

请注意: 请务必按照以上命令操作，**切莫使用sudo命令来操作**，否则会导致Gradlew没有权限，导致depot数据失败。

##### 2.2.3.2 选择二：本机编译，复制执行包到其他服务器上运行

```
chmod +x generate_bee.sh
sh generate_bee.sh build 
```
当前目录下会生成webase-bee工程代码。请将此生成工程下的./webase-bee/dist文件夹复制到其他服务器上，并执行：

```
chmod +x *.jar
nohup java -jar *.jar >/dev/null 2>&1 &
tail -f *.log
```

##### 2.2.3.3 选择三：本机编译，复制执行包到其他服务器，使用supervisor来启动。
使用supervisor来守护和管理进程，supervisor能将一个普通的命令行进程变为后台daemon，并监控进程状态，异常退出时能自动重启。
它是通过fork/exec的方式把这些被管理的进程当作supervisor的子进程来启动，这样只要在supervisor的配置文件中，把要管理的进程的可执行文件的路径写进去即可。
也实现当子进程挂掉的时候，父进程可以准确获取子进程挂掉的信息的，可以选择是否自己启动和报警。
supervisor还提供了一个功能，可以为supervisord或者每个子进程，设置一个非root的user，这个user就可以管理它对应的进程。

编译生成代码的部署同2.2.3.2

使用supervisor来安装与部署的步骤请参阅附录6

#### 2.2.3 检查运行状态及退出

##### 2.2.3.1 检查程序进程是否正常运行
```
ps -ef |grep webase-bee
```
如果看到如下信息，则代表进程执行正常：
```
app   21980 24843  0 15:23 pts/3    00:00:44 java -jar webase-bee0.3.0-SNAPSHOT.jar
```

##### 2.2.3.2 检查程序是否已经正常执行

当你看到程序运行，并在最后出现以下字样时，则代表运行成功：
    
```
Hibernate: select blockheigh0_.pk_id as pk_id1_2_, blockheigh0_.block_height as block_he2_2_, blockheigh0_.event_name as event_na3_2_, blockheigh0_.depot_updatetime as depot_up4_2_ from block_height_info blockheigh0_ where blockheigh0_.event_name=?
Hibernate: select blockheigh0_.pk_id as pk_id1_2_, blockheigh0_.block_height as block_he2_2_, blockheigh0_.event_name as event_na3_2_, blockheigh0_.depot_updatetime as depot_up4_2_ from block_height_info blockheigh0_ where blockheigh0_.event_name=?
Hibernate: select blockheigh0_.pk_id as pk_id1_2_, blockheigh0_.block_height as block_he2_2_, blockheigh0_.event_name as event_na3_2_, blockheigh0_.depot_updatetime as depot_up4_2_ from block_height_info blockheigh0_ where blockheigh0_.event_name=?
```

##### 2.2.3.3 检查数据是否已经正常产生

你也可以通过DB来检查，登录你之前配置的数据库，看到自动创建完表的信息，以及表内开始出现数据内容，则代表一切进展顺利。如你可以执行以下命令：
```
# 请用你的配置信息替换掉[]里的配置，并记得删除[]
mysql -u[用户名] -p[密码] -e "use [数据库名]; select count(*) from block_detail_info"
```
如果查询结果非空，出现类似的如下记录，则代表导出数据已经开始运行：
```
+----------+
| count(*) |
+----------+
|      633 |
+----------+
```

##### 2.2.3.4 停止导入程序

```
ps -ef |grep webase-bee |grep -v grep|awk '{print $2}' |xargs kill -9
```

## 3. 存储模型

数据导出中间件会自动将数据导出到存储介质中，每一类数据都有特定的存储格式和模型，以MySQL为例。包括四类数据：区块数据、账户数据、事件数据和交易数据。

### 3.1 区块数据存储模型

区块数据存储模型包括三个数据存储模型，分别为区块基本数据存储模型、区块详细数据存储模型及区块交易数据存储模型。

#### 3.1.1 区块基本数据存储模型

区块基本数据存储模型用于存储区块整体信息，包括链块高和链上当前交易总量，对应数据库表名称为**block_info**，该表中只会有一条记录，该表不能进行分表操作，如下所示。

| 字段 | 类型 | 字段设置 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| pk_id | bigint(20) | Primary key & NOT NULL | 自增 | 主键Id |
| current_block_height | bigint(20) |  |  | 已抓取的块高 |
| status | int |  | 2 | 独立服务使用，处理块信息是否正常 |
| tx_count | bigint(20) |  |  | 链上总交易量 |
| depot_updatetime | datetime |  | 系统时间 | 记录插入/更新时间 |

#### 3.1.2	区块详细数据存储模型

区块详细数据存储模型用于存储每个区块的详细数据，包括区块哈希、块高、出块时间、块上交易量，对应的数据库表名为**block_detail_info**。如下表所示。

| 字段 | 类型 | 字段设置 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| pk_id | bigint(20) | Primary key & NOT NULL | 自增 | 主键Id |
| block_hash | varchar(225) | Unique key & Index |  | 区块哈希 |
| block_height | bigint(20) |  |  | 区块高度 |
| block_tiemstamp | datetime | index |  | 出块时间 |
| tx_count | int(11) |  |  | 当前区块交易量 |
| depot_updatetime | datetime |  | 系统时间 | 记录插入/更新时间 |

#### 3.1.3区块交易数据存储模型

区块交易数据存储模型用于存储每个区块中每个交易的基本信息，包括区块哈希、块高、出块时间、合约名称、方法名称、交易哈希、交易发起方地址、交易接收方地址，对应的数据库表名为**block_tx_detail_info**。如下表所示。

| 字段 | 类型 | 字段设置 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| pk_id | bigint(20) | Primary key & NOT NULL | 自增 | 主键Id |
| block_hash | varchar(225) | Unique key & Index |  | 区块哈希 |
| block_height | bigint(20) |  |  | 区块高度 |
| block_tiemstamp | datetime | index |  | 出块时间 |
| contract_name | varchar(225) |  |  | 该笔交易的合约名称 |
| method_name | varchar(225) |  |  | 该笔交易调用的function名称 |
| tx_hash | varchar(225) |  |  | 交易哈希 |
| tx_from | varchar(225) |  |  | 交易发起方地址 |
| tx_to | varchar(225) |  |  | 交易接收方地址 |
| depot_updatetime | datetime |  | 系统时间 | 记录插入/更新时间 |

### 3.2 账户数据存储模型

账户数据存储模型用于存储区块链网络中所有账户信息，包括账户创建时所在块高、账户所在块的出块时间、账户地址（合约地址）、合约名称。对应的数据库表名为**account_info**。如下表所示。需要注意的是，如果通过嵌套合约隐式调用构造方法，则不会导出。比如A合约中通过关键字new一个B合约，则B合约不会导出。

| 字段 | 类型 | 字段设置 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| pk_id | bigint(20) | Primary key & NOT NULL | 自增 | 主键Id |
| block_height | bigint(20) | index |  | 区块高度 |
| block_tiemstamp | datetime | index |  | 出块时间 |
| contract_address | varchar(225) | index |  | 合约/账户地址 |
| contract_name | varchar(225) |  |  | 合约名称 |
| depot_updatetime | datetime |  | 系统时间 | 记录插入/更新时间 |

### 3.3 事件数据存储模型

事件数据存储模型是根据合约中的事件（Event）自动生成的。一个合约中有多少个事件就会生成多少个对应的事件数据存储表。

#### 3.3.1 事件数据存储命名规则

由于事件数据存储模型是自动生成的，所以事件数据存储表名和表结构及字段命名采用统一的规则。以如下合约作为示例。

```
pragma solidity ^0.4.7;
contract UserInfo {
    bytes32 _userName;
    uint8 _sex;
    
    function UserInfo(bytes32 userName, uint8 sex) public {
        _userName = userName;
        _sex = sex;
    }
    
    event modifyUserNameEvent(bytes32 userName，uint8 sex);
    
    function modifyUserName(bytes32 userName) public returns(bytes32){
        _userName = userName;
        modifyUserNameEvent(_userName，_sex);
        return _userName;
    }
}
```
##### 3.3.1.1	事件表命名规则

事件表命名规则为：合约名称_事件名称，并将合约名称和事件名称中的驼峰命名转化为小写加下划线方式。比如上述合约中合约名称为UserInfo，事件名称为modifyUserNameEvent，则表名称为user_info_modify_user_name_event。

##### 3.3.1.2	事件字段命名规则

事件字段命名规则：事件字段驼峰命名转化为小写加下划线方式。仍以上述合约中modifyUserNameEvent为例，包含字段userName，则在user_info_modify_user_name_event表中对应的字段为user_name。

#### 3.3.2 事件数据存储模型

事件数据存储模型除过存储该事件的相关信息外，还会存储和该事件相关的块和交易信息，如下表所示。

| 字段 | 类型 | 字段设置 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| pk_id | bigint(20) | Primary key & NOT NULL | 自增 | 主键Id |
| block_height | bigint(20) | index |  | 区块高度 |
| block_tiemstamp | datetime | index |  | 出块时间 |
| **event-paralist** |  |  |  | 事件字段列表 |
| tx_hash | varchar(225) | index |  | 交易哈希 |
| depot_updatetime | datetime |  | 系统时间 | 记录插入/更新时间 |

以上述智能合约为例，对应的 **<event-paralist>** 如下：

| 字段 | 类型 | 字段设置 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| user_name | varchar(255) |  |  | 用户名 |
| sex | int |  |  | 性别 |

### 3.4	交易数据存储模型

交易数据存储模型同事件数据存储模型类似，是根据合约中的方法（Function）自动生成的。一个合约中有多少个方法就会生成多少个对应的方法数据存储表。该方法指的是实际产生交易的方法（含构造方法），不包含事件（Event）方法和查询方法（constant关键字标注）。

#### 3.4.1	交易数据存储命名规则

交易数据存储表名、表结构及字段命名规则同事件数据存储模型类似，以3.3.1中的合约为例进行说明。

##### 3.4.1.1	交易表命名规则

交易表命名规则为：合约名称_方法名称，并将合约名称和方法名称中的驼峰命名转化为小写加下划线方式。比如上述合约中合约名称为UserInfo，方法名称为modifyUserName，则表名称为user_info_modify_user_name；构造方法名称为UserInfo，那么对应的表名为user_info_user_info。

##### 3.4.1.2	交易字段命名规则

交易字段命名规则也是将交易参数字段驼峰命名转化为小写加下划线，不再赘述。需要指出的是，对于一些没有参数的方法，交易数据存储模型没有办法存储，即通过无参方法产生的交易明细将无法通过数据导出工具获取到。

#### 3.4.2	交易数据存储模型

交易数据存储模型除过存储该方法的相关信息外，还会存储和该方法相关的块和交易信息，如下表所示。

| 字段 | 类型 | 字段设置 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| pk_id | bigint(20) | Primary key & NOT NULL | 自增 | 主键Id |
| block_height | bigint(20) | index |  | 区块高度 |
| block_tiemstamp | datetime | index |  | 出块时间 |
| **function-paralist** |  |  |  | 方法字段列表 |
| tx_hash | varchar(225) | index |  | 交易哈希 |
| depot_updatetime | datetime |  | 系统时间 | 记录插入/更新时间 |

以**3.3.1**中的合约为例，对应的 **<function-paralist>** 如下：

| 字段 | 类型 | 字段设置 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| user_name | varchar(255) |  |  | 用户名 |
| sex | int |  |  | 性别 |

## 4. 常见问题
> **1. 为啥我的数据里自动生成的表里，只有block_info和block_detail_info表有数据？**

A： 在单机运行的模式下，block_info和block_detail_info表是链的基本数据，只要服务正常运行，这两个表肯定会有数据。

首先，请检查连接的区块链的地址、端口是否正确。

其次，你需要检查合约的版本。如果你升级了合约，但链上执行的合约都是老版本的合约，这个时候就无法获得数据。

最后，需要检查合约中是否定义了Event、显式定义了构造函数；如果没有定义，是不会有Event和构造函数的表的。  

> **2. 我在链上部署了多个项目的合约，其中的包名并不同，能在同一个工程里导出数据吗？**

A： 可以。只需要手动将编译生成的合约代码的包名改为同一个，然后在配置文件中将monitor.contractPackName配置为该包名，并按照之前的方式配置、重启，即可导出所有合约的数据。

> **3. 如果我的链上所执行的合约是低于V1.2.0版本的怎么办？还可以导出来吗？**

A: 可以，但需要进行特殊的操作。 首先，找到你原有的历史合约，然后使用1.2.0版本的web3sdk进行编译得到V1.2.0版本的Java文件，[合约代码转换为java代码](https://fisco-bcos-documentation.readthedocs.io/zh_CN/v1.0.1/docs/web3sdk/advanced/gen_java_code.html?highlight=compile.sh) ，复制每个Java文件里的ABI字段。

然后找到你用之前版本的web3sdk曾经编译的Java代码，将刚才V1.2.0版本Java文件中的ABI字段手工拷贝到之前Java代码中。

最后将此定制的Java代码放入到配置文件夹中，按手册生成和执行。

> **4. 假如我的合约升级了怎么办，能否导出历史和更新后的合约数据？**

A： 可以。 但是会被作为两个数据库表来进行存储，因为合约的数据结构等可能会改变。

操作方法： 你也猜到了，我们建议建立版本号，将升级的合约与旧版本的合约Java文件，使用不同的命名，保存到配置文件下面。

## 5. 使用技术

框架 | 理由
---|---
SpringBoot - Web框架 | 打开Spring全家桶的最佳方式。我们也同样推荐你使用。
Gradle - 依赖属性管理 | 相比于Maven，Gradle更加简洁和强大。
Beetl - 模板引擎 | Beetl在易用性和性能等维度上超越了知名的竞争对手。
incubator-shardingsphere - 分布式数据库中间件 | 很棒的关系型数据库中间件，目前已经进入Apache孵化器。
Elastic-Job-Lite - 分布式调度解决方案 | 轻量级无中心化解决方案，出自shardingsphere同一个团队。

## 6. 版权说明

该项目签署了授权许可，详情请参阅 LICENSE.md。

## 7. 联系我们

## 附录

### 1. 配置参数说明

WEBASE-MONKEY用于生成FISCO-WEBASE-BEE组件实例，在WEBASE-MONKEY组件中配置文件只有一个：application.properties。该配置文件覆盖了数据导出组件所需的所有配置，并提供了详细的说明和样例，开发者可根据需求进行灵活配置。

#### 1.1 Springboot服务配置

| 配置项 | 是否必输 | 说明 | 举例 | 默认值 |
| --- | --- | --- | --- | --- |
| server.port | N | 启动FISCO-WEBASE-BEE组件实例的服务端口 | 8082 | 8080 |

#### 1.2 FISCO-BCOS节点配置

FISCO-BCOS节点配置用于配置FISCO-WEBASE-BEE服务连接的区块链节点，使得FISCO-WEBASE-BEE服务能够访问连接节点，并通过该节点获取区块链网络上的数据。

| 配置项 | 是否必输 | 说明 | 举例 | 默认值 |
| --- | --- | --- | --- | --- |
| system.orgId | N | 组织机构ID，用于区分不同的机构 | 10000 | FB001 |
| system.nodeStr | Y | 连接区块链节点的nodeStr，nodeName@[IP]:[PORT], 其中prot为channel port | node1@106.12.31.123:8822 | - |
| system.keystorePassword | Y | 节点密钥 | 123456 | - |
| system.clientCertPassWord | Y | 证书密钥 | 123456 | - |

#### 1.3 数据库配置

数据导出组件最终会把区块链网络上的数据导出到数据存储介质中，目前版本仅支持MySQL，所以需要进行数据库配置。

| 配置项 | 是否必输 | 说明 | 举例 | 默认值 |
| --- | --- | --- | --- | --- |
| system.dbUrl | Y | 访问数据的URL | jdbc:mysql://[IP]:[PORT]/[DB]?characterEncoding=utf8&useSSL=false&serverTimezone=GMT%2b8 | - |
| system.dbUser | Y | 数据库用户名 | admin | - |
| system.dbPassword | Y | 数据库密码 | 123456 | - |
| system.contractName.[methodName or eventName].shardingNO | N | 合约数据分片数：数据库指定数据表的个数 | system.Rule.NewruleEvent.shardingNO = 3 | 1 |
| system.sys.[sysTableName].shardingNO | N | 系统数据分片数 | system.sys.BlockTxDetailInfo.shardingNO=5 | 1 |

其中**sysTableName**对应区块数据表和账户数据表，详情见 **数据存储模型** 章节。

#### 1.4 FISCO-WEBASE-BEE工程配置

| 配置项 | 是否必输 | 说明 | 举例 | 默认值 |
| --- | --- | --- | --- | --- |
| system.group | Y | 同spring项目的group | com.example | - |
| system.contractPackName | Y | 编译智能合约所输入的包名 | com.webank.blockchain.wecredit.contracts | - |
| monitor.default.frequency | N | 所有method和event的抓取频率 | 10 | 5 |

#### 1.5 线程池配置

在单机部署下，必须配置线程池参数。数据导出配置用于配置数据导出的频率、线程数及启动多线程条件等。当system.multiLiving=true时，配置文件不会生成线程池相关配置。

| 配置项 | 是否必输 | 说明 | 举例 | 默认值 |
| --- | --- | --- | --- | --- |
| system.multiLiving | Y | 关闭多活开关 | false | false |
| system.maxBlockHeightThreshold | N | 多线程开关阈值：当前区块落后区块高度的阈值，如果超过，系统将启动多线程执行任务 | 10 | 10 |
| system.crawlBatchUnit | N | 线程处理单元：多线程任务模式下单个线程一次任务执行完成的区块数 | 100 | 100 |

#### 1.6 集群多活配置

在集群多活部署的方案中，必须设置集群多活的配置。集群必须通过zookeeper进行服务注册和任务分发。当system.multiLiving=false时，配置文件不会生成zookeeper相关配置。

| 配置项 | 是否必输 | 说明 | 举例 | 默认值 |
| --- | --- | --- | --- | --- |
| system.multiLiving | Y | 启动多活开关 | true | false |
| regcenter.serverList | N | 注册中心服务器列表 | [12.00.10.1:2181;12.00.10.2:2181] | - |
| regcenter.namespace | N | 注册中心命名空间 | wecredit_bee | - |


#### 1.7 其他高级配置

| 配置项 | 是否必输 | 说明 | 举例 | 默认值 |
| --- | --- | --- | --- | --- |
| monitor.[contractName].[methodName/eventName].generated=false | N | 是否抓取特定合约中特定method或event的数据 | on/off | on |
| monitor.[contractName].[eventName].ignoreParam=XXX,XXX | N | 忽略特定合约特定event的特定字段不进行抓取 | xxx,xxx |  |
| length.[contractName].[methodName or eventName].paraName | N | 指定特定字段在数据库表中的长度 |  | 512 |

### 2. Java安装

请参考链接：[Java安装](https://fisco-bcos-documentation.readthedocs.io/zh_CN/latest/docs/tools/oracle_java.html)

### 3. Git安装

git：用于拉取最新代码

**centos**:
```
sudo yum -y install git
```

**ubuntu**:
```
sudo apt install git
```

#### 4. Mysql安装

此处以Centos/Fedora为例。

（1）切换到root

```shell
sudo -s
```

（2）安装mysql

```shell
yum install mysql*
#某些版本的linux，需要安装mariadb，mariadb是mysql的一个分支
yum install mariadb*
```

（3）启动mysql

```shell
service mysqld start
#若安装了mariadb，则使用下面的命令启动
service mariadb start
```

（4）初始化root用户

```shell
mysql -u root
```

**注意，以下语句仅适用于开发环境，不能直接在实际生产中使用！！！**

```sql
/*授权test用户本地访问数据库*/
create user 'test'@'localhost' identified by 'test1234';
```
（5）用SQL语句给root分配密码

``` sql
GRANT ALL PRIVILEGES ON *.* TO 'test'@'%' IDENTIFIED BY 'test1234' WITH GRANT OPTION;
```
**注意，以上语句仅适用于开发环境，不能直接在实际生产中使用！！！**

（6）测试是否成功

> 另开一个ssh测试用户是否可以登陆，并成功授权，登陆数据库

```shell
mysql -utest -ptest@2107 -h 127.0.0.1 -P 3306
```

> 登陆成功后，执行sql语句，若出现错误，则用户授权不成功

```sql
show databases;
use test;
select * from tb_txnByDay;
```

#### 5. zookeeper 安装
zookeeper 支持单机和集群部署，推荐使用集群部署的方式，请参考zookeeper官网的说明：

[集群部署](https://zookeeper.apache.org/doc/r3.4.13/zookeeperAdmin.html#sc_zkMulitServerSetup)

[单机部署](https://zookeeper.apache.org/doc/r3.4.13/zookeeperAdmin.html#sc_singleAndDevSetup)

#### 6. supervisor安装与部署

##### 安装脚本
> sudo yum -y install supervisor

会生成默认配置/etc/supervisord.conf和目录/etc/supervisord.d，如果没有则自行创建。

##### 配置脚本
cd /etc/supervisord.d
修改/etc/supervisord.conf的[include]部分：

```shell
[include]
files = supervisord.d/*.ini
[supervisord]
```

在/etc/supervisord.d目录下配置以下启动配置文件webasebee_config1.ini，注意修改相关的路径。
```shell
[program:supervisor_webasebee]
directory =【你的程序路径】/webase-bee/dist ; 程序的启动目录
command = nohup java -jar 【你的安装包名，如webase-bee0.3.0-SNAPSHOT.jar】 & ; 启动命令，与命令行启动的命令是一样的
autostart = true     ; 在 supervisord 启动的时候也自动启动
startsecs = 15        ; 启动 15 秒后没有异常退出，就当作已经正常启动了
autorestart = true   ; 程序异常退出后自动重启
startretries = 3     ; 启动失败自动重试次数，默认是 3
user = app          ; 用哪个用户启动
redirect_stderr = true  ; 把 stderr 重定向到 stdout，默认 false
stdout_logfile_maxbytes = 150MB  ; stdout 日志文件大小，默认 50MB
stdout_logfile_backups = 20     ; stdout 日志文件备份数
stderr_logfile=【你的日志路径】/webase-bee/dist/log/weevent_bee_error.log
stdout_logfile = 【你的日志路径】/webase-bee/dist/log/weevent_out.log  ;日志统一放在log目录下
[supervisord]
```

##### 启动任务
supervisor支持supervisorctl和supervisord启动，可通过systemctl实现开机自启动。
我们建议采用supervisord的方式启动：

```shell
supervisord -c /etc/supervisord.d/webasebee_config1.ini
```

##### 关闭任务
```shell
ps -ef|grep supervisord| awk '{print $2}'|xargs kill -9
ps -ef|grep webase-bee|grep SNAPSHOT| awk '{print $2}'|xargs kill -9
```
