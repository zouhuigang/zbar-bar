# zbar扩展包下载，因为官网下载太慢，所以在这放个镜像

### 安装方法:

初始化环境:

	yum install -y gcc  gcc-c++
	yum install -y ImageMagick-devel
	yum install libv4l-devel
	yum install python-devel
	ln -s  /usr/include/libv4l1-videodev.h  /usr/include/linux/videodev.h 

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