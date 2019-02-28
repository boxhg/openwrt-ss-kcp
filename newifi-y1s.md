download openwrt image 
====================
1.download openwrt-18.06.1-ramips-mt7620-y1s-squashfs-sysupgrade.bin
>https://downloads.openwrt.org/releases/18.06.1/targets/ramips/mt7620/

2.flash image

>open router's web manager,  update the  openwrt images

download package
====================
1.Shadowsocks-libev for OpenWrt    

- shadowsocks-libev_3.2.1-1_mips_mips32.ipk 
> https://github.com/shadowsocks/openwrt-shadowsocks/releases
> http://openwrt-dist.sourceforge.net/archives/shadowsocks-libev/3.2.1-1/current/mips_mips32/shadowsocks-libev_3.2.1-1_mips_mips32.ipk
>

- luci-app-shadowsocks_1.9.1-1_all.ipk
>https://github.com/shadowsocks/luci-app-shadowsocks    

2.kcptun client: 
- kcptun-linux-mips-20181114.tar.gz   
> https://github.com/xtaci/kcptun/releases

- luci-app-kcptun_1.4.5-1_all.ipk
>https://github.com/kuoruan/luci-app-kcptun/releases

3.DNS-Forwarder
- dns-forwarder_1.2.1-1_mipsel_24kc.ipk
 > https://github.com/aa65535/openwrt-dns-forwarder/releases
 > http://openwrt-dist.sourceforge.net/archives/dns-forwarder/1.2.1/current/mipsel_24kc/dns-forwarder_1.2.1-1_mipsel_24kc.ipk
- luci-app-dns-forwarder
>http://openwrt-dist.sourceforge.net/packages/luci/luci-app-dns-forwarder_1.6.2-1_all.ipk

install from local
===================
1.upload ipk to router by ssh(Xshell,MobaXterm,Winscp etc. )

2.opkg install  xxxx.ipk

    opkg install shadowsocks-libev_3.2.1-1_mips_mips32.ipk  
    opkg install luci-app-shadowsocks_1.9.1-1_all.ipk 
    opkg install luci-app-kcptun_1.4.5-1_all.ipk
    opkg install dns-forwarder_1.2.1-1_mipsel_24kc.ipk
    opkg install luci-app-dns-forwarder_1.6.2-1_all.ipk

3.client_linux_mipsle

    move client_linux_mipsle to /var/kcptun_client

install from ipk sources
============================
1.check router's cpu

    opkg print-architecture | awk '{print $2}'

2.add package source

    src/gz openwrt_dist http://openwrt-dist.sourceforge.net/packages/base/{architecture}
    src/gz openwrt_dist_luci http://openwrt-dist.sourceforge.net/packages/luci

3.run command

    opkg install shadowsocks-libev
    opkg install luci-app-shadowsocks


Openwrt Config 
============================
1.Service－shadowsocks-libev config 

    基本设置－端口转发
        本地端口：5353
        目标地址：8.8.8.8:53
    访问控制－外网区域
        被忽略IP列表： 留空－作为全局代理
        强制走代理IP： 8.8.8.8

2.Service－DNS-Forwarder DNS转发

    监听端口：5353
    监听地址：127.0.0.1
    上游 DNS：8.8.8.8

3.Network－DHCP/DNS

    DNS 转发： 127.0.0.1#5353

> DNS转发效果(全局转发，防止DNS污染)

    设备查询dns->路由器:53->路由器:5353->8.8.8.8:53


Shadowsocks & Kcptun Config
============================

1.Add Kcptun Server, Save&Apply, check running status

    server ip: kcp server ip    
    server port: kcp port
    
    local ip: 127.0.0.1
    local port: 12345
    
2.Add SS Server --> Kcp Client, Save&Apply, check running status

    server: 127.0.0.1   
    port: 12345
    
3.if SS&KCP not running, check the logs    

#### Reference URL：

    http://openwrt-dist.sourceforge.net/
    http://openwrt-dist.sourceforge.net/packages/
    http://openwrt-dist.sourceforge.net/archives/   
    https://my.oschina.net/CasparLi/blog/487458?fromerr=YZt9tpKq    
    https://blog.phpgao.com/xiaomi_router_shadowsocks_libev_spec.html
