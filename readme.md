##Linux 安装vsftpd教程##
1. yum install nginx　　安装nginx
1. service nginx start　　启动nginx
1. yum install vsftpd -y　　安装vsftpd
1. useradd ftpadmin -s /sbin/nologin -d /usr/share/nginx/html　　创建账户ftpadmin，ftpadmin的目录与nginx的目录是同一个目录
1. passwd ftpadmin　　给ftpadmin设置密码
1. vi /etc/vsftpd/vsftpd.conf　　用vi编辑器编辑vsfptd配置文件  
vi编辑器的使用方法。打开文件时默认是命令行模式，只能输入命令，不能修改文本。输入:wq!保存修改并退出，:q！不保存修改并退出。按i键进入insert模式，就可以修改里面的文本了。按ESC退出insert模式，返回命令行模式。光标的移动方法可按pageUp和pageDown快速上下翻页，也可按方向键调整光标的位置。
1. anonymous_enable=NO　　禁止匿名用户登录
1. chroot_list_enable=YES　　限制ftp目录只能浏览自己的home目录以下的文件
1. pasv_enable=YES
   pasv_address=106.14.151.136
   pasv_addr_resolve=yes　　由于阿里云的限制，不支持vsftpd的被动模式，在这里手动配置一下就可以了。腾讯云没有限制，所以不用配置这个。
1. chroot_list_file=/etc/vsftpd/chroot_list　　限制的账户名列表
1. allow_writeable_chroot=YES　　如果ftp客户端连接报错:响应:	500 OOPS: vsftpd: refusing to run with writable root inside chroot(),在vsftpd配置文件中加入这个就行了

1. chkconfig --list　　查看开机自启命令
1. chkconfig --level 35 vsftpd on　　将vsftpd设置为开机自启
1. chkconfig --list　　查看设置好的结果
1. cd /usr/share/nginx/　　打开nginx目录
1. ls -lrth　　查看nginx目录下的html目录的账户权限
1. chown ftpadmin html　　让ftpadmin对目录html有操作权限
1. ls -lrth　　查看设置好的目录权限
1. service vsftpd start　　一切都弄好后启动vsftpd
