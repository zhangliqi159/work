# mysql的密码找回
### 方法一
1. 打开mysql.exe和mysqld.exe所在的文件夹,复制路径地址
2. 打开cmd命令提示符，进入上一步mysql.exe所在的文件夹
3. 输入命令  mysqld --skip-grant-tables  回车，此时就跳过了mysql的用户验证。（输入此命令之后命令行就无法操作了，此时可以再打开一个新的命令行）
在输入此命令之前先在任务管理器中结束mysqld.exe进程，确保mysql服务器端已结束运行）
4. 然后直接输入mysql，不需要带任何登录参数直接回车就可以登陆上数据库
5. 输入show databases;   可以看到所有数据库说明成功登陆
6. 其中mysql库就是保存用户名的地方。输入 use mysql;   选择mysql数据库
7. show tables查看所有表，会发现有个user表，这里存放的就是用户名，密码，权限等等账户信息
8. 输入select user,host,password from user;   来查看账户信息
9. 更改root密码，输入update user set password=password('123456') where user='root' and host='localhost';
10. 再次查看账户信息，select user,host,password from user;   可以看到密码已被修改
11. 退出命令行，重启mysql数据库，即可用新密码成功登录
****************************************
### 方法二
1. 新开一个命令行运行：mysql -u root （如果没有配置mysql的bin环境变量的话需要切换到bin目录下执行此语句）
2. 在命令行执行这个语句（select host,user,password from mysql.user;）
3. 如果要修改密码的话，在命令行下执行下面的语句（update mysql.user set password='要设置的密码' where user='root';）
