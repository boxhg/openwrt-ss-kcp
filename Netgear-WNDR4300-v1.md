#### Netgear WNDR4300 v1

WNDR4300 v1 Techdata: https://openwrt.org/toh/netgear/wndr4300


#### 1.download fireware

http://downloads.openwrt.org/releases/18.06.2/targets/ar71xx/nand/openwrt-18.06.2-ar71xx-nand-wndr4300-ubi-factory.img

#### 2.setup package source

1. open http://192.168.1.1 in browser, login in router web manager , add package source:

open Menu : System -> Software

>OPKG-Configuration

```
> src/gz openwrt_dist http://openwrt-dist.sourceforge.net/packages/base/mips_24kc/
> src/gz ss_dist http://openwrt-dist.sourceforge.net/archives/shadowsocks-libev/3.2.1-1/current/mips_24kc/
> src/gz dns_f_dist http://openwrt-dist.sourceforge.net/archives/dns-forwarder/1.2.1/current/mips_24kc/
> src/gz openwrt_dist_luci http://openwrt-dist.sourceforge.net/packages/luci
```

2. Action - update list

#### 3.install application

1. ss, dns-forwarder ipk
```
shadowsocks-libev
luci-app-shadowsocks
dns-forwarder
luci-app-dns-forwarder
```

2.kcptun client
```
kcptun-linux-mips-20181114.tar.gz
    https://github.com/xtaci/kcptun/releases

luci-app-kcptun_1.4.5-1_all.ipk
    https://github.com/kuoruan/luci-app-kcptun/releases
```

#### 4.install application by ssh shell

login router's ssh shell, run command 

```
opkg install shadowsocks-libev
opkg install luci-app-shadowsocks
opkg install dns-forwarder
opkg install luci-app-dns-forwarder
...
```


#### KCP SS config, DNS-forwarder config

[config Openwrt with KCPTun& ShadowSocks](https://github.com/boxhg/openwrt-ss-kcp/blob/master/README.md)
