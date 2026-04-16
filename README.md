- [规则参考](https://github.com/lainbo/gists-hub/blob/73b207e3d7cd4c1918efe4f03e0f3739cb4a5cfa/src/Clash/RemoteConfig/Lainbo.ini)
- [blackmatrix7大佬规则](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash)
- [subconverter](https://github.com/tindy2013/subconverter/blob/master/README-cn.md#配置文件)
- [分流配置写法](https://github.com/chinnsenn/ClashCustomRule?tab=readme-ov-file)
- [Clash 中 GeoSite 分流的正确使用方式](https://www.aloxaf.com/2025/04/how_to_use_geosite/)
- [关于 Clash 等现代代理软件的规则和 dns 配置问题](https://linux.do/t/topic/155121)
- [虚空终端 Docs](https://wiki.metacubex.one/config/rules/)
- [海豚测速 - 网络代理工具箱](https://www.haitunt.org/app.html)
- [CDN查询](https://www.cdnplanet.com/tools/cdnfinder)

 ### ruleset 排序原则：
- 重要直连分流规则 > 去广告规则 > 小分流 > 国内外大分流 > 补充规则
- 策略组的排序非常重要，因为分流策略组的匹配是按照至上而下收录，匹配到了就停止不再往下

# 进阶配置
→ DIRECT: 直连 

→ REJECT: 该规则下不走网络活动，常用于广告拦截

→ PROCESS-NAME,Cursor.exe  源进程名
