![Logo](logo.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

**Important:** If you are planning to use `git` to get the content of this repository do it like `git clone --depth 1 https://github.com/stamparm/ipsum.git`

Wall of shame (2018-06-29)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
185.56.80.242|public.freeflux.org|11
104.244.73.53|frank8.doneaminovich.com|10
128.199.191.144|sweetycare.com-1480955588261-8gb-sgp1-01|9
5.188.10.76|-|9
80.82.77.33|sky.census.shodan.io|8
123.59.45.153|-|8
154.16.149.74|pluto.tor-exits.libre.zone|8
217.61.96.104|host104-96-61-217.static.arubacloud.com|8
171.25.193.25|tor-exit5-readme.dfri.se|8
115.182.62.212|-|8
197.231.221.211|exit1.ipredator.se|8
61.234.109.82|-|8
46.17.42.33|server5.to-go.net|8
209.15.226.179|www.eliteimage.ca|8
193.201.224.109|-|8
171.25.193.77|tor-exit1-readme.dfri.se|8
51.254.145.98|-|8
193.201.224.208|-|8
193.15.16.4|-|8
80.82.77.139|dojo.census.shodan.io|8
222.187.238.208|-|8
218.17.246.223|-|8
185.8.49.52|host52-49-8-185.static.arubacloud.fr|8
46.17.47.236|host.webgroup.az|8
37.49.231.14|-|8
61.164.252.244|244.252.164.61.broad.ls.zj.dynamic.163data.com.cn|8
61.8.73.166|-|8
167.114.13.149|167.114.13.149.infinity-hosting.com|8
