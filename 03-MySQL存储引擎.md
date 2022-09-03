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

3.1 InnoDB和MyISAM对比

InnoDB和MyISAM是使用MySQL时最常用的两种引擎类型，重点看下两者区别。

事务和外键

  InnoDB支持事务和外键，具有安全性和完整性，适合大量insert或update操作
  
  MyISAM不支持事务和外键，它提供高速存储和检索，适合大量的select查询操作

锁机制

  InnoDB支持行级锁，锁定指定记录。基于索引来加锁实现。
  
  MyISAM支持表级锁，锁定整张表。
  
索引结构

  InnoDB使用聚集索引（聚簇索引），索引和记录在一起存储，既缓存索引，也缓存记录。
  
  MyISAM使用非聚集索引（非聚簇索引），索引和记录分开。
  
并发处理能力

  MyISAM使用表锁，会导致写操作并发率低，读之间并不阻塞，读写阻塞。
  
  InnoDB读写阻塞可以与隔离级别有关，可以采用多版本并发控制（MVCC）来支持高并发。
  
存储文件

  InnoDB表对应两个文件，一个.frm表结构文件，一个.ibd数据文件。InnoDB表最大支持64TB；
  
  MyISAM表对应三个文件，一个.frm表结构文件，一个MYD表数据文件，一个.MYI索引文件。从MySQL5.0开始默认限制是256TB。
  
  ![image](https://user-images.githubusercontent.com/62527778/188273098-cf5b9cb8-8cbf-4950-8da0-00a68c31d2ff.png)

适用场景

MyISAM

  不需要事务支持（不支持）
  
  并发相对较低（锁定机制问题）
  
  数据修改相对较少，以读为主
  
  数据一致性要求不高
  
InnoDB
  需要事务支持（具有较好的事务特性）
  
  行级锁定对高并发有很好的适应能力
  
  数据更新较为频繁的场景
  
  数据一致性要求较高
  
  硬件设备内存较大，可以利用InnoDB较好的缓存能力来提高内存利用率，减少磁盘IO
  
总结

两种引擎该如何选择？

  是否需要事务？有，InnoDB
  
  是否存在并发修改？有，InnoDB
  
  是否追求快速查询，且数据修改少？是，MyISAM
  
  在绝大多数情况下，推荐使用InnoDB
  
扩展资料：各个存储引擎特性对比

  ![image](https://user-images.githubusercontent.com/62527778/188273114-29138022-71b4-4ee7-9095-003bf79685c4.png)

  
  
  
  
