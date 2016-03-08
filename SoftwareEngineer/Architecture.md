#Architecture
---
#theory
[架构之路（一）：目标](http://www.csdn.net/article/2015-09-22/2825768)
[架构之路（二）：性能](http://www.csdn.net/article/2015-09-22/2825773)
[架构之路（三）：单元测试](http://www.csdn.net/article/2015-09-22/2825774)
[架构之路（四）：测试驱动]()


---

#关于业务
按业务需求来使用技术
驱动技术的是业务发展
##不要企图用技术解决所有问题
技术用来解决业务问题，而技术上很难实现的业务问题也可以用业务来解决




##分割
纵向分离系统
分离不相关业务组件
##分布式
问题和挑战：网络延迟->性能问题；服务器宕机；数据一致性；开发管理维护困难
分布式应用
分布式存储
分布式静态资源，各资源独立域名
分布式计算
##集群
提供更好得并发性
##缓存
CDN
反向代理
本地缓存
分布式缓存
前提：数据访问热点不均衡，部分数据频繁访问；
数据在一定时间内有效
##异步
可用性：消息可堆积在队列
响应速度：
消除并发访问高峰：
##冗余
##自动化
发布
代码管理
测试
安全检测部署
监控
报警
失效转移
失效恢复
降级
分配资源
##安全




---
#性能
    解决性能问题，我们可以有很多代码以外行之有效的方法，而可维护性基本上就只能靠代码了
    过早的优化是万恶之源
    优化首先需要找到性能“瓶颈”。否则，任何人都可以随手一指，“这段代码需要优化”
    可读性更强的代码总是更好优化
    硬件永远比软件便宜

响应时间
响应性，如响应后，但短时间无法处理，但给出处理进度条
等待时间
吞吐率
负载
负载敏感度，响应时间随负载变化程度
效率
容量
可伸缩性


吞吐率
瓶颈：找到关键因素
随时间的变化，随环境(用户差异，存储量，数据量，系统的优化，硬件的更换……)的变化
长尾效应，多个子因素共同提升后带来整体性能提升

带宽
http请求，对于网页本身的优化
脚本计算速度
动态内容缓存，缓存命中率，策略，大小，哪些部分，过期策略，分布式多台服务器的缓存
数据缓存，数据库或磁盘中的数据，网页中公用数据
动态内容静态化，缓存一样的问题
web软件
页面组件升级，分离物理资源，针对性的使用并发策略
服务器部署
负载均衡，dns，lvs，反向代理
优化数据库，连接池，安全性，存储引擎特性，索引，散列数据
扩展性，
视觉等待减少

c2网络
传输速度，带宽，处理速度，中间节点
c3服务器并发处理能力
吞吐率
压力测试
合理的并发数，过大崩溃，过小浪费





---
#安全

---
#维护
    扩展

---
#成本

---
#模块划分



----
#案例
[【SDCC讲师专访】架构师王小雪：解析快的打车的高可用架构](http://www.csdn.net/article/2015-10-28/2826069)
可用性：这是最重要的，系统不可用什么都是浮云。这里要考虑的点很多，例如单点、性能瓶颈、可能的风险、快速发现故障、快速定位问题原因等
扩展性：基于高度的复用抽象，能够快速灵活的满足业务需求
伸缩性：系统服务能力是否可以随着加机器得到线性的提升
安全性：不给外部钻空子的机会
技术栈：在一个公司里，过多的语言选型或者同一个领域过多的架构选型，不是一件好事，除非是的确有必要，否则会花巨大的成本在内部系统整合上，因为语言不一样，很多东西很难复用，也很难集中力量对某个语言生态有深度的掌握，这是没有必要的。不是说架构师不应该多学习几门编程语言，而是要注意公司内部多语言开发的成本与内耗，目前快的打车系统以java为主，也在用python、golang、c，但基本都是工具的开发。

关于架构师
以下是我认为架构师在设计时应该秉承的一些原则吧。
业务为王：技术只是手段，业务才是根本，这句话可能对技术人有些打击，但这是事实。不能为了玩技术而技术，要解决实际的问题，直接或间接的产生技术价值。
发散思考：架构不是仅解决问题就行。无论大小或简单复杂，有些点是必须要考虑的：例如单点、性能瓶颈、可能的风险、快速发现故障、快速定位问题原因、快速响应业务需求。
适度设计：架构是不断迭优化的。特别是在互联网这个行业，充满了很多机遇，也充满了很多不确定性，业务经常需要快速试错，发展速度也相当快。不能想当然的设计一套大而全的方案，期望解决所有的问题，而要随着业务的场景和发展，秉承一些基本的设计原则同时，解决最重要的问题。





---
#LMAX架构
[LMAX架构](http://www.jdon.com/42452)








---
#EAP
Level1：开始启动。形成初步的计划。
Level2：现状分析(As-Is)。分析当前的业务过程模型和系统/技术现状，作为实施计划的基线。
Level3：目标分析(To-Be)。依次进行数据架构、应用架构和技术架构，形成对目标的设计。
Level4：实现和整合计划。决定如何实现Level3中设计的目标。包括实现应用系统的详细步骤，日程表，成本-收益分析，以及整合路径。

---
#Zachman
企业架构和企业信息系统结构架构(Zachman Framework for EnterprisArchitecture and e Information Systems Architecture)
支持或封装其他事情的一种结构，尤其是作为其他的一些已经创建的东西的基础给予其骨架支持；一种外部的工作平台；脚手架；一种基本结构；组成观察显示的一系列的假象，内容，价值和实践


能够从六种视角出发，并能为每个视角在六个方面（什么内容（What）、如何工作（How）、何处（Where）、何人负责（Who）、何时（When）和为什么动机（Why））做出解答，那么此架构描述就是完备的


数据列（What）应遵从：事物——关系——事物。
功能列（How）应遵从：流程——输入/输出——流程。
网络”列（Where）应遵从：节点——连接——节点。
人列（Who）应遵从：人员——工作——人员。
时间列（When）应遵从：事件——周期——时间。其中，事件指代某一时间点，而周期代表了一段时间区间。
原因列（Why）应遵从：结果——方式——结果。其中，结果代表了目标状态，而方式则用于表示为了达成目标状态而采用的行为。

##Zachman 好处
确保每个利益相关着能够从描述的焦点考虑。
通过把每个焦点精简到每个特殊观众涉及的焦点来提升构架材料的质量。
确保每个商业需求能够追踪到技术实现。
确保商业方面不会规划出多余没用的功能。
确保技术组包含在商业组的规划中。

---
#TOGAF框架
The Open Group Architecture Framework (TOGAF) 架构框架

---
#FEA框架


---
#DoDAF 







---
[微信后台架构之美](http://segmentfault.com/a/1190000002975375)























