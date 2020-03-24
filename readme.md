### Linux SDK加载107问题解决方案
1. 将SDK动态库路径加入到LD_LIBRARY_PATH环境变量
```
# 修改系统预加载项,增加一行export
vim ~/.bashrc
export  LD_LIBRARY_PATH=$LD_LIBRARY_PATH:{pyhikvsion/hkws/lib/在Linux中的绝对路径}:{pyhikvsion/hkws/lib/HCNetSDKCom/在Linux中的绝对路径}
source ~/.bashrc

vim /etc/profile
export  LD_LIBRARY_PATH=$LD_LIBRARY_PATH:{pyhikvsion/hkws/lib/在Linux中的绝对路径}:{pyhikvsion/hkws/lib/HCNetSDKCom/在Linux中的绝对路径}
source /etc/profile
```
2. 在/etc/ld.so/conf下增加sdk路径
```
//查看配置信息
cat /etc/ld.so.conf
//如果有以下Include，建议在ld.so.conf.d下新建文件设置，这样隔离比较干净
include ld.so.conf.d/*.conf
//切换到指定目录
cd /etc/ld.so.conf.d

vim hikvsdk.conf
#加入以下2个路径
{pyhikvsion/hkws/lib/HCNetSDKCom/在Linux中的绝对路径}
{pyhikvsion/hkws/lib/在Linux中的绝对路径}

//保存完后执行以下命令重新加载系统.so配置
ldconfig

```