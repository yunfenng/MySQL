MySQL存储引擎

存储引擎在MySQL的体系架构中位于第三层，负责MySQL中的数据的存储和提取，是与文件打交道的子系统，它是根据MySQL提供的文件访问层抽象接口定制的一种文件访问机制，这种机制就叫作存储引擎。
使用show engines命令，就可以查看当前数据库支持的引擎信息。

![image](https://user-images.githubusercontent.com/62527778/188256532-f4afdd14-4781-40fd-92e6-50435f484080.png)

在5.5版本之前默认采用MyISAM存储引擎，从5.5开始采用InnoDB存储引擎。

  InnoDB：支持事务，具有提交，回滚和崩溃恢复能力，事务安全
  
  MyISAM：不支持事务和外键，访问速度快
  
  Memory：利用内存创建表，访问速度非常快，因为数据在内存，而且默认使用Hash索引，但是一旦关闭，数据就会丢失
  
  Archive：归档类型引擎，仅能支持insert和select语句
  
  Csv：以CSV文件进行数据存储，由于文件限制，所有列必须强制指定not null，另外CSV引擎也不支持索引和分区，适合做数据交换的中间表
  
  BlackHole: 黑洞，只进不出，进来消失，所有插入数据都不会保存
  
  Federated：可以访问远端MySQL数据库中的表。一个本地表，不保存数据，访问远程表内容。
  
  MRG_MyISAM：一组MyISAM表的组合，这些MyISAM表必须结构相同，Merge表本身没有数据，对Merge操作可以对一组MyISAM表进行操作。
