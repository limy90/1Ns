# 打造一个属于自己的clash分流配置

 [分流配置写法](https://github.com/chinnsenn/ClashCustomRule?tab=readme-ov-file)
 [分流配置写法](https://www.songxin.org/2023/01/12/%E5%B7%A5%E5%85%B7%E4%BD%BF%E7%94%A8/%E7%AE%80%E6%98%93%E6%95%99%E7%A8%8B-Clash-%E8%87%AA%E5%AE%9A%E4%B9%89%E5%9C%A8%E7%BA%BF%E5%88%86%E6%B5%81%E8%A7%84%E5%88%99%E7%AD%96%E7%95%A5%E7%BB%84/)
 [规则参考](https://github.com/lainbo/gists-hub/tree/master/src/Clash/List)

## 制作分流策略组
- 命名：文件命名随意，但是一定是英文+以 .ini 结尾。
  
- .ini 配置文件中：
- ruleset 指的是配配置中包含的分流规则，
- custom_proxy_group 指的是最终在Clash中呈现的分流策略组及其排序。

- ruleset 排序原则：
- 重要直连分流规则 > 去广告规则 > 小分流 > 国内外大分流 > 补充规则。
- 策略组的排序非常重要，因为分流策略组的匹配是按照至上而下收录，匹配到了就停止不再往下

## 进阶配置
→ DIRECT: 直连 

→ REJECT: 该规则下不走网络活动，常用于广告拦截

→ .*: 表示加入你订阅中所有节点 

→ url-test: 表示有该代码下的节点会自动测速 

# 自动归类节点 - 以图片中香港节点策略组为例
→ (港|HK|Hong Kong)
代表具有"港"，"HK"，"HongKong"关键词的节点会归类到香港节点这个策略组中，
测速以 http://www.gstatic.com/generate_204`300,,50为准。

以下规则说明均摘自 [订阅转换规则](https://github.com/tindy2013/subconverter/blob/master/README-cn.md#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)

### ruleset

> 从本地或 url 获取规则片段
>
> 格式为 `Group name,[type:]URL[,interval]` 或 `Group name,[]Rule `
>
> 支持的type（类型）包括：surge, quanx, clash-domain, clash-ipcidr, clash-classic
>
> type留空时默认为surge类型的规则
>
> \[] 前缀后的文字将被当作规则，而不是链接或路径，主要包含 `[]GEOIP` 和 `[]MATCH`(等同于 `[]FINAL`)。

    -   例如：

    ```ini
    ruleset=🍎 苹果服务,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Apple.list
    # 表示引用 https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Apple.list 规则
    # 且将此规则指向 [proxy_group] 所设置 🍎 苹果服务 策略组
    
    ruleset=Domestic Services,clash-domain:https://ruleset.dev/clash_domestic_services_domains,86400
    # 表示引用clash-domain类型的 https://ruleset.dev/clash_domestic_services_domains 规则
    # 规则更新间隔为86400秒
    # 且将此规则指向 [proxy_group] 所设置 Domestic Services 策略组
    
    ruleset=🎯 全球直连,rules/NobyDa/Surge/Download.list
    # 表示引用本地 rules/NobyDa/Surge/Download.list 规则
    # 且将此规则指向 [proxy_group] 所设置 🎯 全球直连 策略组
    
    ruleset=🎯 全球直连,[]GEOIP,CN
    # 表示引用 GEOIP 中关于中国的所有 IP
    # 且将此规则指向 [proxy_group] 所设置 🎯 全球直连 策略组
    
    ruleset=!!import:snippets/rulesets.txt
    # 表示引用本地的snippets/rulesets.txt规则
    ```

### custom_proxy_group

> 为 Clash 、Mellow 、Surge 以及 Surfboard 等程序创建策略组, 可用正则来筛选节点
>
> \[] 前缀后的文字将被当作引用策略组

```ini
custom_proxy_group=Group_Name`url-test|fallback|load-balance`Rule_1`Rule_2`...`test_url`interval[,timeout][,tolerance]
custom_proxy_group=Group_Name`select`Rule_1`Rule_2`...
# 格式示例
custom_proxy_group=🍎 苹果服务`url-test`(美国|US)`http://www.gstatic.com/generate_204`300,5,100
# 表示创建一个叫 🍎 苹果服务 的 url-test 策略组,并向其中添加名字含'美国','US'的节点，每隔300秒测试一次，测速超时为5s，切换节点的延迟容差为100ms
custom_proxy_group=🇯🇵 日本延迟最低`url-test`(日|JP)`http://www.gstatic.com/generate_204`300,5
# 表示创建一个叫 🇯🇵 日本延迟最低 的 url-test 策略组,并向其中添加名字含'日','JP'的节点，每隔300秒测试一次，测速超时为5s
custom_proxy_group=负载均衡`load-balance`.*`http://www.gstatic.com/generate_204`300,,100
# 表示创建一个叫 负载均衡 的 load-balance 策略组,并向其中添加所有的节点，每隔300秒测试一次，切换节点的延迟容差为100ms
custom_proxy_group=🇯🇵 JP`select`沪日`日本`[]🇯🇵 日本延迟最低
# 表示创建一个叫 🇯🇵 JP 的 select 策略组,并向其中**依次**添加名字含'沪日','日本'的节点，以及引用上述所创建的 🇯🇵 日本延迟最低 策略组
custom_proxy_group=节点选择`select`(^(?!.*(美国|日本)).*)
# 表示创建一个叫 节点选择 的 select 策略组,并向其中**依次**添加名字不包含'美国'或'日本'的节点
```

有了以上规则，理论上你可以自己配置所有你想要方式
