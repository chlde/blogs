# 问题描述
使用apt-get安装应用失败，异常为
`W: Failed to fetch http://xxxx
 Unable to connect to xxx:http: [IP: xxx.xxx.xxx 80]`
 
# 问题定位
由于树莓派的apt-get，默认source为http://raspbian.raspberrypi.org/raspbian/。这个路径会包含一些失效的链接。当使用apt-get install自动执行安装时，会使用失效的链接作为下载链接，导致安装失败。

# 问题解决
* 使用其他国内source替换默认配置
* source配置路径：/etc/apt/sources.list
* 注释掉原source，添加新配置，如下：
<code>
    \#deb http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
    
    deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi
    
    deb http://mirrors.neusoft.edu.cn/raspbian/raspbian stretch main contrib non-free rpi
    
    deb http://mirrors.zju.edu.cn/raspbian/raspbian/ stretch main contrib non-free rpi
    
    \# Uncomment line below then 'apt-get update' to enable 'apt-get source'
    
    \#deb-src http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
</code>

* 使用apt-get update更新配置
* https://www.raspbian.org/RaspbianMirrors 中有更多Raspbian的镜像