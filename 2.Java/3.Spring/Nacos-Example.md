### Nacos-Example

Nacos（ Dynamic Naming and Configuration Service ）可作为服务注册中心和配置中心。

下载Nacos-server： https://github.com/alibaba/nacos/releases 

单点启动：

- linux：`sh startup.sh -m standalone` 
- windows：`cmd startup.cmd` 

Console：http://127.0.0.1:8848/nacos/index.html

#### Nacos 注册中心

引入Maven依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
    <version>0.9.0.RELEASE</version>
</dependency>
```

##### 服务提供者

Nacos-Provider配置文件： `bootstrap.yml` 或  `bootstrap.properties`。

```yml
server:
  port: 8082
  servlet:
    context-path: /provider
spring:
  application:
    name: nacos-provider
  cloud:
    nacos:
      # 注册中心
      discovery:
        server-addr: 47.93.251.190:8848 # nacos-server地址和端口
```

SpringBootApplication启动类新增注解：`@EnableDiscoveryClient`。

```java
@SpringBootApplication
@EnableDiscoveryClient
public class NacosDiscoveryProviderApplication {
	public static void main(String[] args) {
		SpringApplication.run(NacosDiscoveryProviderApplication.class, args);
	}
}
```

服务提供接口：

```java
@RestController
@RequestMapping(value = "/provide/")
public class NacosDiscoveryProviderController {
	@GetMapping(value = "out/{value}")
	public String provider(@PathVariable String value) {
		return "Nacos Provider Out::" + value;
	}
}
```

##### 服务消费者

Nacos-Consumer配置文件： `bootstrap.yml` 或  `bootstrap.properties`。

```yaml
server:
  port: 8083
  servlet:
    context-path: /consumer
spring:
  application:
    name: nacos-consumer
  cloud:
    nacos:
      # 注册中心
      discovery:
        server-addr: 47.93.251.190:8848 # nacos-server地址和端口
```

SpringBootApplication启动类新增注解：`@EnableDiscoveryClient`。

```java
@SpringBootApplication
@EnableDiscoveryClient
public class NacosDiscoveryConsumerApplication {
	public static void main(String[] args) {
		SpringApplication.run(NacosDiscoveryConsumerApplication.class, args);
	}
}
```

消费者远程调用服务：

```java
@RestController
@RequestMapping(value = "/consume/")
public class NacosDiscoveryConsumerController {
	@Bean
	@LoadBalanced
	public RestTemplate getRestTemplate() {
		return new RestTemplate();
	}

	@Autowired
	private RestTemplate restTemplate;

	@GetMapping(value = "/get/{value}")
	public String consumer(@PathVariable String value) {
		String url = "http://nacos-provider/provider/provide/out/"+value;
		String callServiceResult = restTemplate.getForEntity(url, String.class).getBody();
		return callServiceResult;
	}
}
```

##### 服务注册策略

Nacos 服务注册策略：每5s向nacos-server发送一次心跳（携带服务名、服务IP和端口等）， 同时nacos-server会向client发起健康检查，支持tcp/http检查，如果15s内无心跳且健康检查失败，则认为实例不健康。如果30秒内健康检查失败则剔除实例。 

#### Nacos 配置中心

引入Maven依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
    <version>0.9.0.RELEASE</version>
</dependency>
```

创建配置文件： `bootstrap.yml` 或  `bootstrap.properties`。

> ※ 配置文件命名必须为bootstrap。

```yml
server:
  port: 8083
  servlet:
    context-path: /config
spring:
  application:
    name: nacos-config # 应用名称，默认的prefix，dataId 相关。
  profiles:
    active: dev # 当前环境，dataId 相关。
  cloud:
    nacos:
      # 注册中心
      discovery:
        server-addr: 47.93.251.190:8848 # nacos-server地址和端口
      # 配置中心
      config:
        server-addr: 47.93.251.190:8848 # nacos-server地址和端口
        prefix: nacos-config # dataId prefix
        file-extension: yml # 配置文件类型
        group: GROUP1 # 组
        namespace: e5fc50b3-4af9-40f7-b49d-8428f2951b1f # 组命名空间
```

**Nacos 配置 dataId 规则**：

```yml
${prefix}-${spring.profile.active}.${file-extension}
```

- prefix： 默认为 spring.application.name 的值，也可  spring.cloud.nacos.config.prefix 配置。
- spring.profile.active：当前环境对应的profile，如 test、uat、prod 之类，若未设置，则为空。
- file-extension：文件格式，默认properties，也可通过 spring.cloud.nacos.config.file-extension 配置。
- group：默认 **`DEFAULT_GROUP`** ，可通过 spring.cloud.nacos.config.group 配置。

> 配置文件分组：根据 spring.profile.active 环境进行分组，根据 group+namespace进行业务独立分组/功能层级分组。

##### Nacos 多配置加载

**外部配置 ext-config[n]**：n越小加载优先级越高，后加载配置覆盖先加载配置。

```yml
server:
  port: 8083
  servlet:
    context-path: /config
spring:
  application:
    name: nacos-config # 应用名称，默认的prefix，dataId 相关。
  profiles:
    active: dev # 当前环境，dataId 相关。
  cloud:
    nacos:
      discovery:
        server-addr: 47.93.251.190:8848 # nacos-server地址和端口
      config:
        server-addr: 47.93.251.190:8848 # nacos-server地址和端口
        prefix: nacos-config # dataId prefix
        file-extension: yml # 配置文件类型
        group: GROUP1 # 组
        namespace: e5fc50b3-4af9-40f7-b49d-8428f2951b1f # 组命名空间
        # 外部配置：n越小加载优先级越高。
        ext-config[0]:
          dataId: common.yml
          group: GROUP1 # 要加载的外部配置的所属组
          refresh: true # 配置文件是否支持动态刷新，默认不支持
        ext-config[1]:
          dataId: log.yml # 要加载的外部配置的dataId
          group: GROUP1 # 要加载的外部配置的所属组
          refresh: true # 配置文件是否支持自动刷新，默认不支持
```

> 可加载不同 Group 下的配置文件。

**共享配置 shared-dataids**：

```yml
server:
  port: 8083
  servlet:
    context-path: /config
spring:
  application:
    name: nacos-config
  profiles:
    active: dev
  cloud:
    nacos:
      # 注册中心
      discovery:
        server-addr: 47.93.251.190:8848 # nacos-server地址和端口
      # 配置中心
      config:
        server-addr: 47.93.251.190:8848 # nacos-server地址和端口
        prefix: nacos-config # dataId prefix
        file-extension: yml # 配置文件类型
#        group: GROUP1 # 组
#        namespace: e5fc50b3-4af9-40f7-b49d-8428f2951b1f # 组命名空间
        #外部配置
        ext-config[0]:
          dataId: config.yml
#          group: GROUP1 # 外部配置的所属组
          refresh: true # 配置文件是否支持自动刷新，默认不支持
        ext-config[1]:
          dataId: log.yml # 外部配置的dataId
#          group: GROUP1 # 外部配置的所属组
          refresh: true # 配置文件是否支持自动刷新，默认不支持
        # 共享配置
        shared-dataids: global.yml,common.yml # 共享配置dataId，使用","分割，以先后顺序加载。
        refreshable-dataids: global.yml,common.yml # 共享配置开启动态刷新，使用","分割。
```

> 只能加载同一 Group 下的配置文件。
>
> ？config或ext-config 指定 group 后，共享配置无法正常加载。

**Nacos 配置加载优先级**： A < B < C，后加载配置覆盖前加载配置。 

- A：通过 `spring.cloud.nacos.config.shared-dataids` 支持多个共享 Data Id 的配置。
- B：通过 `spring.cloud.nacos.config.ext-config[n].data-id` 的方式支持多个扩展 Data Id 的配置，n越小加载优先级越高。
- C： 通过内部相关规则(应用名、应用名+ Profile )自动生成相关的 Data Id 配置。

> 相关源码：https://github.com/liziczh/lizi-nacos/