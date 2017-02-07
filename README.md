XSSO

统一单点登陆验证服务



1. 可对单点登陆验证服务进行集群。其目的是为了安全，多一个容灾用的备份服务，并不是为了提高性能，它也没有多大的性能消耗，所以集群两台即可。

2. 会话数据是用于通讯的数据结构，它有三种方式。

   2.1 只保存票据，不保存会话数据；

   2.2 采用可通用可动态扩展的Map集合数据结构；

   2.3 采用专属数据结构，将应用服务上的会话数据Java类，打成jar包的方式或直接复制源码的方式放进来即可。

3. 经实测：

   3.1 集群中所有单点登陆验证服务因断电等原因均故障时，不影响应用服务器正常登陆的。

   3.2 集群中某一台单点登陆验证服务故障重启后，故障前的会话数据不丢失，对于故障前、后已登陆的用户依然保证单点登陆的能力。

   3.3 应用服务器故障重启后，从单点登陆验证服务同步会话数据后，依然保证故障前、后已登陆的用户有单点登陆的能力

4. 票据由应用服务生成，可活动的个性化定制票据格式。同时，也有利于单点登陆验证服务无主从关系的集群架构。

5. 数据通讯的主端口为1821，浮动端口为17000~17999，均可在sys.ServerConfig.xml配置中修改。请保证服务器防火墙允许这些端口的通讯。

6. 监控页面(默认密码xsso)

➢ 在线用户数量 http://127.0.0.1:8080/XSSO/analyses/analyseObject?xid=USID*

➢ 在线用户的具体信息 http://127.0.0.1:8080/XSSO/analyses/analyseObject?xid=完整的票据号