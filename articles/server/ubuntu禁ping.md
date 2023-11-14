使用`vi /etc/sysctl.conf`命令打开配置文件，在最后一行加上`net.ipv4.icmp_echo_ignore_all = 1`，按`Esc`键，输入`:wq`保存即可完成禁ping操作。

修改完成之后，需要使用`sudo sysctl -p`命令让它实时生效，当然你也可以重启后自动生效。