```
port: 7890
socks-port: 7891
unified-delay: true                # 以“完成握手后”的 RTT 统计延迟，更贴近真实体验
tcp-concurrent: true               # 并发拨号择优保留，跨境网络通常更稳更快
find-process-mode: strict          # 更精准地识别连接来源进程（Windows 需管理员权限）

dns:
  enable: true
  ipv6: false
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  use-system-hosts: true
  prefer-h3: false
  respect-rules: true
  fake-ip-filter:
    - '*.lan'
    - localhost.ptlogin2.qq.com
    - '+.srv.nintendo.net'
    - '+.stun.playstation.net'
    - '+.msftconnecttest.com'
    - '+.msftncsi.com'
    - '+.xboxlive.com'
    - 'xbox.*.microsoft.com'
    - '*.battlenet.com.cn'
    - '*.battlenet.com'
    - '*.blzstatic.cn'
    - '*.battle.net'
#nameserver（国外）proxy-nameserver（国内）direct-nameserver（国内）
#用来解析 nameserver 和 fallback 里面的域名的，必须为 IP, 可为加密 DNS
  default-nameserver:
    - 223.5.5.5
    - 223.6.6.6
    - 119.29.29.29
  direct-nameserver:
    - system
    - https://doh.pub/dns-query
    - https://dns.alidns.com/dns-query	
  nameserver:
    - https://cloudflare-dns.com/dns-query#节点选择
    - https://8.8.8.8/dns-query#节点选择
    - https://1.1.1.1/dns-query#节点选择
  proxy-server-nameserver:
    - https://doh.pub/dns-query
    - https://dns.alidns.com/dns-query
    - https://1.1.1.1/dns-query#节点选择
    - https://8.8.8.8/dns-query#节点选择
profile:
  store-selected: true
  store-fake-ip: true
sniffer:
  enable: true
  sniff:
    TLS:
      ports: [443, 8443]
    HTTP:
      ports: [80, 8080-8880]
      override-destination: true	  	  
geodata-mode: true
geo-auto-update: true
geodata-loader: standard
geo-update-interval: 24
geox-url:
  geoip: https://github.com/MetaCubeX/meta-rules-dat/releases/download/latest/geoip.dat
  geosite: https://github.com/MetaCubeX/meta-rules-dat/releases/download/latest/geosite.dat
  mmdb: https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/country.mmdb
  asn: https://github.com/MetaCubeX/meta-rules-dat/releases/download/latest/GeoLite2-ASN.mmdb	  
tun:
  enable: true
  stack: mixed
  auto-route: true
  auto-redirect: true
  auto-detect-interface: true
  dns-hijack:
    - any:53
    - tcp://any:53
  mtu: 1500
  strict-route: true
  gso: true
  gso-max-size: 65536
  udp-timeout: 300
  endpoint-independent-nat: false
  include-interface:
    - eth0
  exclude-interface:
    - eth1
  include-uid:
    - 0
  include-uid-range:
    - 1000:9999
  exclude-uid:
    - 1000
  exclude-uid-range:
    - 1000:9999
  include-android-user:
    - 0
    - 10
  include-package:
    - com.android.chrome
  exclude-package:
    - com.android.captiveportallogin
```
