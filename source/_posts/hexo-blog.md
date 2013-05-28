#在树莓派上基于xbian、hexo搭建博客

看到同事基于gor搭建了一个博客，于是想弄一个博客。

**目标**

	1 搭建极简单博客。
	2 文件放在github上。

**材料**

	1 树莓派1个(包含电源线、8G-class10-sd卡一个、HDMI转接线，大约花费￥400)
	2 显示器一个
	3 u口键盘一个
	4 电脑一台

**步骤**
	
操作系统自带xwindow，格式化。选择xbian，自带无线网卡驱动，又有优化版的XBMC。
安装系统(mac下)

	1.下载最新xbian:[xbian官网](http://www.xbian.org)
	2.解压XBian1.0Alpha5.img，Mac下的ALZIP，Windows用7ZIP
	3.安装系统到sd
		- diskutil list
		- df  -h 
		- diskutil unmount /dev/disk1s1  (disk1s1为sd卡)
		- sudo dd bs=1m if=XBian1.0Alpha5.img of=/dev/rdisk1 (回复系统镜像到sd卡)
	把sd卡拔下插到树莓派上，接通电源，连上显示器、鼠标、网线，走起。
	xbian login： xbian
	password： raspberry

	Config>Settings>System>Resize SD（扩展系统到整个SD，必要的）
	Config>Settings>System>Overclocking（超频，我选到了Medium）
	Config>Settings>System>Hostname（设备名，我改成了iMedia）
	Config>Settings>System>Timezone（时区，我选择了Asia>shanghai，提示：到选择城市的时候，你输入键盘的s即可定位到上海）
	Config>Settings>User Accounts（我不知道root密码以前是什么，我都改成“raspberry”了）
	Config>Settings>Networking>WLAN（这里你按自己需要设置好了，设置完毕后会提示你的IP，无线驱动基本有，我选择的是DHCP、WPA）
	Config>Settings>SSH root login（开启）
> 安装软件环境

	1. sudo apt-get update
		这里提一个，我配置时出现了 E:Could not open lock file /var/lib/dpkg/lock - open (13:Permission denied) 这个错误。解决方案为：
		sudo rm -rf /var/lib/dpkg/lock

    	sudo rm -rf /var/cache/apt/archives/lock

    	sudo apt-get update

    	最后运行：sudo dpkg --configure -a  重新配置（系统会提醒） 。
	2. sudo apt-get install make g++ python vim lrzsz;
	3. mkdir ~/nodejs && cd $_
	4. wget -N http://nodejs.org/dist/node-latest.tar.gz
	5. tar xzvf node-latest.tar.gz && cd `ls -rd node-v*`
	6. ./configure
	7. make install
	8. 大约耗时2h，耐心等待。安装的时候出了个小插曲，装node报错，我可是等了2个小时啊。。。重新安装后通过。。。
> 申请花生壳免费域名

	[花生壳官网](http://www.oray.com),注册帐号-域名服务-免费域名，选一个喜欢的，申请成功后进去域名管理-免费域名-a记录，输入树莓派的地址（树莓派的地址查询可用Advanced IP Scanner）。

> 安装hexo

	xbian自带git，所以不用安装了^_^
	1. npm intall -g hexo
	2. hexo init project
	3. cd project
	4. hexo new "First Article"
	5. hexo generate
	6. sudo hexo server -p 80 (设置端口为80，默认是4000)
	7. 现在可以访问了。
	
> 放到github上
	1. cd project
	2. git init
	3. git add .
	4. git commit -m 'init'
	5. git remote add orgin xxx
	6. git push origin master
	

	