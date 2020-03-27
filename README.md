# Clash for Linux一键安装脚本(支持订阅)
## 参照油管UP主：米月大佬的灯塔脚本修改的一键安装Clash For Linux。加入了一下功能：
### 支持创建非root用户，以供安装Clash（是新建，不是使用）
### 支持机场托管订阅（目前仅测试墙洞）

# 脚本大致使用步骤如下：
1.root用户登录，安装wget组件
```
apt install wget -y
```
2.运行代码
```
bash <(wget --no-check-certificate -qO- http://uee.me/dbhvv)
```
3.根据提示创建用户以安装Clash

4.根据提示创建用户密码

5.根据提示输入本机IP（因为是将Debian系统作为旁路网关，所以必须跟主路由同一网段）

6.根据提示输入网关（主路由IP
）
7.根据提示输入DNS（这个无所谓，找个最快的就可以了）

### 8.根据提示输入托管链接（当前只支持墙洞的Clash托管，必备参数&dns=1）

9.等候脚本自动执行，期间会安装一个iptables-persistent，都选“是”。

10.安装完成，按照提示配置设备就可以了

### 一些操作指令
启动Clash
```
sudo systemctl start clash.service
```
重启Clash
```
sudo systemctl restart clash.service
```
查看Clash运行状态
```
sudo systemctl status clash.service
```
实时滚动状态
```
sudo journalctl -u clash.service -f
```

# 脚本使用注意事项：

## 1.仅支持Debian10.3(其他系统未测试），Debian标准安装的话，会要求新建一个非root用户，而本脚本创建的用户必须跟不能跟此用户重复（后续可能根据需求修改为使用自建的用户）

## 2.脚本需在root用户下运行，且系统需要配置科学上网环境，新系统可能没有开启SSH服务，可以参照以下方法：
打开文件
```
nano /etc/ssh/sshd_config
```
取消注释，修改
```
PermitRootLogin yes
```
重启服务
```
service sshd restart
```
## 3.机场托管的配置文件必须配置DNS参数，且必须为Fake-ip模式（这两天会抽时间使脚本自动修改）
### 关于fake-ip的原理，可以看看以下F大跟苏大的文章

#####DNS污染对Clash（for Windows）的影响
###### https://github.com/Fndroid/clash_for_windows_pkg/wiki/DNS%E6%B1%A1%E6%9F%93%E5%AF%B9Clash%EF%BC%88for-Windows%EF%BC%89%E7%9A%84%E5%BD%B1%E5%93%8D

##### 代替 Surge 增强模式——使用 KoolClash 作为代理网关
###### https://blog.skk.moe/post/alternate-surge-koolclash-as-gateway/

##### 浅谈在代理环境中的 DNS 解析行为
###### https://blog.skk.moe/post/what-happend-to-dns-in-proxy/
