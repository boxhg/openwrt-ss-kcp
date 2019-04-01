#### 1.Running OpenWrt(KCP+SS) on VMware/VirtualBox to provides a Transparent Proxy Service for other VM

VM1:  OpenWrt 18.06.2-x86, KCP+SS
```
    LAN - Network Adapter 1:   Host-only 
    WAN - Network Adapter 2:   Bridge
```

VM2: Windows\Linux

```
    LAN - Network Adapter 1:   Host-only 
```

The network Traffic is:
```
VM2(Host-only) -> Openwrt VM1(Host-only, Bridge) -------> KCP + SS --->  WWW
```

#### 2.prepare OpenWrt VM

- download openwrt-x86 img
>https://downloads.openwrt.org/releases/18.06.2/targets/x86/generic/openwrt-18.06.2-x86-generic-combined-ext4.img.gz

- unzip openwrt-18.06.2-x86-generic-combined-ext4.img.gz

> extract openwrt-18.06.2-x86-generic-combined-ext4.img
 
- convert img to vmdk with qemu-img (linux) or  

```
qemu-img convert -f raw openwrt-18.06.2-x86-generic-combined-ext4.img -O vmdk openwrt-18.06.2-x86-generic-combined-ext4.vmdk
```

- Create New VM in VMware, use IDE for Virtual Disk type.  modify it's vmx file

```
ide0:0.fileName = "openwrt-18.06.2-x86-generic-combined-ext4.vmdk"
```

vmware下搭建openwrt
> https://blog.csdn.net/ballack_linux/article/details/81331527


#### 3.download ss,dns-forwarder,kcptun package 

3.1. download  4 package :

> http://openwrt-dist.sourceforge.net/packages/base/i386_pentium4/
```
http://openwrt-dist.sourceforge.net/packages/base/i386_pentium4/shadowsocks-libev_3.2.5-1_i386_pentium4.ipk
http://openwrt-dist.sourceforge.net/packages/luci/luci-app-shadowsocks_1.9.1-1_all.ipk

http://openwrt-dist.sourceforge.net/packages/base/i386_pentium4/dns-forwarder_1.2.1-1_i386_pentium4.ipk
http://openwrt-dist.sourceforge.net/packages/luci/luci-app-dns-forwarder_1.6.2-1_all.ipk

```

3.2.kcptun client

```
kcptun-client_20190325-1_i386_pentium4.ipk
    https://github.com/kuoruan/openwrt-kcptun/releases/

luci-app-kcptun_1.4.5-1_all.ipk
    https://github.com/kuoruan/luci-app-kcptun/releases
```


#### 4.install application by ssh shell

> upload the ipks to router by ssh client
> login router's ssh shell, run command 

```
opkg install shadowsocks-libev_3.2.5-1_i386_pentium4.ipk
opkg install luci-app-shadowsocks_1.9.1-1_all.ipk

opkg install dns-forwarder_1.2.1-1_i386_pentium4.ipk
opkg install luci-app-dns-forwarder_1.6.2-1_all.ipk

opkg install kcptun-client_20190325-1_i386_pentium4.ipk
opkg install luci-app-kcptun_1.4.5-1_all.ipk
...
```


#### KCP SS config, DNS-forwarder config

[config Openwrt with KCPTun& ShadowSocks](https://github.com/boxhg/openwrt-ss-kcp/blob/master/README.md)

Kcptun - Settings，Client File:  /usr/bin/kcptun-client
