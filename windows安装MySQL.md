# 在windows上安装MySQL

### 1. 官方网址下载 MySQL 

​	从Oracle网站下载Community版本的MySQL。如mysql-8.0.23-winx64.zip。

### 2.安装

​	将mysql-8.0.23-winx64.zip 解压到目标目录。可以看看目录结构非常标准。

#### 2.1 解压

​	将其解压到C:\Program Files\MySQL

	#### 2.2 新建配置文件

​	在MySQL文件夹下，新建my.ini配置文件

​	内容：

```bash
[mysql]

# 设置mysql客户端默认字符集
default-character-set=utf8

[mysqld]

# 设置3306端口
port = 3306

# 设置mysql的安装目录
basedir=C:\Program Files\MySQL

# 设置mysql数据库的数据的存放目录
datadir=C:\Program Files\MySQL\data

# 允许最大连接数
max_connections=20

# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8

# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

#### 2.3 服务安装

​	切换到 `MySQL` 文件夹的 `bin` 目录里。在这个目录里打开管理员模式的 PowerShell。启用管理员模式是因为要读写该目录，而所有 Program Files目录下的文件，都只能在管理员模式下读写。

在 PowerShell 里输入如下命令：

```Powershell
.\mysqld.exe install
```

这一步告诉 Windows 10，要把 MySQL 作为一项服务启动。而 新手可能对 `mysqld` 这个词语中的最后一个字母 `d` 不太理解，好好的 `MySQL` 为什么加一个后缀 `d`？其实，这个字母d是指 daemon，学过操作系统原理的你，应该知道有一类很特殊的进程叫做 **守护进程**，其作用就是作为一项服务存在。你因该猜到了，这个后缀 `d`指的就是守护进程，每次使用 MySQL 之前都要启动这个进程。新手应该逐渐收集这种计算机“黑话”并加以记忆和联想。

#### 2.4 初始化数据库

在bin目录下继续输入命令

```powershell
.\mysqld.exe --initialize --console
```

`--initialize` 会告诉 MySQL 根据`my.ini`中的字段，创建一个系统数据库以及初始化数据文件目录，这个地方还会让 MySQL 生成一个随机的 root 用户的密码并输出在屏幕上。一定要看清楚并记住这个密码，否则你无法第一次登录 MySQL，切记！

#### 2.5 启动服务

启动 MySQL 服务。

在bin目录下，继续输入命令：

```powershell
net start mysql
```

运行完这个命令，屏幕输出会告诉你 MySQL 服务已经启动了。

#### 2.6 配置环境变量

将 `mysql.exe` 的路径写入系统的 `PATH` 环境变量。Windows的环境变量是通过图形化方式管理的，这与 UNIX 系列系统有很大不同。个人认为 Windows 的管理比较简单，还算不错吧。

写入方法也很简单，在文件管理器的地址栏，输入 `控制面板\系统和安全\系统`，在弹出界面的左边找到 `高级系统设置`，进入，单击 `环境变量`。在弹出的对话框里双击 `PATH` 哪一行，系统会再弹出一个对话框。选择 `新建`，输入`C:\Program Files\MySQL\bin`。

这个路径是你的 MySQL 程序的地址。如果你安装在了其他地方，那就自定义设置。一路确定，并退出。

#### 2.7 登录MySQL

重新打开一个 PowerShell窗口，一定要重新打开，否则环境变量不生效。

在新 PowerShell 窗口下输入

```bash
mysql -u root -p
```

这时候会让你输入密码，密码在第 3 步已经详细说了。输入，Enter！顺利的话，你就进入系统了。

重新设置密码：

```sql
ALTER USER 'root'@'localhost' identified with mysql_native_password by '<你的密码>';
```

之后就可以在任意窗口下，通过新的密码登录 MySQL 了。



