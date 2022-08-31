![image](https://user-images.githubusercontent.com/62527778/187800981-1b9e2a47-6dc5-43b9-b8d1-69b4e3ca7547.png)

①建立连接（Connectors&Connection Pool），通过客户端/服务器通信协议与MySQL建立连接。MySQL 客户端与服务端的通信方式是 “ 半双工 ”。对于每一个 MySQL 的连接，时刻都有一个线程状态来标识这个连接正在做什么。

通讯机制：

  全双工：能同时发送和接收数据，例如平时打电话。

  半双工：指某一时刻，要么发送数据，要么接收数据，不能同时。例如早期对讲机。
  
  单工：只能发送数据或者只能接收数据。例如单行道

线程状态：

  show processlist; // 查看用户正在运行的线程信息，root用户能查看所有线程，其他用户只能看自己的
  
  ![image](https://user-images.githubusercontent.com/62527778/187801050-a0148a74-85fd-48a5-a042-f2f1620b4aa0.png)

  Id: 线程ID，可以使用kill xx;
  
  User: 启动这个线程的用户

  Host：发送请求客户端的IP和端口号
  
  db：当前命令在哪个库执行
  
  Command：该线程正在执行的操作命令
  
  Time：表示该线程处于当前状态的时间，单位是秒
  
  State：线程状态
  
  Info：一般记录线程执行的语句，默认显示前100个字符。想查看完整的使用show full processlist;
