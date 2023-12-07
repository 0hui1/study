# Linux常用命令
* ls-查看当前目录下的文件 
	* ls -l 详细查看文件内容
	* ls -a 查看所有文件，包括隐藏文件
* cd-进入当前目录
	* cd.. 进入当前目录上一级
	* cd~ 进入当前目录家目录
* pwd 查看当前文件目录 
* yum install -y 安装软件
* yum search 命令 查找该命令在哪个包中
* ping 链接 
	* ping www.baidu.com /ping baidu.com一般用来检查是否能联网
* ip addr 查看IP地址
* nmtui 查询网卡配置
* tree 以树状图显示目录
	* tree -L 1 / 显示根目录的第一级目录
	* tree -d / 只显示目录
	* tree -Ld 1 /etc 或者 tree -dL 1 /etc 只显示etc下的第一级目录
* mkdir /hui 创建目录
	|命令|功能|
	---|---
	|mkdir -pv /hui/1/2/3|显示创建过程 
	|mkdir -p /hui/1/2/3|创建多层目录
* touch 创建文件-创建多个文件加空格
* touch hui{01..10} 批量创建多个文件
~~~
[root@CentOS hui]# touch text1.txt vidio.avi text
[root@CentOS hui]# ls -l
total 0
-rw-r--r-- 1 root root 0 Aug 10 19:50 text
-rw-r--r-- 1 root root 0 Aug 10 19:50 text1.txt
-rw-r--r-- 1 root root 0 Aug 10 19:50 vidio.avi

[root@CentOS hui]# touch hui{01..10}
[root@CentOS hui]# ls -l
total 0
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui01
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui02
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui03
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui04
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui05
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui06
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui07
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui08
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui09
-rw-r--r-- 1 root root 0 Aug 10 23:14 hui10
-rw-r--r-- 1 root root 0 Aug 10 19:50 text
-rw-r--r-- 1 root root 0 Aug 10 19:50 text1.txt
-rw-r--r-- 1 root root 0 Aug 10 19:50 vidio.avi
~~~
* cp 源路径文件 目标路径  ------单一文件copy
* cp 文件 文件 文件 目标路径 ------多文件copy
* cp 备份要在目标文件后加 .bak (backup)
	* 查找时需要在文件后加*
~~~
[root@CentOS hui]# cp /hui/vidio.avi /hui/vidio.avi.bak 
[root@CentOS hui]# ls -l vidio.avi*
-rw-r--r-- 1 root root 0 Aug 10 19:50 vidio.avi
-rw-r--r-- 1 root root 0 Aug 11 00:13 vidio.avi.bak
~~~
* cp -r  源路径文件 目标路径 ------可以复制目录
	|选项|含义|
	---|---
	|-r|----递归复制，复制目录以及目录内容|
	|-p|复制的时候保持属性不变 
	|-a|相当于 -p -r -d -pdr
	|-d|复制时复制软连接（快捷方式）
~~~
[root@CentOS /]# cp /hui/text1.txt /huicp
[root@CentOS /]# ls -l huicp
total 0
drwxr-xr-x 2 root root 182 Aug 10 23:38 hui
-rw-r--r-- 1 root root   0 Aug 10 23:39 text1.txt
~~~
* mv 源路径文件 目标路径 移动剪切
~~~
[root@CentOS hui]# mv /hui/a.txt /hui02/
[root@CentOS hui]# ls -l /hui02/
total 0
drwxr-xr-x 2 root root 6 Aug 11 00:40 a.txt
~~~
* rm 文件路径 删除文件（只能删除文件）
	* 一般情况下不要删除文件，可以移动到 /tmp/下（类似于windows回收站）
	
	|命令|含义|
	|-|-|
	|-f|强制删除目录|
	|-rf|递归删除目录和目录下所有文件|
* vi 命令 编辑文件 
~~~
#1.存在目录/hui/hui-text.txt/
若目录存在，文件不存在也可创建文件
#2.进入文件
[root@CentOS hui]# vi /hui/hui-text.txt
按 i （insert）进入编辑模式
#3.修改文件内容
按esc键退出编辑模式
#4.保存并退出
：wq
：w（write保存）
：q （quit退出）仅限于未修改文件的情况
：q！强制退出不保存！
#查看文件内容
cat /hui/hui-text.txt
~~~
* cat 查看、显示文件内容
	* cat -n 显示文件内容并添加行号
~~~
[root@CentOS hui]# cat -n /hui/hui-text.txt 
     1	你好
     2	hello
~~~
* 查询命令帮助
	* 方法1 命令 --help 显示简易的帮助
		cat --help
	* 方法2 man 命令
		man cat
		其中name为名字部分
		DESCRIPYTION为命令的详细说明
	* 方法3 info 超级详细的帮助
* wc 统计文件的信息
	分别为行数、单词数、大小
	* 只看行数 wc -l
	~~~
	[root@CentOS hui]# wc /hui/hui-text.txt 
     2  2 13 /hui/hui-text.txt
     [root@CentOS hui]# wc -l /hui/hui-text.txt 
	 2 /hui/hui-text.txt
    ~~~
* 管道 I 用来传递上一个命令的结果
~~~
ps -ef |wc -l  #显示所有进程的数量
ps -ef #显示所有进程
#统计ssh进程的数量
[root@CentOS hui]# ps -ef |grep ssh
root        974      1  0 17:15 ?        00:00:00 /usr/sbin/sshd -D
root       1497    974  0 17:16 ?        00:00:00 sshd: root@pts/0
root       1693   1499  0 19:17 pts/0    00:00:00 grep --color=auto ssh
~~~
* sort 命令 排序
	* seq 10 生成数字
	* seq 10 | sort 将生成的数字排序（按照符号排序）
	* seq 10 | sort -n 将生成的数字排序 （按照数字正序排序）
	* seq 10 | sort -nr 将生成的数字排序 （按照数字逆序排序）
	* sort -nr -k3 指定第三列逆序排序（k后面的数字为指定的列数）
	* sort -nrk3 -k4 根据第三列排序，若第三列相同则根据第四列排序
	* sort -t‘ 分隔符’ -nrk3 -k4  指定第三列中的分隔符来排列
~~~
[root@CentOS ~]# seq 10 | sort
1
10
2
3
4
5
6
7
8
9
~~~
* -rwxrwxr-x 1hui hui 16744 9月 5 11：18 hello
![输入图片说明](/imgs/2023-09-05/477XQBpvYdJextpW.png)
-（小横杠）表示常规文件文件（d开头则为目录文件），前三位表示自己的权限（可读可写可执行）之后三位表示同组权限（可读可写可执行）最后表示普通用户权限
* chmod 改变权限 每三位为一组通过二进制来表示 例如chmod 675
* find /home/hui/ -name ’test1.txt‘在目录下以名字查找文件 
*  find /home/hui/ -type f -name  ’test1.txt‘type 是指文件类型，f是指文件
* find /home/hui/ -type f -name  ‘*.txt’ 模糊搜索 以txt结尾的文件（加个星号）
*  find /home/hui/ -type f -name  ‘*123*’ 模糊搜索 包含123的文件（前后都加星号）
* date 显示时间
	* +表示以。。。格式显示日期
	* +%F 年月日
	* +%T 时分秒 
	* +%w 周几
	* hour 表示小时 min 分钟 sec 秒
	* date + %H：%M：%S
* grep ‘root’ /etc/passwd 过滤，在路径中找出包含root的行
* grep -n ‘root’ /etc/passwd （-n显示行号）
* ps -ef |grep 'sshd' 在所有的进程里找出包含sshd的行
* echo “hello，Linux” 打印字符
* echo -n "hello，Linux" 用来换行
* gzip -k test 压缩文件
* bzip2 -k test  压缩文件（压缩率更高）
*  gzip -dk test.gz 解压缩文件
* bzip2 -dk test.bz2 解压缩文件
* tar 
~~~
tar常用选项
-c(create) 表示创建用来生成文件包
-x：表示提取，从文件包中提取文件
-t可以查看压缩的文件。
-z使用gzip方式进行处理，它与”c“结合就表示压缩，与”x“结合就表示解压缩。
-j使用bzip2方式进行处理，它与”c“结合就表示压缩，与”x“结合就表示解压缩。
-v(verbose)详细报告tar处理的信息
-f(file)表示文件，后面接着一个文件名。 
-C  <指定目录>    解压到指定目录

1.tar打包、gzip压缩
1）压缩
	tar -czvf   压缩文件名   目录名
	如：tar czvf dira.tar.gz  dira

注意：
tar  -czvf与tar  czvf是一样的效果，所以说，后面统一取消-。

2）查看
	tar tvf   压缩文件名
	如：tar tvf dira.tar.gz

3）解压
	tar xzvf 压缩文件名
	tar xzvf 压缩文件名  -C  指定目录
	如：tar xzvf dira.tar.gz   解压到当前目录
	如：tar xzvf dira.tar.gz   -C  /home/book   解压到/home/book
	
2.tar打包、bzip2压缩
1）压缩
	tar cjvf   压缩文件名   目录名
	如：tar cjvf dira.tar.bz2  dira
	
2）查看
	tar tvf   压缩文件名
	如：tar tvf dira.tar.bz2

3）解压
	tar xjvf 压缩文件名
	tar xjvf 压缩文件名  -C  指定目录
	如：tar xjvf dira.tar.bz2   解压到当前目录
	如：tar xjvf dira.tar.bz2 -C  /home/book  解压到/home/book
~~~

