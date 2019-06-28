---
layout:     post   				    # 使用的布局（不需要改）
title:      Azure API Management Security - Shared Secret 				# 标题 
subtitle:   Shared Secret #副标题
date:       2019-06-28 				# 时间
author:     Henry 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Azure
---

## Azure API Management Gateway Security and Protection
>Azure API Management 网关与服务提供者直接可以通过多种方式来保证安全：
  - HTTP Basic
  - Mutual Certificate
  - Shared Secret
  - IP Filter
  - VNET/NSG

今天主要介绍 Shared Secret，通过在API Management Gateway inbound request 里设置一个shared secret，后台服务提供者来校验这个secret来防止非法的请求。 前端的客户端不需要做任何改动，通过Azure Portal 来完成设置。
  - 在 API Management -> Named value 增加两个properties

  
|  Display Name   | Values  |
|  ----  | ----  |
| SSHeaderName  | apiss |
| SSHeaderValue  | ***** |

- 在对应的API inbound request policy 中增加以下设置：
```<set-header name="{{SSHeaderName}}" exists-action="override">
    <value>{{SSHeaderValue}}</value>
</set-header>
```
- 通过Developer Portal 追踪Request可以看到之前设置的Header 已经添加进去了
```"headers": [
            {
                "name": "Host",
                "value": "conferenceapi.azurewebsites.net"
            },
            {
                "name": "apiss",
                "value": "fabd32e06cae48ddaebb96b7261cab38"
            },
            {
                "name": "Ocp-Apim-Subscription-Key",
                "value": "b3580fb1d2104e67a7ca6b79f3dd2667"
            },
            {
                "name": "Request-Id",
                "value": "|09d77070-3fbb-4ef8-94a8-57ef6474fcae.3d48b3dc."
            },
            {
                "name": "Request-Context",
                "value": "appId=cid-v1:bd4d0747-2b3a-4a0c-8ff9-0d5fdf19acc8"
            },
            {
                "name": "X-Forwarded-For",
                "value": "40.118.203.215"
            }
        ]
```
