# clash-proxy-providers-rule-providers-
clash 如何添加多个订阅,proxy-providers和rule-providers的介绍和使用
Clash 是一个多平台的代理软件，它支持多种类型的代理，并且提供了灵活的规则设置。在 Clash 中，可以通过配置文件来设定代理和规则，而 proxy-providers 和 rule-providers 就是配置文件中的两个重要部分。

1. Proxy Providers: Proxy Providers 是 Clash 的一个功能，它允许你从远程获取代理服务器列表。你可以在配置文件中设定多个 Proxy Providers，每个 Proxy Providers 的格式如下：


```
proxy-providers:
  foo: # 代理提供者的名称为 "foo"
    type: http # 代理提供者的类型是 http，意味着 Clash 将从一个 http URL 获取代理服务器列表
    path: ./profiles/proxies/foo.yaml # 本地存储代理服务器列表的文件路径
    url: #你的订阅地址  #从这个 URL 获取代理服务器列表
    interval: 3600  #每 3600 秒（即一小时）更新一次代理服务器列表
    filter:  '英国 '#只接收包含“英国”在内的代理服务器
    health-check: # 这个部分定义了健康检查的设置
      enable: true # 启用健康检查
      url: http://www.gstatic.com/generate_204 # 用于健康检查的 URL，如果代理服务器可以成功访问这个 URL，那么就认为它是健康的
      interval: 300 # 每 300 秒（即五分钟）进行一次健康检查
```

    
2. Rule Providers: Rule Providers 是 Clash 的一个功能，它允许你从远程获取规则列表。你可以在配置文件中设定多个 Rule Providers，每个 Rule Providers 的格式如下：

```
Rule Provider:

 
rule-providers:
  reject: # 规则提供者的名称为 "reject"
    type: http # 规则提供者的类型是 http，意味着 Clash 将从一个 http URL 获取规则列表
    behavior: domain # 这个规则列表的行为是 "domain"，意味着这个列表包含的是域名规则
    url: YOUR_URL # 从这个 URL 获取规则列表
    path: ./ruleset/reject.yaml # 本地存储规则列表的文件路径
    interval: 86400 # 每 86400 秒（即一天）更新一次规则列表


3. 如何添加多个订阅: 在 Clash 的配置文件中，你可以添加多个 Proxy Providers 和 Rule Providers。只需要在配置文件中添加多个 Proxy Providers 和 Rule Providers 的定义即可。例如：

 
 
  proxy-providers:
    ProxyProvider1: # 代理提供者的名称为 "ProxyProvider1"
      type: http # 代理提供者的类型是 http，意味着 Clash 将从一个 http URL 获取代理服务器列表
      url: http://example.com/proxies1.txt # 从这个 URL 获取代理服务器列表
      interval: 1200 # 每 1200 秒（即20分钟）更新一次代理服务器列表
    ProxyProvider2: # 另一个代理提供者的名称为 "ProxyProvider2"
      type: http # 同样，代理提供者的类型是 http
      url: http://example.com/proxies2.txt # 从这个 URL 获取代理服务器列表
      interval: 1200 # 每 1200 秒更新一次代理服务器列表
 
 
  rule-providers:
    RuleProvider1: # 规则提供者的名称为 "RuleProvider1"
      type: http # 规则提供者的类型是 http，意味着 Clash 将从一个 http URL 获取规则列表
      url: http://example.com/rules1.txt # 从这个 URL 获取规则列表
      interval: 1200 # 每 1200 秒更新一次规则列表
    RuleProvider2: # 另一个规则提供者的名称为 "RuleProvider2"
      type: http # 同样，规则提供者的类型是 http
      url: http://example.com/rules2.txt # 从这个 URL 获取规则列表
      interval: 1200 # 每 1200 秒更新一次规则列表



以上就是 Clash 中 Proxy Providers 和 Rule Providers 的介绍和使用方法。请注意，你需要将上述的 URL 替换为你的实际的 URL。
