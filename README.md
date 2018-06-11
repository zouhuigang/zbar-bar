# zbar扩展包下载，因为官网下载太慢，所以在这放个镜像

### 安装方法:

初始化环境:

centos:

	yum install -y gcc  gcc-c++
	yum install -y ImageMagick-devel
	yum install libv4l-devel
	yum install python-devel
	ln -s  /usr/include/libv4l1-videodev.h  /usr/include/linux/videodev.h 
	
ubuntu:

	sudo apt-get install imagemagick
	sudo apt-get install python-gtk2-dev 
	sudo apt-get install libv4l-dev
	sudo ln -s /usr/include/libv4l1-videodev.h /usr/include/linux/videodev.h 

下载并安装:

	wget http://downloads.sourceforge.net/project/zbar/zbar/0.10/zbar-0.10.tar.gz
	tar -zvxf zbar-0.10.tar.gz \
	cd  zbar-0.10 \
	./configure  --without-gtk --without-qt --without-imagemagick --without-python
	make \
	make install

	添加环境变量vi /etc/profile,找到动态链接库的路径,在最后添加2行:

	LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
	export LD_LIBRARY_PATH

	使环境变量生效
	source /etc/profile
	
###  问题汇总

Q:

	fatal error: linux/videodev.h: No such file or directory
	搜索问题，发现应该安装v4l(Video for Linux)的开发库。
Debian系：

	$ sudo apt-get install libv4l-dev
RH系：

	$ sudo yum install libv4l-devel
Arch：

	$ sudo pacman -S v4l-utils
	
	
建立软链接

	$ sudo ln -s /usr/include/libv4l1-videodev.h /usr/include/linux/videodev.h
Edit: 我发现自己的/usr/include/linux/目录下有videodev2.h文件，于是先尝试给此文件建立软链接：

	$ sudo ln -s /usr/include/linux/videodev2.h /usr/include/linux/videodev.h
重新make，成功。


Q:

	ubuntu  make 
	
	/usr/include/x86_64-linux-gnu/bits/stdio2.h:140:1: error: expected identifier or ‘(’ before ‘{’ token
	 {
	 ^
	 
A:

	export CFLAGS=""
	./configure  --without-gtk --without-qt --without-imagemagick --without-python
	sudo make
	sudo make install


### 参考文档

[https://segmentfault.com/a/1190000004335339](https://segmentfault.com/a/1190000004335339)

[https://bbs.archlinux.org/viewtopic.php?id=151274?db=5](https://bbs.archlinux.org/viewtopic.php?id=151274?db=5)

