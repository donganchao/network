# 简易c/s通信（10/14）  
## 使用说明：  
1.本地测试：（client.cpp文件中line28，server端地址为本机地址127.0.0.1）  
  ——linux下将两个c++文件用g++编译，命令：g++ server.cpp -o server  g++ client.cpp -o client；  
  ——在对应目录里找到两个生成的程序server和client并运行，命令：(sudo) ./server  ./client；  
  ——在client端输入相应子串server端即可得到响应；  
2.局域网下不同主机测试：（client.cpp文件中line28，server端地址为对应server端主机ip地址）  
  ——确保两台主机在同一局域网中，作server端主机查本机ip地址，命令：ifconfig（linux）/ipconfig（Windows），client端修改文件对应地址并ping该ip地址保证连通；  
  ——注意防火墙策略，如果不通可能是被防火墙过滤，关闭防火墙命令：service iptables stop；  
  ——其他步骤参考本地测试时步骤；  
