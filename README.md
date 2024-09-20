# bilibili-cn-bj-fx-01-ipv6-fix

## Archived: This issue has been fixed as of 20240920.

Fix IPV6 records of `cn-bj-fx-01-[08..12].bilivideo.com` by redirect them to `cn-bj-fx-01-01.bilivideo.com`.

Append the following config to `/etc/config/firewall` on your openwrt router. `fw4` required.
```
config ipset
        option family 'ipv6'
        list match 'dest_ip'
        option name 'cn-bj-fx-01-ipv6-fix'
        list entry '2404:4d00:1:1::2:8'
        list entry '2404:4d00:1:1::2:9'
        list entry '2404:4d00:1:1::2:10'
        list entry '2404:4d00:1:1::2:11'
        list entry '2404:4d00:1:1::2:12'
        list entry '2404:4d00:1:1::2:13'

config redirect
        option dest 'wan'
        option target 'DNAT'
        option name 'bilibili-cdn-ipv6'
        option src 'lan'
        option ipset 'cn-bj-fx-01-ipv6-fix'
        option reflection '0'
        option family 'ipv6'
        option dest_ip '2404:4d00:1:1::2:2'
        list proto 'all'
```
