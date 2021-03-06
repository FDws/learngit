# 中间件
1. 概念/核心/组成 - 远程过程调用
2. 基本定义: 中间件是一种软件, 它能够使得处于应用层中的各个应用成分之间实现跨网络的协同工作(即互操作), 这时允许各应用成分之下所涉及的"系统结构/操作系统/通信协议/数据库和其他应用服务各不相同

## RPC(远程过程调用)
1. 基本功能:
    - 语义的角度: RPC用过程调用实现远程通信
    - 应用的角度: RPC基于过程的远程通信特点, 为网络和分布式系统的应用提供了灵活方便的通信功能
    - RPC实质是实现网络七层协议中会话层的功能
2. 模型: 服务方侦听客户请求, 当客户的请求到达以后, 调用制定的过程进行处理, 并把执行结果返回给客户端
3. 语义规则: 
    - Last-Of-Many: 服务方最后一次的执行结果作为最终结果返回
    - At-Most-One: 调用过程最多执行一次, 即收到结果认为调用成功, 未收到结果看作没用调用过
    - At-Least-One: 调用过程至少执行一次, 回复消息可能有多次
    - Exactly-Once: 若服务正常, 则远程过程恰好执行一次, 并且返回一个调用结果
4. 语义存在的问题:
    - RPC中数据表示问题
    - 指针问题
    - 故障问题
    - 被调用者未收到调用命令之前的故障
    - 执行过程体时的故障
    - 结果返回被调用者之前故障
5. 排队RPC: 使得RPC拥有一定的队列机制, 提高性能
## ODP(面向对象中间件)
1. 面向对象优势: 数据与相关功能是捆绑在一起的, 更好的表示了系统中相对独立的对象
2. 基本概念: 对象(Object) / 类(Class) / 封装(Encapsulation) / 抽象(Abstract) / 多态(Polymorphism)
## CORBA(公共对象请求代理体系结构)
0. ORB: 对象请求代理, 
    - 是对象之间建立客户端/服务器关系的中间件, 在CORBA规范中处于核心地位.
    - ORB可以使得对象透明的向其他本地或者远程对象发出请求或获得应答
1. CORBA ORB 优点:
    - 静态和动态的方法调用 : 既可以在编译时静态的定义方法调用也可以在运行时动态查找
    - 高级语言绑定 : 服务对象的语言不受限
    - 位置透明 : 既可以单机运行也可以与其他ORB互联
    - 内置安全和事务处理
    - 与遗留系统共存: CORBA 可以让对象的定义与实现分离
2. 最重要特征: 提供了客户与目标对象之间的交互透明性, 屏蔽了一下内容
    - 对象位置: 客户并不需要知道目标对象的物理位置
    - 对象实现: 客户不必知道有关对象实现的具体细节
    - 对象的执行状态
    - 对象的通信机制
    - 数据表示
3. IDL(Interface Description Language) 接口定义语言
    - 纯说明性语言, 与主机上的编程语言无关
    - 通过一种中立的方式描述接口, 使得不同编程语言可以通过此接口进行通信, 使用不同的语言来实现对象, 而他们之间又可以进行互操作.
4. 动态调用
    - 动态调用界面 - 支持客户方的动态请求调用
    - 动态框架界面 - 支持服务方的动态对象调用
5. 对象适配器
    - 对象登记
    - 对象引用的产生
    - 服务器进程的激活
    - 对象的激活
    - 对象的撤销
    - 对象向上调用
6. 核心服务
    - 对象定位: 通过名称服务和交易服务
    - 对象消息: 事件服务定义了组件之间消息传输的框架
    - 安全: 安全服务
## JavaEE
1. Java企业版本
2. 包含技术:
    - EJB
    - RMI(Java 远程方法调用)
    - JNDI(Java 名称和目录接口)
    - JDBC
    - JTA JTS 支持事务处理
    - JMS(Java 消息服务) : 用户分布式对象的异步通信
    - Java Servlet JSP
    - Java IDL: 使其他语言与Java集成
    - Connectors: 使得JavaEE可以运行高端事务处理的主机系统集成
## EJB
1. 是一种C/S结构, 提供服务的方法运行在服务端, 根据客户端的请求调用相应的方法
2. 主要包括
    - EJB构件
        - 会话bean(Session Bean)维护会话: 短暂对象, 运行在服务端, 执行一些应用的逻辑处理. 分为有状态和无状态bean.
        - 实体bean(Entity Bean)处理事务: 持久化的对象, 可以被其他对象调用, 不维护客户端状态, 具有唯一的标识
        - 消息bean(MessageDrivenBean)提供异步消息机制: 专门设计用来处理JMS消息 
    - 容器
    - 服务器
    - EJB对象
    - EJBHome
3. EJB容器:EJB构件运行时的环境, 是一层代替bean执行相应服务的接口.
    - 客户通过接口与EJB通信
        - Home接口: 用户请求服务首先通过JNDI服务定位对象的Home接口, 然后通过调用Home接口中的方法建立EJB对象
        - 远端调用接口: 由EJB容器提供的EJB类的一个对象, 它用来实现EJB远端调用接口.
4. EJB角色
    - EJB服务提供者
    - EJB容器提供者
    - 企业beans提供者
    - 应用程序组装者
    - 配制者
    - 系统管理员
    - 持久性管理器提供者
5. 与其他技术的关系
    - EJB与JavaBeans的一个重要区别是EJB提供了网络功能
    - 以后会有许多基于CORBA的EJB产品, EJB到CORBA的映射
        - 分布映射
        - 命名映射
        - 事务映射
        - 安全性映射
## COM(组件对象模型)
1. 实质: 一种对象组件构造和使用对象组件来构造应用程序的框架规范, 同时也是一种软件组织方式
2. 最常见的发布方式`DLL`
4. 应用程序分为客户和服务器
5. 核心概念:
    - 组件: 具有一定逻辑的可执行代码, 组成应用程序的构件
    - 接口: 对其他软件和组件能使用的公共功能的定义, 是组件与外界的交互通道
6. COM中的接口:
    - 由函数指针表构成的一个内存结构
    - 所有的COM组件必须实现`IUnknown`接口
    - 采用引用计数的方法进行声明周期的管理
    - 所有的COM接口都继承了`IUnknown`接口
    - `IDispatch`接口使程序更容易的使用组件
    - 所有的接口都有两个名称: 
        - 字符串(可重复)  供人识别
        - 软件使用的名称(唯一) 供软件识别, 通常使用GUID
    - 通常使用界面描述语言(IDL) 来描述接口
7. 类工厂机制
    - 类工厂: 可以创建其他组件的组件
    - 类工厂没有唯一的CLSID标识符
    - 没有在注册表中注册
    - 用于创建组件的标准接口为`IClassFactory`
8. COM组件开发步骤
    - 编写组件实现类
    - 编写组件的类工厂
    - 编写DLL的辅助代码
    - 注册组件, 完成发布
3. DCOM: 分布式环境中的COM
    - 使用RPC提供分布功能
    - DCOM将COM技术扩展到分布式计算领域, 通过DCOM配置程序, 使得COM组件不经修改就可以在网络环境中运行
4. COM+
    - 面向应用的高级COM运行环境, 他在COM编程模型的基础上实现了许多面向企业应用的分布式应用程序所需的服务
    - 截取控制策略使COM+技术的核心
5. COM/DCOM/COM+技术使微软在分布式环境下的基本规范, 适合在客户机和服务器端开发应用程序, 提供了可靠的/统一的操作环境, 使得软件开发更简单
6. .NET
    - 一个主要目的是简化COM开发
## RMI(远程方法激发)
1. 概述: 使程序可以调用不同虚拟机上的方法, 但是使程序员认为调用的是本地类文件上的本地方法
2. 目标:
    - 支持不同虚拟机上对象之间无缝的远程调用
    - 支持服务器对客户端的回调
    - 把分布式对象模型继承到Java语言中, 尽可能在语义上保留Java语言的面向对象特性
    - 使分布式对象模型和本地Java对象模型间的不同表面化
    - 使编写可靠的分布式应用程序尽可能简单
    - 保留Java运行时环境提供的安全性
3. 三层体系结构:
    - 存根/框架层(Stub/Skeleton): 应用程序与系统其他部分的接口
        - 存根是客户内部完成打包数据和管理网络连接工作的本地对象, 在客户调用远程对象上的方法时, 实际调用的是本地存根对象上的方法
        - 框架负责接收并且解包远程方法调用为本地方法调用
    - 远程引用曾(Remote Reference): 提供远程引用和调用协议的支持
    - 传输层: 在不同的地址之间传输序列化的字节流
4. 序列化:
    - 实现`Serializable`接口
    - 有无参的`public`构造方法
    - 类中不包含不可序列化的引用
## DCE(分布式计算环境)
1. 应用开发者需要提供三个文件:
    - 界面定义文件: 服务器提供的远程过程调用的界面(数据结构/过程名/参数)
    - 客户程序: 定义了用户界面, 对远程过程的调用以及客户方的处理功能
    - 服务器程序: 提供远程调用的实现
2. 提供两种服务:
    - 基础服务
        - 线程服务
        - RPC服务
        - 目录服务
        - 安全服务
    - 扩充性服务
        - 分布式文件服务
        - 时间服务
3. 存在问题
    - RPC设计不周, 开发工具薄弱
    - 性能差/适用系统少/使用困难
    - 没有采用面向对象技术
## Web 服务
1. WebService是在Internet上进行分布式计算的基本构造块
2. 优点之一就是允许在不同平台上, 以不同的编程语言编写的各种程序以基于标准的方式相互通信
3. SOAP Web服务的通信协议, 用来定义消息的XML格式, 不一定使用HTTP
4. WSDL: Web服务说明语言
    - 用于说明一组SOAP消息以及如何交换这些消息
    - 与编程语言无关, 适用于说明不同平台/不同编程语言访问的Web 服务接口.
    - 定义了服务位置, 以及使用什么样的通信协议与服务进行通信
## 事务处理
1. 事务的ACID特性
    - 原子性(Atomicity)
    - 一致性(Consistency)
    - 孤立性(Isolation)
    - 持久性(Durability)
2. 分布式事务处理模型`X/OPEN DTP`
    - 由三部分组成
        - 应用程序(Application Program AP) : 分布式事务的使用者, 是开始(begin), 提交(Commit), 回滚(Rollback)事务的发出者
        - 资源管理器(Resource Manager RM): 提供对共享资源的访问, 例如数据库管理系统/文件访问系统
        - 事务管理器(Transaction Manager TM): 应用程序与资源管理器中间的协调者, 为每个事务分配标识符, 监视事务的进展, 保证事务处理的顺利进行, 并负责事务失败后的恢复
    - 处理过程: 应用程序首先通过Tx接口告诉事务管理器需要开始一个事务, 事务管理器负责分配全局的事务ID, 调用XA接口通知各个资源管理器一个新的事务开始. 然后应用程序访问资源管理器,. 当操作完成以后, 应用程序要求事务管理器提交事务, 事务管理器调用XA接口协调各个资源管理器进行事务的提交
3. 事务的类型
    - 平坦事务: 所有的操作都包含在一组开始和结束事务的语句中间, 这些操作处于同一级别, 被视为一个整体. 平坦事务在AP调用`tx_begin()`时才开始执行.
    - 链式事务: 在链式食物中, 事务的开始并不要求AP显示的调用`tx_begin()`, 当前事务的结束(`tx_commit()/tx_rollback`)就标志着下一个事务的开始, 事务与事务像链条一样彼此相接
    - 嵌套事务: 事务就有不同的级别, 事务可以包含子事务, 形成树状的事务结构, 树的叶子是平坦事务, 树根是顶层事务. 一个事务的回滚导致其他的事务回滚; 一个子事务能够提交不仅取决于自己, 而且取决于它的所有祖先事务都能成功提交
    - 从作用域的角度, 事务可以分为全局事务和本地事务
4. 两阶段提交协议(Two Phase Commitment Protocol)
    - 作用: 分布式事务涉及到多个节点数据的更新, 任何一个节点或者结点之间通信的失效都可能导致分布式事务的失败. 为了保证事务的完整性, 分布式事务采用两阶段提交协议.
    - 当事务管理器向资源管理器发出正式的提交请求前, 先询问所有的资源管理器是否已经准备好提交. 仅当所有的资源管理器都给出了肯定的答复时, 事务管理器才发出提交请求. 若有资源管理器给出否定的回答, 则事务管理器指示所有的资源管理器进行回滚
    - 两个阶段
        - 准备阶段: 询问时候准备好了
        - 提交阶段: 检查回答, 指示提交或者回滚