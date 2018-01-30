![Datax-logo](https://github.com/Arvin-Mark/DataX-src/blob/master/images/DataX-logo.jpg)



# DataX

DataX 是异构数据广泛使用的离线数据同步工具/平台，实现包括 MySQL、Oracle、SqlServer、Postgre、HDFS、Hive、ADS、HBase、OTS、ODPS 等各种异构数据源之间高效的数据同步功能。



# Features

DataX本身作为数据同步框架，将不同数据源的同步抽象为从源头数据源读取数据的Reader插件，以及向目标端写入数据的Writer插件，理论上DataX框架可以支持任意数据源类型的数据同步工作。同时DataX插件体系作为一套生态系统, 每接入一套新数据源该新加入的数据源即可实现和现有的数据源互通。



# Quick Start

##### Download [Datax-bin下载地址](https://github.com/Arvin-Mark/datax-bin/archive/master.zip)

##### 请点击：[Quick Start](https://github.com/Arvin-Mark/DataX-src/blob/master/userGuid.md)



# Support Data Channels

DataX目前已经有了比较全面的插件体系，主流的RDBMS数据库、NOSQL、大数据计算系统都已经接入，目前支持数据如下图，配置详情请点击图下列出DataX数据源参考指南

| 类型           | 数据源        | Reader(读) | Writer(写) |
| ------------ | ---------- | :-------: | :-------: |
| RDBMS 关系型数据库 | Mysql      |     √     |     √     |
|              | Oracle     |     √     |     √     |
|              | SqlServer  |     √     |     √     |
|              | Postgresql |     √     |     √     |
|              | 达梦         |     √     |     √     |
| 阿里云数仓数据存储    | ODPS       |     √     |     √     |
|              | ADS        |           |     √     |
|              | OSS        |     √     |     √     |
|              | OCS        |     √     |     √     |
| NoSQL数据存储    | OTS        |     √     |     √     |
|              | Hbase0.94  |     √     |     √     |
|              | Hbase1.1   |     √     |     √     |
|              | MongoDB    |     √     |     √     |
| 无结构化数据存储     | TxtFile    |     √     |     √     |
|              | FTP        |     √     |     √     |
|              | HDFS       |     √     |     √     |




# Support Data Channels List

* [adswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/adswriter/doc/adswriter.md)
* [drdsreader](https://github.com/Arvin-Mark/DataX-src/blob/master/drdsreader/doc/drdsreader.md)
* [drdswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/drdswriter/doc/drdswriter.md)
* [ftpreader](https://github.com/Arvin-Mark/DataX-src/blob/master/ftpreader/doc/ftpreader.md)
* [ftpwriter](https://github.com/Arvin-Mark/DataX-src/blob/master/ftpwriter/doc/ftpwriter.md)
* [hbase](https://github.com/Arvin-Mark/DataX-src/blob/master/hbase094xreader/doc/hbase094xreader.md)
* [hbase094xreader](https://github.com/Arvin-Mark/DataX-src/blob/master/hbase094xwriter/doc/hbase094xwriter.md)
* [hbase11xreader](https://github.com/Arvin-Mark/DataX-src/blob/master/hbase11xreader/doc/hbase11xreader.md)
* [hbase11xwriter](https://github.com/Arvin-Mark/DataX-src/blob/master/hbase11xwriter/doc/hbase11xwriter.md)
* [hbasereader](https://github.com/Arvin-Mark/DataX-src/blob/master/hbasereader/doc/hbasereader.md)
* [hbasewriter](https://github.com/Arvin-Mark/DataX-src/blob/master/hbasewriter/doc/hbasewriter.md)
* [hdfsreader](https://github.com/Arvin-Mark/DataX-src/blob/master/hdfsreader/doc/hdfsreader.md)
* [hdfswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/hdfswriter/doc/hdfswriter.md)
* [mongodbreader](https://github.com/Arvin-Mark/DataX-src/blob/master/mongodbreader/doc/mongodbreader.md)
* [mongodbwriter](https://github.com/Arvin-Mark/DataX-src/blob/master/mongodbwriter/doc/mongodbwriter.md)
* [mysqlreader](https://github.com/Arvin-Mark/DataX-src/blob/master/mysqlreader/doc/mysqlreader.md)
* [mysqlwriter](https://github.com/Arvin-Mark/DataX-src/blob/master/mysqlwriter/doc/mysqlwriter.md)
* [ocswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/ocswriter/doc/ocswriter.md)
* [odpsreader](https://github.com/Arvin-Mark/DataX-src/blob/master/odpsreader/doc/odpsreader.md)
* [odpswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/odpswriter/doc/odpswriter.md)
* [oraclereader](https://github.com/Arvin-Mark/DataX-src/blob/master/oraclereader/doc/oraclereader.md)
* [oraclewriter](https://github.com/Arvin-Mark/DataX-src/blob/master/oraclewriter/doc/oraclewriter.md)
* [ossreader](https://github.com/Arvin-Mark/DataX-src/blob/master/ossreader/doc/ossreader.md)
* [osswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/osswriter/doc/osswriter.md)
* [otsreader](https://github.com/Arvin-Mark/DataX-src/blob/master/otsreader/doc/otsreader.md)
* [otswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/otswriter/doc/otswriter.md)
* [postgresqlreader](https://github.com/Arvin-Mark/DataX-src/blob/master/postgresqlreader/doc/postgresqlreader.md)
* [postgresqlwriter](https://github.com/Arvin-Mark/DataX-src/blob/master/postgresqlwriter/doc/postgresqlwriter.md)
* [rdbmsreader](https://github.com/Arvin-Mark/DataX-src/blob/master/rdbmsreader/doc/rdbmsreader.md)
* [rdbmswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/rdbmswriter/doc/rdbmswriter.md)
* [sqlserverreader](https://github.com/Arvin-Mark/DataX-src/blob/master/sqlserverreader/doc/sqlserverreader.md)
* [sqlserverwriter](https://github.com/Arvin-Mark/DataX-src/blob/master/sqlserverwriter/doc/sqlserverwriter.md)
* [streamreader](https://github.com/Arvin-Mark/DataX-src/blob/master/streamreader/doc/streamreader.md)
* [streamwriter](https://github.com/Arvin-Mark/DataX-src/blob/master/streamwriter/doc/streamwriter.md)
* [txtfilereader](https://github.com/Arvin-Mark/DataX-src/blob/master/txtfilereader/doc/txtfilereader.md)
* [txtfilewriter](https://github.com/Arvin-Mark/DataX-src/blob/master/txtfilewriter/doc/txtfilewriter.md)



# Contact us

系统问题请及时提出在issue。请前往：[DataxIssue](https://github.com/Arvin-Mark/DataX-src/issues)

钉钉&微信扫描以下二维码加入交流群：

![DataX-OpenSource-DingTalk](https://github.com/Arvin-Mark/DataX-src/blob/master/images/DataX-DingTalk.png)

![DataX-OpenSource-WeChat](https://github.com/Arvin-Mark/DataX-src/blob/master/images/DataX-WeChat.png)
