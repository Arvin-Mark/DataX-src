
# System Requirements

- Linux
- [JDK(1.6以上，推荐1.6) ](http://www.oracle.com/technetwork/cn/java/javase/downloads/index.html)
- [Python(推荐Python2.6.X) ](https://www.python.org/downloads/)
- [Apache Maven 3.x](https://maven.apache.org/download.cgi) (Compile DataX)

# Quick Start

* 工具部署

  * 方法一、直接下载Datax-bin工具包：[DataX-bin](https://github.com/Arvin-Mark/datax-bin)

    下载后解压至本地某个目录，进入bin目录，即可运行同步作业：

    ``` shell
    $ cd  {YOUR_DATAX_HOME}/bin
    $ python datax.py {YOUR_JOB.json}
    ```

  * 方法二、下载DataX-src源码，自己编译：[DataX-src源码](https://github.com/Arvin-Mark/DataX-src)

    (1)、下载DataX源码：

    ``` shell
    $ git clone git@github.com:Arvin-Mark/DataX-src.git
    ```

    (2)、通过maven打包：

    ``` shell
    $ cd  {DataX_source_code_home}
    $ mvn -U clean package assembly:assembly -Dmaven.test.skip=true
    ```

    打包成功，日志显示如下：

    ```
    [INFO] BUILD SUCCESS
    [INFO] -----------------------------------------------------------------
    [INFO] Total time: 08:12 min
    [INFO] Finished at: 2015-12-13T16:26:48+08:00
    [INFO] Final Memory: 133M/960M
    [INFO] -----------------------------------------------------------------
    ```

    打包成功后的DataX包位于 {DataX_source_code_home}/target/datax/datax-bin/ ，结构如下：

    ``` shell
    $ cd  {DataX_source_code_home}
    $ ls ./target/datax/datax-bin/
    bin		conf		job		lib		log		log_perf	plugin		script		tmp
    ```


* 配置示例：从stream读取数据并打印到控制台

  * 第一步、创建创业的配置文件（json格式）

    可以通过命令查看配置模板： python datax.py -r {YOUR_READER} -w {YOUR_WRITER}

    例如：python datax.py -r streamreader -w streamwriter

    ``` shell
    $ cd  {YOUR_DATAX_HOME}/bin
    $  python datax.py -r streamreader -w streamwriter
    DataX (UNKNOWN_DATAX_VERSION), From Alibaba !
    Copyright (C) 2010-2015, Alibaba Group. All Rights Reserved.
    Please refer to the streamreader document:
        * [https://github.com/Arvin-Mark/DataX-src/blob/master/streamreader/doc/streamreader.md](https://github.com/Arvin-Mark/DataX-src/blob/master/streamreader/doc/streamreader.md)

    Please refer to the streamwriter document:
        * [https://github.com/Arvin-Mark/DataX-src/blob/master/streamwriter/doc/streamwriter.md](https://github.com/Arvin-Mark/DataX-src/blob/master/streamwriter/doc/streamwriter.md)

    Please save the following configuration as a json file and  use
         python {DATAX_HOME}/bin/datax.py {JSON_FILE_NAME}.json
    to run the job.

    {
        "job": {
            "content": [
                {
                    "reader": {
                        "name": "streamreader",
                        "parameter": {
                            "column": [],
                            "sliceRecordCount": ""
                        }
                    },
                    "writer": {
                        "name": "streamwriter",
                        "parameter": {
                            "encoding": "",
                            "print": true
                        }
                    }
                }
            ],
            "setting": {
                "speed": {
                    "channel": ""
                }
            }
        }
    }
    ```

    根据模板配置json如下：

    ``` json
    #stream2stream.json
    {
      "job": {
        "content": [
          {
            "reader": {
              "name": "streamreader",
              "parameter": {
                "sliceRecordCount": 10,
                "column": [
                  {
                    "type": "long",
                    "value": "10"
                  },
                  {
                    "type": "string",
                    "value": "hello，你好，世界-DataX"
                  }
                ]
              }
            },
            "writer": {
              "name": "streamwriter",
              "parameter": {
                "encoding": "UTF-8",
                "print": true
              }
            }
          }
        ],
        "setting": {
          "speed": {
            "channel": 5
           }
        }
      }
    }
    ```

  * 第二步：启动DataX

    ``` shell
    $ cd {YOUR_DATAX_DIR_BIN}
    $ python datax.py ./stream2stream.json
    ```

    同步结束，显示日志如下：

    ``` shell
    ...
    2015-12-17 11:20:25.263 [job-0] INFO  JobContainer -
    任务启动时刻                    : 2015-12-17 11:20:15
    任务结束时刻                    : 2015-12-17 11:20:25
    任务总计耗时                    :                 10s
    任务平均流量                    :              205B/s
    记录写入速度                    :              5rec/s
    读出记录总数                    :                  50
    读写失败总数                    :                   0
    ```

# Support Data Channels

目前DataX支持的数据源有:

### Reader
----

> **Reader实现了从数据存储系统批量抽取数据，并转换为DataX标准数据交换协议，DataX任意Reader能与DataX任意Writer实现无缝对接，达到任意异构数据互通之目的。**

----

**RDBMS 关系型数据库**

* [MysqlReader](https://github.com/Arvin-Mark/DataX-src/blob/master/mysqlreader/doc/mysqlreader.md): 使用JDBC批量抽取Mysql数据集。
* [OracleReader](https://github.com/Arvin-Mark/DataX-src/blob/master/oraclereader/doc/oraclereader.md): 使用JDBC批量抽取Oracle数据集。
* [SqlServerReader](https://github.com/Arvin-Mark/DataX-src/blob/master/sqlserverreader/doc/sqlserverreader.md): 使用JDBC批量抽取SqlServer数据集
* [PostgresqlReader](https://github.com/Arvin-Mark/DataX-src/blob/master/postgresqlreader/doc/postgresqlreader.md): 使用JDBC批量抽取PostgreSQL数据集
* [DrdsReader](https://github.com/Arvin-Mark/DataX-src/blob/master/drdsreader/doc/drdsreader.md): 针对公有云上DRDS的批量数据抽取工具。

**数仓数据存储**

* [ODPSReader](https://github.com/Arvin-Mark/DataX-src/blob/master/odpsreader/doc/odpsreader.md): 使用ODPS Tunnel SDK批量抽取ODPS数据。

**NoSQL数据存储**

* [OTSReader](https://github.com/Arvin-Mark/DataX-src/blob/master/otsreader/doc/otsreader.md): 针对公有云上OTS的批量数据抽取工具。
* [HBaseReader](https://github.com/Arvin-Mark/DataX-src/blob/master/hbasereader/doc/hbasereader.md): 针对 HBase 0.94版本的在线数据抽取工具
* [MongoDBReader](https://github.com/Arvin-Mark/DataX-src/blob/master/mongodbreader/doc/mongodbreader.md)：MongoDBReader

**无结构化数据存储**

* [TxtFileReader](https://github.com/Arvin-Mark/DataX-src/blob/master/txtfilereader/doc/txtfilereader.md): 读取(递归/过滤)本地文件。
* [FtpReader](https://github.com/Arvin-Mark/DataX-src/blob/master/ftpreader/doc/ftpreader.md): 读取(递归/过滤)远程ftp文件。
* [HdfsReader](https://github.com/Arvin-Mark/DataX-src/blob/master/hdfsreader/doc/hdfsreader.md): 针对Hdfs文件系统中textfile和orcfile文件批量数据抽取工具。
* [OssReader](https://github.com/Arvin-Mark/DataX-src/blob/master/ossreader/doc/ossreader.md): 针对公有云OSS产品的批量数据抽取工具。
* [streamreader](https://github.com/Arvin-Mark/DataX-src/blob/master/streamreader/doc/streamreader.md)：StreamReader
* [rdbmsreader](https://github.com/Arvin-Mark/DataX-src/blob/master/rdbmsreader/doc/rdbmsreader.md)：rdbmsreader

### Writer

----

> **Writer实现了从DataX标准数据交换协议，翻译为具体的数据存储类型并写入目的数据存储。DataX任意Writer能与DataX任意Reader实现无缝对接，达到任意异构数据互通之目的。**

----

**RDBMS 关系型数据库**

* [MysqlWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/mysqlwriter/doc/mysqlwriter.md): 使用JDBC(Insert,Replace方式)写入Mysql数据库
* [OracleWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/oraclewriter/doc/oraclewriter.md): 使用JDBC(Insert方式)写入Oracle数据库
* [PostgresqlWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/postgresqlwriter/doc/postgresqlwriter.md): 使用JDBC(Insert方式)写入PostgreSQL数据库
* [SqlServerWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/sqlserverwriter/doc/sqlserverwriter.md): 使用JDBC(Insert方式)写入sqlserver数据库
* [DrdsWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/drdswriter/doc/drdswriter.md): 使用JDBC(Replace方式)写入Drds数据库

**数仓数据存储**

* [ODPSWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/odpswriter/doc/odpswriter.md): 使用ODPS Tunnel SDK向ODPS写入数据。
* [ADSWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/adswriter/doc/adswriter.md): 使用ODPS中转将数据导入ADS。

**NoSQL数据存储**

* [OTSWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/otswriter/doc/otswriter.md): 使用OTS SDK向OTS Public模型的表中导入数据。
* [hbasewriter](https://github.com/Arvin-Mark/DataX-src/blob/master/hbasewriter/doc/hbasewriter.md)：hbasewriter
* [OCSWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/ocswriter/doc/ocswriter.md)：OCSWriter
* [MongoDBWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/mongodbwriter/doc/mongodbwriter.md)：MongoDBWriter

**无结构化数据存储**

* [TxtFileWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/txtfilewriter/doc/txtfilewriter.md): 提供写入本地文件功能。
* [ftpwriter](https://github.com/Arvin-Mark/DataX-src/blob/master/ftpwriter/doc/ftpwriter.md)：ftpwriter
* [OssWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/osswriter/doc/osswriter.md): 使用OSS SDK写入OSS数据。
* [HdfsWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/hdfswriter/doc/hdfswriter.md): 提供向Hdfs文件系统中写入textfile文件和orcfile文件功能。
* [StreamWriter](https://github.com/Arvin-Mark/DataX-src/blob/master/streamwriter/doc/streamwriter.md)：StreamWriter
* [rdbmswriter](https://github.com/Arvin-Mark/DataX-src/blob/master/rdbmswriter/doc/rdbmswriter.md)：rdbmswriter

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

Google Groups: [DataX-user](https://github.com/Arvin-Mark/DataX-src)
