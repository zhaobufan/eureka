# eureka
服务的注册与发现
 Eureka Server与Eureka Client之间的联系主要通过心跳的方式实现。
 心跳(Heartbeat)即Eureka Client定时向Eureka Server汇报本服务实例当前的状态，维护本服务实例在注册表中租约的有效性。
 高可用：可以通过运行多个Eureka server实例并相互注册的方式实现。Server节点之间会彼此增量地同步信息，从而确保节点中数据一致。
 单机搭建多节点，实现高可用 （修改本机host文件，绑定一个主机名，单机部署时使用ip地址会有问题）
    

Eureka Client将定时从Eureka Server中拉取注册表中的信息，并将这些信息缓存到本地，用于服务发现。
eureka 配置参数说明
  ------ server -------
   #Eureka在CAP理论当中是属于AP ， 也就说当产生网络分区时，Eureka保证系统的可用性，但不保证系统里面数据的一致性
   #默认开启，服务器端容错的一种方式，即短时间心跳不到达仍不剔除服务列表里的节点
   #关闭自我保护模式
  eureka.server.enable-self-preservation=false
   #续约发送间隔默认30秒，心跳间隔
  eureka.instance.lease-renewal-interval-in-seconds=5
  ---- client-----------
  #是否将自己注册到Eureka Server,默认为true 表明该服务会向eureka注册自己的信息
  eureka.client.refetch-registry=true
  #是否从eureka server获取注册信息 默认为true
  eureka.client.fetch-registry=true
   #设置服务注册中心的URL，用于client和server端交流
  eureka.client.service-url.defaultZone=http://${eureka.instance.hostname}:${server.port}/eureka
  #表示eureka client间隔多久去拉取服务注册信息，默认为30秒，对于api-gateway，如果要迅速获取服务注册状态，可以缩小该值，比如5秒
  eureka.client.registry-fetch-interval-seconds=5
  # 续约到期时间（默认90秒）
  eureka.instance.lease-expiration-duration-in-seconds=60
 
  
  
                  
                     
    
