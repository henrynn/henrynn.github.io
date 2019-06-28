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
    1. HTTP Basic
    2. Mutual Certificate
    3. Shared Secret
    4. IP Filter
    5. VNET/NSG

今天主要介绍 Shared Secret，通过在API Management Gateway inbound request 里设置一个shared secret，后台服务提供者来校验这个secret来防止非法的请求。 前端的客户端不需要做任何改动，通过Azure Portal 来完成设置。


