##  **前言** 

 最近因为工作需要，集中精力在研究第三方shiro鉴权框架的使用技巧，既然说到了shiro是用来做权限校验功能的，那么shiro的核心在哪呢，它由哪几块组成的，每一块的作用是什么？它与其它鉴权框架相比有什么优势？ 带着这些问题，我便对shiro展开了猛烈攻击。 



##  Shiro简介

 Apache Shiro 是Java的一个安全框架，因为对比Spring Sercurity 相对简单，所以使用的人也是越来越多。shiro可以帮助我们完成：认证、授权、加密、会话管理、与web集成、缓存等一条龙服务。并且它的API也是很简单的。话不多说先上官图： 

```
<img src="https://github.com/qq1371189713/Builder_Walle/blob/master/images/shiro1.png" width="100%">
```

1.Authentication:做身份认证/登录，验证用户是否有登录身份。

2.Authorization：与前一个英文拼写比较相似，大家不要搞混淆了，这个是用来做权限验证。验证用户是否有某个功能权限。是否有资格去操作某个功能。

3.Session Management : 会话管理，用户在登录完成以后就会形成一次会话，在没有退出系统（或浏览器）之前，他的所有信息都存在会话当中。

4.Cryptography:加密功能，用来保护数据的安全性，像MD5,RSA这些加密算法都是用来保护密码的安全。

5.Web Support:web支持，可以集成到web环境。

6.Caching:缓存，在账户登录以后，其用户信息、对应角色、权限资源不必每次到数据库中查询，提高效率。

7.Concurrency:shiro支持多线程应用的并发验证，例如在开启一个线程的时候同时开启另外一个线程，能把权限自动传播过去。

8.Testing:提供测试支持。

9.Run As: 允许一个用户装扮成另一个用户的身份进去访问（在授权之后）。

10.Remember Me: 记住账号，这是很常见的一个功能，在登录一次后，自动保存账号信息

一个完整的shiro工作流程 大致是 ：  Application Code   (请求进来)---->  把当前的用户存放到Subject 对象当中 ---->Shiro SecurityManager (管理所有的subject对象)   ----> Realm(验证登录用户，一般与数据库交互做验证，可以自定义实现realm对象)  

1.Subject:是shiro的核心之一，代表当前登录用户，这个用户的身份可以是任何与系统交互的主体，如爬虫、机器人等等，是一个抽象主体。

2.SecurityManager：安全管理器，所有的Subject都会绑定到这里，所有操作都会与SecurityManager进行交互，管理着Subject,有点类似与springmvc中的DispatcherServlet 前端控制器。

3.Relam: shiro从Realm那里（与数据库交互）获取安全数据，如用户，角色，权限资源，SecurityManager 要验证用户身份，需要从Realm获取用户进行对比身份是否合法，可以把Realm看做是DataSource.
