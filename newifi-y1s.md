download openwrt image 
====================
1.download openwrt-18.06.1-ramips-mt7620-y1s-squashfs-sysupgrade.bin
    https://downloads.openwrt.org/releases/18.06.1/targets/ramips/mt7620/

2.flash image
    
    
download package
====================
1.Shadowsocks-libev for OpenWrt
    
    shadowsocks-libev_3.2.1-1_mips_mips32.ipk    
        https://github.com/shadowsocks/openwrt-shadowsocks/releases
        http://openwrt-dist.sourceforge.net/archives/shadowsocks-libev/3.2.1-1/current/mips_mips32/shadowsocks-libev_3.2.1-1_mips_mips32.ipk

  
    luci-app-shadowsocks_1.9.1-1_all.ipk
        https://github.com/shadowsocks/luci-app-shadowsocks    
    
2.kcptun client: 
    kcptun-linux-mips-20181114.tar.gz   
        https://github.com/xtaci/kcptun/releases
    
    luci-app-kcptun_1.4.5-1_all.ipk
        https://github.com/kuoruan/luci-app-kcptun/releases
   

3. DNS-Forwarder
    dns-forwarder_1.2.1-1_mipsel_24kc.ipk
        https://github.com/aa65535/openwrt-dns-forwarder/releases
        http://openwrt-dist.sourceforge.net/archives/dns-forwarder/1.2.1/current/mipsel_24kc/dns-forwarder_1.2.1-1_mipsel_24kc.ipk
    
    luci-app-dns-forwarder
        http://openwrt-dist.sourceforge.net/packages/luci/luci-app-dns-forwarder_1.6.2-1_all.ipk

install manual
===============
1.upload ipk to router by ssh

2.opkg install  xxxx.ipk    
    opkg install shadowsocks-libev_3.2.1-1_mips_mips32.ipk  
    opkg install luci-app-shadowsocks_1.9.1-1_all.ipk 
    
    opkg install luci-i18n-kcptun_1.4.5-1_all.ipk
    

install by online
=================
1.check router's cpu
    opkg print-architecture | awk '{print $2}'

2.add package source
    src/gz openwrt_dist http://openwrt-dist.sourceforge.net/packages/base/{architecture}
    src/gz openwrt_dist_luci http://openwrt-dist.sourceforge.net/packages/luci

3.run command
    opkg install shadowsocks-libev
    opkg install luci-app-shadowsocks
    

dns-config
============================
1.服务－shadowsocks-libev config 
    基本设置－端口转发
        本地端口：5300
        目标地址：8.8.8.8:53
    访问控制－外网区域
        被忽略IP列表： 留空－作为全局代理
        强制走代理IP：  8.8.8.8
        
2.服务－DNS转发
    监听端口：5353
    监听地址：127.0.0.1
    上游 DNS：8.8.8.8
    
3.网络－DHCP/DNS
    DNS 转发： 127.0.0.1#5353

4.dns send path
    设备查询dns->路由器:53->路由器:5353->8.8.8.8:53
   
    
参考：    
=====================
http://openwrt-dist.sourceforge.net/
http://openwrt-dist.sourceforge.net/packages/
http://openwrt-dist.sourceforge.net/archives/   
https://my.oschina.net/CasparLi/blog/487458?fromerr=YZt9tpKq    
https://blog.phpgao.com/xiaomi_router_shadowsocks_libev_spec.html
