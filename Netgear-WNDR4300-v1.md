#### Netgear WNDR4300 v1

WNDR4300 v1 Techdata: https://openwrt.org/toh/netgear/wndr4300


#### 1.update fireware

http://downloads.openwrt.org/releases/18.06.2/targets/ar71xx/nand/openwrt-18.06.2-ar71xx-nand-wndr4300-ubi-factory.img

#### 2.download ss,dns-forwarder,kcptun package 

1. download  4 package :

> http://openwrt-dist.sourceforge.net/packages/base/mips_24kc/
```
http://openwrt-dist.sourceforge.net/packages/base/mips_24kc/shadowsocks-libev_3.2.5-1_mips_24kc.ipk
http://openwrt-dist.sourceforge.net/packages/luci/luci-app-shadowsocks_1.9.1-1_all.ipk

http://openwrt-dist.sourceforge.net/packages/base/mips_24kc/dns-forwarder_1.2.1-1_mips_24kc.ipk
http://openwrt-dist.sourceforge.net/packages/luci/luci-app-dns-forwarder_1.6.2-1_all.ipk
```

2.kcptun client

```
kcptun-client_20190109-2_mips_24kc.ipk
    https://github.com/kuoruan/openwrt-kcptun/releases/

luci-app-kcptun_1.4.5-1_all.ipk
    https://github.com/kuoruan/luci-app-kcptun/releases
```


#### 3.install application by ssh shell

> upload the ipks to router by ssh client
> login router's ssh shell, run command 

```
opkg install shadowsocks-libev_3.2.5-1_mips_24kc
opkg install luci-app-shadowsocks_1.9.1-1_all.ipk

opkg install dns-forwarder_1.2.1-1_mips_24kc.ipk
opkg install luci-app-dns-forwarder_1.6.2-1_all.ipk

opkg install kcptun-client_20190109-2_mips_24kc.ipk
opkg install luci-app-kcptun_1.4.5-1_all.ipk
...
```


#### KCP SS config, DNS-forwarder config

[config Openwrt with KCPTun& ShadowSocks](https://github.com/boxhg/openwrt-ss-kcp/blob/master/README.md)

Kcptun - Settings，Client File:  /usr/bin/kcptun-client
