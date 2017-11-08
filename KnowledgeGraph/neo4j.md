# neo4j  

## 一、关于neo4j  

*  以Java实现，使用图（graph）的概念来进行建模的数据库，属于非关系型数据库（NoSQL）；  
*  neo4j最基本的元素为节点和边，分别对应实体和实体间关系，数据保存的格式不是表和集合而是实体和关系，节点和边都有自身的属性（详见[Nodes&Relationships](https://neo4j.com/docs/developer-manual/3.2/cypher/syntax/values/#_structural_types)）；  
*  对于对象模型本身就是一个图结构的应用，使用 Neo4j 这样的图形数据库进行存储是最适合的，因为在进行模型转换时的代价最小（如社交网络）；  
*  不适合使用neo4j数据库的情况：  
 1.记录大量基于事件的数据（例如日志条目或传感器数据）  
 2.对大规模分布式数据进行处理，类似于Hadoop  
 3.二进制数据存储  
 4.适合于保存在关系型数据库中的结构化数据  
* 有自己的语言Cypher（Cypher为ASCII风格的语法，它在括号内表示节点名称，并用箭头表示一个节点指向另一个节点的关系），对Java和Python有很好的支持；

## 二、安装与使用

### 安装：  
*  Linux、Mac、Windows均可安装，详见[Installation](https://neo4j.com/docs/operations-manual/3.2/installation/),以下为Linux；  
* 1.先安装Java，详见[Prerequisite：Install Java 8](https://neo4j.com/docs/operations-manual/3.2/installation/linux/debian/#debian-ubuntu-prerequisites)  
  2.下载压缩包，地址：[https://neo4j.com/download/other-releases/](https://neo4j.com/download/other-releases/)  （选Debian/Ubuntu的压缩包）  
  3.使用tar命令解压：``` tar -xf <filename>```  
 
### 使用:  
* 解压后，进入bin文件夹下运行 ```./neo4j start```，打开浏览器输入地址：http://localhost:7474/ 即可；  
* 关于其中的文件夹：
  bin - scripts and other executables；
  conf - server configuration；
  data - databases；
  lib - libraries；
  plugins - user extensions；
  logs - log files；
  import - location of files for LOAD CSV；  
#### 如何创建/导入数据（以.csv格式文件为例）：
  
* 通过Cypher创建数据：
```  
CREATE (A: PLAYER {name: 'A', height: '1.70m', nationality: 'China'})
MERGE (A)-[:LIKES{since:'2014'}]->(B: SINGER{name:'B',bloodType:'O'})
```  
更多关于Cypher参考：  
https://neo4j.com/docs/developer-manual/3.2/cypher/
https://www.w3cschool.cn/neo4j/neo4j_cql_introduction.html  

* 通过已有数据生成新数据库：  
1.将[例子](https://neo4j.com/docs/operations-manual/3.2/tutorial/import-tool/#import-tool-basic-example)（movies.csv；actors.csv；roles.csv）通过gedit编辑保存为.csv文件；  
2.进入bin文件夹下通过neo4j-admin程序创建新数据库： （填写储存.csv文件的绝对路径） ```./neo4j-admin import --mode=csv --database=instance.db --nodes /home/dac/Desktop/movies.csv --nodes /home/dac/Desktop/actors.csv --relationships /home/dac/Desktop/roles.csv```  
3.进入conf文件夹下用gedit打开neo4j.conf配置文件，修改第九行为：```dbms.active_database=instance.db```   


* 将已有数据导入数据库：  
1.将需要导入的.csv文件copy到import文件夹下；  
2.通过```LOAD CSV```语句导入，参见：https://neo4j.com/docs/developer-manual/3.2/cypher/clauses/load-csv/#query-load-csv