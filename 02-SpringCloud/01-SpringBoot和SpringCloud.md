# 关于SpringCloud、SpringBoot
## SpringBoot
 - 1. 核心思想：约定大于配置，让依赖变得有序简单，减少开发的配置事件
 - 2. 简化新的Spring应用的初始搭建以及开发过程

## SpringCloud
 - 1. 分布式服务治理的框架，专注于服务之间的通讯、熔断、监控
 - 2. 微服务之后，项目的数量变多，SpringCloud可以提供各种组件搭建服务要求的方案

## SpringCloud的常用组建
### Feign
 声明式服务调用
 - 1. 服务提供者：提供标准的接口
 - 2. 服务调用者：启用Feign，并在调用方接口上声明服务提供者的名字，如：@FeignClient(name = ApiConstant.SERVICE_NAME)

### Hystrix
  服务调用者的容错保护，有服务降级 、服务熔断、请求缓存、请求合并、依赖隔离

### Ribbon
  服务调用者的负载均衡器

### Bus
   消息总线，配置Config仓库修改

### Stream
   消息驱动，特性：订阅发布、消费组、消息分区

### Sleuth
   分布式服务跟踪，TraceID和SpanId

### Eureka
   注册中心，特性：失效剔除、服务保护

### Zuul
   API服务网关，功能有路由分发和过滤

### Config
   分布式配置中心   


## 总区别
 - 1. SpringBoot是Spring的一套快速配置的脚手架，可以基于SpringBoot快速开发当个微服务，SpringCloud是基于SpringBoot实现的云应用开发工具
 - 2. SpringBoot专注于快速、方面集成单个服务，SpringCloud关注全局的服务治理框架
