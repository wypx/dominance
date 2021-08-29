### 设置交叉工具链
```
在/.bashrc文件中加入gcc交叉工具链目录

sudo gedit ~/.bashrc

export PATH=$PATH:/root/Desktop/gcc-linaro-6.3.1-2017.02-x86_64_arm-linux-gnueabihf/bin

export PATH=$PATH:/home/gcc-linaro-6.3.1-2017.02-i686_arm-linux-gnueabihf/bin

请注意PATH代表环境变量，:冒号代表追加

libzlib.a
sudo cp -rf libz.a /opt/hisi-linux-nptl/arm-hisiv100-linux/target/usr/lib
sudo cp -rf zlib.h zconfig.h /opt/hisi-linux-nptl/arm-hisiv100-linux/target/usr/include/


ligogg.a
sudo cp -rf libogg.a /opt/hisi-linux-nptl/arm-hisiv100-linux/target/usr/lib
sudo cp -rf /ogg /opt/hisi-linux-nptl/arm-hisiv100-linux/target/usr/include/

```