# 实验五 基于 Scapy 编写端口扫描器
## 实验目的
- 掌握网络扫描之端口状态探测的基本原理
## 实验环境
- python + scapy
## 实验要求
- [x] 禁止探测互联网上的 IP ，严格遵守网络安全相关法律法规
- 完成以下扫描技术的编程实现:
    - [x] TCP connect scan / TCP stealth scan
    - [x] TCP Xmas scan / TCP fin scan / TCP null scan
    - [x] UDP scan
- [x] 上述每种扫描技术的实现测试均需要测试端口状态为：开放、关闭 和 过滤 状态时的程序执行结果
- [x] 提供每一次扫描测试的抓包结果并分析与课本中的扫描方法原理是否相符？如果不同，试分析原因；
- [x] 在实验报告中详细说明实验网络环境拓扑、被测试 IP 的端口状态是如何模拟的
- [x] （可选）复刻 nmap 的上述扫描技术实现的命令行参数开关

## 实验准备
#### 1.网络拓扑
![2](img5/cisco.png)
#### 2.环境布置
- 需要安装ufw，来控制端口状态。
    ```bash
    #安装ufw
    sudo apt-get upgrade
    sudo apt-get install ufw

    #端口状态控制
    #允许访问
    sudo ufw enable && ufw allow portno/tcp(udp)
    #过滤状态
    sudo ufw enable && ufw deny portno/tcp(udp)
    #关闭状态
    sudo ufw disable
    ```
#### 3.先述知识
- 端口状态
    开放✅
    关闭⛔
    被过滤⚠

## 实验过程
#### 1. TCP connect scan
##### I.编程实现
- ##### 代码
    ```bash
    #! /usr/bin/python

    from scapy.all import *

    dst_ip = "172.16.111.124"
    src_port = RandShort()
    dst_port=8083

    tcpconnectscan_pkts = sr1(IP(dst=dst_ip)/TCP(sport=src_port,dport=dst_port,flags="S"),timeout=10)
    if tcpconnectscan_pkts is None:
        print("Filtered")
    elif(tcpconnectscan_pkts.haslayer(TCP)):
        if(tcpconnectscan_pkts.getlayer(TCP).flags == 0x12):
            print("Open")
        elif (tcpconnectscan_pkts.getlayer(TCP).flags == 0x14):
            print("Closed")
    ```
- ##### 结果
    ###### closed
    kali-attacker2
    

## 实验问题与解决方案
```bash
#安装dnsmasq服务以开启udp端口
    sudo apt install dnsmasq
    sudo systemctl start dnsmasq
```
## 参考资料
- [第五章 网络扫描](https://c4pr1c3.github.io/cuc-ns/chap0x05/main.html)
- [2020-ns-public-Crrrln](https://github.com/CUCCS/2020-ns-public-Crrrln/blob/chap0x05/chap0x05/exp5.md)
- [2021-ns-public-Tbc-tang](https://github.com/CUCCS/2021-ns-public-Tbc-tang/blob/chap0x05/0x05.md)
- [Kali Linux渗透测试之端口扫描（一）——UDP、TCP、隐蔽端口扫描、全连接端口扫描](https://blog.csdn.net/qq_38684504/article/details/89298654)
- [Kali-linux查看打开的端口](https://www.cnblogs.com/student-programmer/p/6727732.html)
