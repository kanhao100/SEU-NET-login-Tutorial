# SEU-NET-login-Tutorial
# 东南大学校园网一键认证教程

终端一行命令完成东南大学校园网认证，默认开启无感知认证，无需重复执行。  
One command to authenticate SEU campus network with persistent connection enabled by default.

## Usage 使用方法

```bash
curl "https://w.seu.edu.cn:801/eportal/?c=Portal&a=login&callback=dr1003&login_method=1&user_account=%2C0%2C你的一卡通号&user_password=你的密码&wlan_user_ip=你的IP地址"
```
如果不行，提示TLS之类的错误，可以添加-k 参数忽略HTTPS证书验证。
如果还是不行，很有可能是DNS无法解析`w.seu.edu.cn`，可以尝试下面的：

```bash
curl -k "https://202.119.25.2:801/eportal/?c=Portal&a=login&callback=dr1003&login_method=1&user_account=%2C0%2C你的一卡通号&user_password=你的密码&wlan_user_ip=你的IP地址"
```

Replace the following parameters in the curl command with your information:
请将以下命令中的参数替换为你的信息：

- `一卡通号`: Your SEU card number 你的一卡通号
- `密码`: Your password 你的密码
- `地址`: Your IP address IP地址


## How to get your IP address 如何获取IP地址
确认连接上校园网，网卡设置为DHCP，自动获取IP地址。(此IP地址只能用于校内局域网通讯)

### Linux
Open Terminal and type:
打开终端并输入：
```bash
ifconfig
```
or 或者：
```bash
ip addr
```
or 或者:
```bash
curl baidu.com
```
then you will see the IP address in the response.
```bash
<NextuRL>http://202.119.25.2/a79.htm?userIP=你的IP地址&wlanacname=sPL NetEngine8000F8</NextURL>
```

## 认证成功提示
```
dr1003({"result":"1","msg":"\u8ba4\u8bc1\u6210\u529f"})
```
`\u8ba4\u8bc1\u6210\u529f` 是 **Unicode** 转义，解码后就是 "认证成功"。


## 鸣谢

https://github.com/ChenYuWuAi/seu-autologin

https://github.com/CleverPuppy/seu-wlan-logintool

脚本还是不如复制一行命令简单，而且我们不需要定时执行，只需要初始连接的时候执行一次即可。


