Lenovo Newifi Y1S
============================
Y1S Techdata:  https://openwrt.org/toh/hwdata/lenovo/lenovo_newifi_y1s

download openwrt image 
====================
1.download openwrt-18.06.1-ramips-mt7620-y1s-squashfs-sysupgrade.bin
>https://downloads.openwrt.org/releases/18.06.1/targets/ramips/mt7620/

2.flash image

>open router's web manager,  flash openwrt images in router

download package
====================
1.Shadowsocks-libev for OpenWrt    

- shadowsocks-libev_3.2.1-1_mipsel_24kc.ipk
> https://github.com/shadowsocks/openwrt-shadowsocks/releases
> http://openwrt-dist.sourceforge.net/archives/shadowsocks-libev/3.2.1-1/current/mipsel_24kc/shadowsocks-libev_3.2.1-1_mipsel_24kc.ipk
>

- luci-app-shadowsocks_1.9.1-1_all.ipk
>https://github.com/shadowsocks/luci-app-shadowsocks    

2.kcptun client
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
1.upload ipk to router by ssh client(Xshell,MobaXterm,Winscp etc.)

2.opkg install  xxxx.ipk

    opkg install shadowsocks-libev_3.2.1-1_mipsel_24kc.ipk  
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

    src/gz openwrt_dist http://openwrt-dist.sourceforge.net/packages/base/mipsel_24kc/
    src/gz ss_dist http://openwrt-dist.sourceforge.net/archives/shadowsocks-libev/3.2.1-1/current/mipsel_24kc/
    src/gz dns_f_dist http://openwrt-dist.sourceforge.net/archives/dns-forwarder/1.2.1/current/mipsel_24kc/
    src/gz openwrt_dist_luci http://openwrt-dist.sourceforge.net/packages/luci

3.run command

    opkg install shadowsocks-libev
    opkg install luci-app-shadowsocks
    opkg install dns-forwarder
    opkg install luci-app-dns-forwarder
    ...


Shadowsocks & Kcptun Config
============================

1.Service－Kcptun Client 

服务器管理 - Add Kcptun Server

    server ip: kcp server ip    
    server port: kcp port
    
    local ip: 127.0.0.1
    local port: 12345
    
基本设置
    
    Server: kcp server
    Client: /var/kcptun_client         
    
2.Service－Shadowsocks config 

ShadowSocks - Servers Manage
    Add SS Server --> Kcp Client

    server: 127.0.0.1   
    port: 12345

ShadowSocks - General Settings - 
    
    Transparent Proxy
        choose the ss server config
    
ShadowSocks - Access Control

    Zone WAN
    Bypassed IP List : NULL As global proxy
    Forwarded IP:  8.8.8.8    


3.Save&Apply, check running status. If SS&KCP not running, check the logs    


Openwrt Dns Config 
============================
1.Service－DNS-Forwarder 

    Listen Port：5353
    Listen Address：127.0.0.1
    DNS Server：8.8.8.8

2.Network－DHCP/DNS

    DNS Forwarder： 127.0.0.1#5353

######the DNS Query packet trace:

client query dns->Router:53->Router:5353->8.8.8.8:53

###### open google.com in browser, and router is working..


#### Reference URL：

    http://openwrt-dist.sourceforge.net/
    http://openwrt-dist.sourceforge.net/packages/
    http://openwrt-dist.sourceforge.net/archives/  
    
    https://my.oschina.net/CasparLi/blog/487458   
    https://blog.phpgao.com/xiaomi_router_shadowsocks_libev_spec.html
