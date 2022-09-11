# 实验1 基于 VirtualBox 的网络攻防基础环境搭建
## 实验目的
  - 掌握 VirtualBox 虚拟机的安装与使用；
  - 掌握 VirtualBox 的虚拟网络类型和按需配置；
 -  掌握 VirtualBox 的虚拟硬盘多重加载；
## 实验环境

- VirtualBox 虚拟机
- 攻击者主机（Attacker）：Kali
- 网关（Gateway, GW）：Debian Buster
- 靶机（Victim）：Debian (victim1); xp(victim1,victim2); Kali(victim2)

## 实验要求
- 虚拟硬盘配置成多重加载，效果如下图所示；

![2](img/vb-multi-attach.png)

- 搭建满足如下拓扑图所示的虚拟机网络拓扑；

![2](img/vb-exp-layout.png)

- 根据实验宿主机的性能条件，可以适度精简靶机数量

- 完成以下网络连通性测试；
- [x] 靶机可以直接访问攻击者主机
- [x] 攻击者主机无法直接访问靶机
- [x] 网关可以直接访问攻击者主机和靶机
- [x] 靶机的所有对外上下行流量必须经过网关
- [x] 所有节点均可以访问互联网

## 实验过程
### 1.环境配置
- 多重加载
  在虚拟介质管理中，先释放已导入的虚拟磁盘文件，然后设置为多重加载，再添加到已创建的虚拟机中。
  
  ![2](img/duochongjiazai.png)
  
- 网卡配置
  - 对于作为网关的Debian虚拟机，设置四片网卡如下：

    ![2](img/debian_net.png)
    
    在设置网卡一为NAT网络前，需要到全局设定-网络里添加新的NAT网络，结果如下：
    
    ![2](img/debian_nat.png)

    同时，为确保网卡二的正常运行，在主机网络管理器中确认是否启用了Host-Only网络：
    
    ![2](img/hostonly_wk.png)
    
   - 对于作为靶机的四台虚拟机，只需设置一片网卡，接入不同的内部网络即可。以xp-victim1举例，接入的网络是编号为intnet0的内部网络。
 
    ![2](img/xp_wk.png)
    
   -对于作为攻击者的kali虚拟机，只需一片接入外部网络的网卡。
   





## 问题及解决方案
1. 无法登录kali
  根据视频用用户名```cuc```和密码```cuc```登录，显示失败。
  
  ![2](img/error_kalilogin.png)

  解决方案：用户名```kali```,密码```kali```

## 参考资料
- [给非root用户赋予sudo权力](https://www.myfreax.com/how-to-add-and-delete-users-on-debian-9/#:~:text=%E5%9C%A8Debian%E4%B8%AD%EF%BC%8C%E6%9C%89%E4%B8%A4%E4%B8%AA%E5%8F%AF%E7%94%A8%E4%BA%8E%E5%88%9B%E5%BB%BA%E6%96%B0%E7%94%A8%E6%88%B7%E5%B8%90%E6%88%B7%E7%9A%84%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B7%A5%E5%85%B7%EF%BC%9A%20useradd%20%E5%92%8C%20adduser%20%E3%80%82%20useradd%20%E6%98%AF%E7%94%A8%E4%BA%8E%E6%B7%BB%E5%8A%A0%E7%94%A8%E6%88%B7%E7%9A%84%E4%BD%8E%E7%BA%A7%E5%AE%9E%E7%94%A8%E7%A8%8B%E5%BA%8F%EF%BC%8C%E8%80%8C%20adduser,%E6%98%AF%E7%94%A8Perl%E7%BC%96%E5%86%99%E7%9A%84%20useradd%20%E7%9A%84%E5%8F%8B%E5%A5%BD%E4%BA%A4%E4%BA%92%E5%BC%8F%E5%89%8D%E7%AB%AF%E3%80%82%20%E8%A6%81%E4%BD%BF%E7%94%A8%20adduser%20%E5%91%BD%E4%BB%A4%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%90%8D%E4%B8%BA%20username%20%E7%9A%84%E6%96%B0%E7%94%A8%E6%88%B7%E5%B8%90%E6%88%B7%EF%BC%8C%E8%AF%B7%E8%BF%90%E8%A1%8C%EF%BC%9A)
- [Kali Linux初始账号和密码不知道怎么办？](https://www.bilibili.com/read/cv10217865/)
- [linux命令scp(复制文件和目录)详解及cp和scp命令的使用方法](https://blog.csdn.net/qq_34374664/article/details/81289540)
