- [规则参考](https://github.com/lainbo/gists-hub/blob/73b207e3d7cd4c1918efe4f03e0f3739cb4a5cfa/src/Clash/RemoteConfig/Lainbo.ini)
- [blackmatrix7大佬规则](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash)
- [subconverter](https://github.com/tindy2013/subconverter/blob/master/README-cn.md#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
- [分流配置写法](https://github.com/chinnsenn/ClashCustomRule?tab=readme-ov-file)
- [Clash 中 GeoSite 分流的正确使用方式](https://www.aloxaf.com/2025/04/how_to_use_geosite/)
- [关于 Clash 等现代代理软件的规则和 dns 配置问题](https://linux.do/t/topic/155121)
- [虚空终端 Docs](https://wiki.metacubex.one/config/rules/)
- [海豚测速 - 网络代理工具箱](https://www.haitunt.org/app.html)
- [CDN查询](https://www.cdnplanet.com/tools/cdnfinder)

# 制作分流策略组
文件命名随意，但是一定是英文+ .ini 结尾

ini 配置文件中
- ruleset 指的是配配置中包含的分流规则
- custom_proxy_group 指的是最终在Clash中呈现的分流策略组及其排序
- Select 后面有多少 []XXXX 代表该策略组有多少种规则可以选，一般用 ``` ` ``` 分隔，最后一项后不需要分隔

```
custom_proxy_group=无需代理`select`[]DIRECT`[]节点选择
```

 ### ruleset 排序原则：
- 重要直连分流规则 > 去广告规则 > 小分流 > 国内外大分流 > 补充规则
- 策略组的排序非常重要，因为分流策略组的匹配是按照至上而下收录，匹配到了就停止不再往下

# 进阶配置
→ DIRECT: 直连 

→ REJECT: 该规则下不走网络活动，常用于广告拦截

→ .*: 表示加入你订阅中所有节点 

→ url-test: 表示有该代码下的节点会自动测速 

→ PROCESS-NAME,Cursor.exe  源进程名
