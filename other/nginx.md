# nginx作用于用途

- 负载均衡

- 动静分离

- 高可用

# nginx 反向代理配置

- 全局块->work_processes；支持的并发处理量

- 局部块（events）-> worker_connections 1024;支持最大的连接数

- http 块
  - http全局块：文件引入，MIME-TYPE 定义，日志自定义，连接超时时间，单链接请求上限等。
  - server块:与虚拟主机有密切关系，虚拟主机从用户角度看，和一台独立的硬件主机是完全一样的，该技术产生是为了节省互联网服务器硬件成本；每个http块可以包括多个server块，而每个server块就相当于一个虚拟主机；server也分为全局server块，以及可以同时包含多个location块。
  - location块：一个server可以配置多个location;作用是基于nginx服务器接收到请求字符串（如：server_name/uri-string），对虚拟主机名称（也可是IP别名）之外的字符串（如：/uri-string）进行匹配；对特定请求处理，数据缓存和应答控制等功能；还有许多第三方模块配置也在这里进行。

## location 配置规则

- =：用于不含正则表达式的uri前，需要与uri严格匹配。
- ~：用于uri包含正则表达式，区分大小写
- ~*：用于表达uri正则，不区分大小写
- ^~：用于不含正则表达式uri前，要求nginx服务器找到表示uri和请求字符串匹配度最高的location后，使用此location处理请求，而不再使用location块中的正则uri和请求字符串匹配。

# nginx 负载均衡配置

## 配置步骤

- 先在http快配置自定义server,里面配置服务器地址。

  - upsteam myserver {

    ​	server 127.0.0.1:8080 weight=5

    ​    server 127.0.0.1:8080 weight=10

    ​     fair

    }

- 在loaction中加入
  - proxy_pass http://myserver;

## 分配策略

 ### 轮询（默认）

- 每个请求按时间顺序逐一分配到不同后端服务器，如果后端服务器down掉，能自动删除。

### weight(权重)

- weight代表权重，默认为1，权重越高，被分配的客户端越多。
- 制定轮询几率，weight和访问率成正比，用于后端服务器性能不均衡的情况。

### ip hash(指定)

- 每个请求按访问ip大的hash结果分配，可以固定每个访问一个后端服务器。
- 可以解决session共享的问题

### fair（第三方）

- 按后端服务器的响应时间分配，响应时间短的优先分配。

# nginx动静分离

## 实现方式

- 把静态文件独立成单独的域名，放在独立的服务器上。
- 动态和静态一起发布，通过nginx分开。

# nginx配置高可用

## 准备环境

- 两台安装nginx服务器
- 两台服务器上安装 keepalived
- 安装后，在etc生成目录keepalived，有文件keepalived.conf

## 高可用配置





# nginx原理

## 主从复制(master/worker)

- 一个master和多个worker有哪些好处
  - 可以使用nginx -s reload 热部署，利于nginx热部署操作。
  - 对于每个worker都是独立的进程，不需要加锁。互不干扰。
- 设置多少个worker才合适？
  - nginx采用多路复用机制。
  - 跟当前电脑的(cpu)核数相等。
- worker连接数（worker_connection）？
  - 发送一个请求，占用几个worker数？
    - 2个或者4个。
- worker支持的最大并发数？
  - (worker_connection * worker_processes)/2  或者/4;