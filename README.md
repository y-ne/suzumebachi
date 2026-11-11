```bash
# change timezone
uci get system.@system[0].timezone
uci get system.@system[0].zonename
date

# get system hostname
uci get system.@system[0].hostname

# set system hostname
uci set system.@system[0].hostname='suzumebachi'
uci commit system
/etc/init.d/system reload

# change root pass
passwd

# change lan ip addr
uci set network.lan.ipaddr='10.10.1.1'
uci set network.lan.netmask='255.255.255.0'
uci commit network
/etc/init.d/network restart

# dhcp
uci show dhcp.lan

# disable ipv6
uci set network.lan.ipv6='0'
uci delete network.lan.ip6assign 2>/dev/null
uci set dhcp.lan.dhcpv6='disabled'
uci set dhcp.lan.ra='disabled'
uci commit network
uci commit dhcp
/etc/init.d/network restart
/etc/init.d/odhcpd restart
```

### Wireless thingy

```bash
# 2.4 g (MT7603)
uci set wireless.radio0.disabled='0'
uci set wireless.radio0.country='ID'
uci set wireless.radio0.channel='6'
uci set wireless.radio0.htmode='HT40'
uci delete wireless.radio0.txpower

uci set wireless.default_radio0.ssid='2_suzumebachi'
uci set wireless.default_radio0.encryption='psk2'
uci set wireless.default_radio0.key='password'

# 5g (MT76x2E)
uci set wireless.radio1.disabled='0'
uci set wireless.radio1.country='ID'
uci set wireless.radio1.channel='149'
uci set wireless.radio1.htmode='VHT80'
uci delete wireless.radio1.txpower

uci set wireless.default_radio1.ssid='5_suzumebachi'
uci set wireless.default_radio1.encryption='psk2'
uci set wireless.default_radio1.key='password'

# hardware flow offloading
uci set firewall.@defaults[0].flow_offloading='1'
uci set firewall.@defaults[0].flow_offloading_hw='1'

uci commit
/etc/init.d/firewall restart
wifi reload
```
