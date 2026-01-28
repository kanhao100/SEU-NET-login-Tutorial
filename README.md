# SEU-NET-login-Tutorial
# 东南大学校园网一键认证教程

终端一行命令完成东南大学校园网认证，默认开启无感知认证，无需重复执行。  
One command to authenticate SEU campus network with persistent connection enabled by default.

## 使用场景
试想，你使用一个只有128MB RAM的嵌入式设备(软路由等)，进入了Linux终端，插上校园网网线或者连接上了`SEU-WLAN`却不知道如何认证。

## Usage 使用方法

```bash
curl "https://w.seu.edu.cn:801/eportal/?c=Portal&a=login&callback=dr1003&login_method=1&user_account=%2C0%2C你的一卡通号&user_password=你的密码&wlan_user_ip=你的IP地址"
```
如果不行，提示TLS之类的错误，可以添加-k 参数忽略HTTPS证书验证。
如果还是不行，很有可能是DNS无法解析`w.seu.edu.cn`，可以尝试重启或者试下面的：

```bash
curl -k "https://202.119.25.2:801/eportal/?c=Portal&a=login&callback=dr1003&login_method=1&user_account=%2C0%2C你的一卡通号&user_password=你的密码&wlan_user_ip=你的IP地址"
```

Replace the following parameters in the curl command with your information:
请将以下命令中的参数替换为你的信息：

- `一卡通号`: Your SEU card number 你的一卡通号
- `密码`: Your password 你的密码
- `地址`: Your IP address IP地址


## How to get your IP address 如何获取IP地址
确认连接上校园网，网卡设置为DHCP，将自动获取IP地址。(此IP地址只能用于校内局域网通讯) 如果出现认证失败的问题，请先检查是否已经分配到了内网IP地址。

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

## 进阶使用提示

总所周知，[东南大学校园网10元/月套餐](https://yingxin.seu.edu.cn/2024/0712/c27754a497559/page.htm)仅提供带宽30Mbps, 限制终端数4个；或者30元套餐限速100Mbps。每个终端数(不同的MAC地址)的限速都是单独的，如果有多线程大文件下载需求的话，可以考虑进行宽带叠加，比如WIFI+以太网网线。也可以考虑使用软路由，自行探索。 

## 鸣谢

https://github.com/ChenYuWuAi/seu-autologin

https://github.com/CleverPuppy/seu-wlan-logintool

脚本还是不如复制一行命令简单，而且我们不需要定时执行，只需要初始连接的时候执行一次即可。


