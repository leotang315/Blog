# linux设置静态IP方法

### 1. 进入 /etc/sysconfig/network-scripts

### 2. vim ifcfg-ens32，修改配置如下：

​	2.1 修改该文件属性

​		BOOTPROTO=static 

​    	ONBOOT=yes

​	2.2 而后在配置文件内追加配置如下：

​		IPADDR=192.168.1.201   

​		NETMASK=255.255.255.0 

​		GATEWAY=192.168.1.1

​		DNS1 = 192.168.1.1

![1](.\res\1.PNG)

### 3. 退出 vim 编辑，重启网卡：

​	systemctl restart network

### 4. 测试效果

​	ping 百度：ping www.baidu.com