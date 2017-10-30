#  有关socket通信的总结   

##  一、socket基本概念

1.Socket是对TCP/IP的一种封装，将复杂的协议隐藏在socket接口后面，用户通过接口让socket去组织数据以符合指定的协议；   
2.Socket可以认为是一种网络间不同计算机上进程通信的一种方法，利用三元组（ip地址，协议，端口）就可以唯一标识
网络中的进程，网络中的进程通信可以利用这个标志与其它进程进行交互。

## 二、最基本的socket通信过程与调用的函数：
 
### 1.socket（）创建套接字：
*  int socket(int domain, int type, int protocol)：domain指定协议族，type指定socket类型，protocol指定协议（注：type和protocol并非随意组合）
；    
*  socket函数类似于普通文件的打开操作，普通文件的打开操作返回一个文件描述字，而socket()用于创建一个socket描述字（socket descriptor），
它唯一标识一个socket；

### 2.bind（）分配套接字地址：  
*  int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen)：sockfd是socket函数创建的描述字，*addr指向要绑定给sockfd的协议地址，
addrlen是对应的地址长度；  
*  通常server端在启动的时候都会绑定一个众所周知的地址（如ip地址+端口号）用于提供服务，client端可以通过它来接连服务器；而client端可以不用指定，它
有系统自动分配一个端口号和自身的ip地址组合，因此server端在listen之前会调用bind()，而client端就不会调用，而是在connect()时由系统随机生成一个；  

### 3.listen()等待连接请求/connect()请求连接/accept()允许连接请求：  
*  int listen(int sockfd, int backlog)：server端，sockfd是要监听的socket描述字，backlog是可以排队的最大连接个数；  
*  int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen)：client端，sockfd是client端socket描述字，*addr是server端socket
地址，addrlen是其地址长度；  
*  int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen)：server端，sockfd是server端socket描述字，*addr指向返回client端的协议地址，
*addrlen是地址长度；
 
### 4.read()/write() 数据交换：  
*  开始调用网络I/O进行读写操作；  

### 5.close()关闭连接：  
*  类似于普通文件操作完后关闭文件的动作；  



