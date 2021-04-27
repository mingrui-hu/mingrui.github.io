layout: post
title:  "小白从头创建基于华为云ECS的3个ubuntu服务器"
categories: linux

# 小白从头搭建基于华为云ECS的3个ubuntu服务器

> 作为一个从前只做过linux使用者的小白， 从没操心过环境搭建问题的dummy， 赶鸭子上架不得不自己配好3台服务器
>
> 由于是在公司环境配置的，涉及公司隐私安全要求，此处没有图片，只有步骤记录

## 1. 购买3台华为云ECS服务器：

> 背景：这三台服务器只有一台挂了EIP(弹性公网IP), 剩下两台只有小网IP(别问为什么，问就是组里穷疯了)
>
> 同时， 这三台服务器的网关、安全组规则已经被管理员限定死了。定死的DNS服务器不能解析任何地址（公司内网都不能，巨坑）&不允许自己魔改DNS服务器地址，所以有接下来的一些*扭曲*操作



- 在云控制台检查安全组规则，确认可以访问内网(可以连接公司ubuntu镜像源)

## 2. 配置apt源， 改为公司镜像

- DNS不能解析镜像网址， 所以首先在可以在windows10 `ping $mirror_addr` 获取到镜像源IP`mirror_IP`

- 直接修改host文件`/etc/hosts`, 增加`mirror_addr` -> `mirror_IP`的映射

- 修改apt源

  ```
  sudo cp -a /etc/apt/sources.list /etc/apt/sources.list.bak
  sudo sed -i 。。。。
  ```

  

- ping 一下试试 -> 成功就下一步

## 3. 挂载数据盘

   - 在云上配的数据盘初始是没有分区没有挂载的

   - 0. 检查

        ```lsblk -f
        lsblk -f
        df -h
     ```

        

   - 1. 分区

        1. parted vs fdisk

     2. 创建逻辑卷

     3. 挂载

        1. 注意这里一定要先挂到一个temp mnt point, 然后mv orig_target_dir ->创建placeholder -> mount -a

           否则如果目标挂载路径原来有不小心放进去的数据， 但是忘记了没删除， 直接挂载会隐藏掉原来的文件结构，但原来的挂载disk空间并没有被释放，可能会导致 磁盘空间不足`df -h`占用极高，但你就是找不到在哪里占用的:(

## 4. 创建用户

   ```shell
   sudo adduser $username
   sudo usermod -aG sudo $username # 加sudo权限
   ```

## 5. 配置Samba文件系统

## 6. 安装GUI

> BG: 我们的服务器也要给不熟悉命令行的人用，同时需要允许他们从windows remote desktop访问



 - 对每一台服务器：
   	- install desktop
   -  install & start xrdp service
- 在有公网ip的服务器装远程访问GUI工具: REMMINA

## 7. 安装matlab (linux GUI)
   - 3台服务器间传输文件 - rsync
   - 改 /etc/hosts 增加matlab license 服务器解析IP
   - 安装matlab
   - 配置/etc/profile.d/matlab_lic_var.sh
   - 给matlab命令创建一个GUI shortcut

END

> 两天时间搞完了，搞完了回头看操作步骤，其实很简单，但确实花了不少时间，尤其是配网和可视化部分