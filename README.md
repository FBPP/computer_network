# 序章：计算机网络概述
### 1、局域网，广域网，internet
+ 局域网：在同一个网段，使用交换机连接的计算机共同组成一个局域网
+ 广域网：距离较远，不在同一个网段的网络
+ internet：有各个国家的ISP（电信，联通等）相互连接组成的全球互联的网络
### 2、数据包和数据帧
+ 数据帧包含源端口和目的端口和数据
+ 数据包包含数据的源IP地址，目的ip地址，数据  
	+ [data][15.0.0.2][16.0.0.2]
+ 数据帧包括数据包+起始mac地址，终止mac地址，FCS
	+ [data][15.0.0.2][16.0.0.2][mc1][mc2]
### 3、网络设备
+ 交换机：连接同一个局域网中计算机
+ 网关：在一个局域网中的数据出口和数据入口
+ 路由器：在互联网中发送和传输数据的中间设备
+ DNS服务器：查询用户发来的域名对应的ip地址返回给用户
### 4、osi参考模型
+ 应用层：能产生网络流量的程序
	+ 应用程序配置错误
+ 表示层：传输数据加密解密，压缩处理（二进制，ASCII）
+ 会话层：两台计算机之间建立会话
+ 传输层：可靠传输，不可靠传输，流量控制
+ 网络层：选择数据往哪里走，最佳路径，规划ip
	+ 配错ip，子网掩码，网关，路由器没有配置到达目标网络的路由
+ 数据链路层：帧的开始结束，透明传输，差错校验
	+ MAC冲突，ADSL欠费，网速没有协调一致，计算机连接到了错误的vlan
+ 物理层：接口标准，电器标准，传输介质
	+ 没有连接网络，发送接收数据包
### 5、计算机网络的性能指标
+ 速率：连接在计算机网络的主机在数字信道上每秒传输bit的位数
+ 带宽： 数据信道所支持的最高速率
+ 吞吐量：单位时间内某个网络的数据量
+ 时延 = 发送时延+传播时延+排队时延+处理时延
+ 发送时延 = 数据块长度（bit）/带宽
+ 时延带宽积：单位时间在网络中的数据量
+ 往返时间：从发送数据，到发送方接收到接收方确认的时间
+ 信道利用率：有数据通过的时间/(有+无)数据通过的时间
# 第一章：物理层
### 1、数据通信
+ 数据：运送消息的实体
+ 信号：数据电器或电磁的表现
	+ 数字信号：参数的取值是离散的
	+ 模拟信号：参数的取值是连续的
+ 码元：代表不同离散数值的基本波形
	+ 一码元可以携带nbit信息量
+ 信道通信
	+ 单向通信：一个只能发，一个只能收
	+ 半双工：在同一时刻，一个只能发，一个只能收
	+ 全双工：在同一时刻，两边既可以发，也可以收
+ 基带信号，带通信号
	+ 基带信号：来自信源的信号，直接表达信息，不便于远距离传输
	+ 带通信号：吧基带信号提高频率，便于远距离传输 
	+ 把基带信号调成带通信号的方法
		+ 调幅 ： 0：无频率，1：有频率
		+ 调频：0：频率小，1：频率大
		+ 调相：0：正弦波，1：余弦波
+ 编码格式
	+ 单极性不归零码：0V：0，xV：1
	+ 双极性不归零码：-XV ： 0 ，XV ： 0
	+ 单极性归零码：不变：0，高电压：1，出现数据之后会归零
	+ 双极性归零码：高电压：1，低电压：0，出现数据之后归零
	+ 曼彻斯特：低-高：0，高-低：1，能够区分0是否是数据
	+ 差分曼彻斯特：bit与bit之间有信号跳变，下一个bit为0，无信号跳变，下一个bit为1，能够区分0是否是数据
+ 信道极限容量
	+ 奈氏准则：没有电磁干扰，传输速率也要有上限，只作用于模拟信号
	+ 香农公式：减少速率可以减少噪声干扰
### 2、信道复用技术
+ 目的是增加信道的利用率，在高速传输线路上传输多个用户数据
+ 频分复用：按照信号的频率区分用户数据
+ 时分复用：按照接收的顺序区分用户数据
	+ 统计时分复用，在每个数据里面加标记区分用户数据
+ 波分复用：就是光的频分复用
### 3、数字传输系统
+ E1链路欧洲的
+ T1链路北美的
+ 中国用的是E1
# 第二章：数据链路层
### 1、数据链路层的信道类型
+ 点到点信道：一对一
+ 广播信道：一对多
### 2、帧
+ 数据链路层传送的是帧
+ 帧有帧头和帧尾，物理层地址，校验码
+ 如果校验码和数据不相符，接收方会丢到该数据帧
### 3、数据链路层解决的三个基本问题
+ 封装成帧
	+ 用特殊的字符表示帧的开始结束
+ 透明传输
	+ “ESC”转义字符，十六进制编码1B
	+ 如果数据中出现和帧头帧尾相同的数，则在它前面加上“ESC”
	+ 如果数据中出现数据“ESC”，就在它前面再加一个“ESC”
	+ 接收时会去掉“ESC”
+ 差错控制
	+ 循环冗余校验
	+ 对数据做除法，余数作为FCS
	+ 不能发现哪一位错了
	+ 除数越长，检测出错误的成功率越高
### 4、点到点通讯的数据链路层
+ 电话线接入internet，使用ppp协议
+ ppp协议不具备纠错功能，流量控制功能
+ 点到点链路如果使用ppp协议，则MAC地址固定为FF（因为只有一个目的地，一条路径）
+ ppp协议三个组层部分
	+ 可以用于异步串行或同步串行介质
	+ 使用LCP（链路控制协议）建立并维护数据链路层连接（身份验证，拨号上网，计费，欠费）
	+ NCP（网络层控制协议）允许在点到点连接上使用多种网络层协议
+ ppp协议的帧格式
	+ F | A |  C |  协议  | ip数据报 |   FCS |  F
	+ 7E| FF| 03 |        | 信息    |	  | 7E
	+ 1 | 1	| 1  | 2      |<=1500   | 2    |    1
+ ppp的透明传输
	+ 字节传输流
		+ 将信息中的7E改成两个字节序列{7D,5E}
		+ 将7D改成{7D，5D}
		+ 在ASCII控制字符（<20）的字符前加7D
	+ 二进制传输
		+ 发现5个连续的1后面加一个0
### 5、广播通讯的数据链路层   
+ csma/cd协议：载波监听多点接入/碰撞检测
	+ “多点接入”：许多计算机连在一根总线上
	+ “载波监听”发送数据前，检测总线上是否有其他计算机发送数据，如果有，暂时不发送，以免发生碰撞
	+ “碰撞检测”当两个信号相互碰撞时，两个信号电压摆动值会增大，导致总线上的信号严重失真，当有计算机接收到碰撞信号时，并且摆动电压大于一定门限时，这检测到发生碰撞
	+ “碰撞处理”检测到发生碰撞后，所有正在发送信号的计算机停止发送，等待一个随机时间继续发送。
	+ 只能进行半双工通信，不能全双工
+ 争用期：最先发送数据帧的站，在发送数据后最多经过的时间，就知道是否发生碰撞
	+ 10MB/s以太网，争用期可发送64字节
+ 二进制指数类型的退避算法
### 6、以太网局域网
+ 只要满足csma/cd,都叫以太网 
+ 以太网的帧格式
	+ 目的MAC地址 6 源MAC地址 6 类型（表示上层的协议） 2 数据46~1500 FCS 4
+ 扩展以太网
	+ 使用光纤可以将100m扩展至几公里
	+ 集线器级联 使网络中的计算机数量增加，但是效率减少，变成了一个大的冲突率
+ 优化以太网
	+ 网桥：记录源MAC地址是在哪边的，然后如果同一边的集线器的计算机发送数据，网桥拦截其往另一边通过
	+ 交换机：随着网桥的发展，它不再连接集线器，而是计算机，就变成了交换机，交换机的口可以存储数据帧队列，交换机的网是全双工，发送数据帧互不干扰（安全），每个口独立带宽，基于MAC地址转发，能学习MAC地址表。
+ 高速以太网
	+ 速率达到100MB/s被称为高速以太网，工作在全双工模式下
+ 吉比特以太网 
	+ 网速达到1GB/s，可以在全双工和半双工（不需要csma/cd协议）下工作
+ 10吉比特以太网
	+ 10GB/s,全双工，跨全校园，全企业
# 第三章：网络层
+ 网络层负责呢在不同网络之间尽力转发数据包，基于数据包第IP地址转发
	+ 不负责重传，不负责顺序
+ 网络层将传输层的数据段（分组）添加目标ip地址和源ip地址
+ 静态路由器器上的路由表记录了：如果到目标ip地址，下一跳的路由ip地址是什么
+ 网关：路由器的每个口（网卡）都有ip地址和MAC地址，和一个网段连接的一端的网段与此网段相同，如果和非路由器的网段连接，此端为网关
### 1、网络层如何转发数据包
+ 用子网掩码判断 目的ip和源ip是否在同一个网段（使用目的ip地址和本机的子网掩码做与运算，和自己网段作对比）
	+ 如果在同一网段，则由ARP协议广播获取目的ip地址的MAC地址，并由数据链路层按照MAC地址的形式封装成帧传输
	+ 如果不是一个网段的，由ARP协议广播获取网关的ip地址对应的MAC地址，所以如果计算机想和另一个网段的计算机通信，则必须配置网关，不然不能使用ARP协议发送网关的ip地址解析广播
### 2、网络层协议
+ ARP协议，向一个网段内每台计算机和网关发送广播（MAC地址是全F），目标ip地址的计算机或网关收到后，返回该设备的MAC地址
	+ ARP协议是数据通信之前的工作，为IP协议提供服务
	+ ARP缓存，当计算机收到返回的MAC地址后会在缓存中存储目标IP地址对应的MAC地址，这样以后再发就不用再发送ARP广播了，动态缓存一段时间不使用就会从缓存中删除
	+ ARP欺骗，当计算机收到目标不是自己IP地址的ARP广播时，返回自己的MAC地址给源计算机，从而导致源计算机的ARP缓存中缓冲的是目的IP和错误计算机MAC地址之间的对应关系
+ icmp协议
	+ 功能：检验网络层是否畅通
	+ ping命令 time 查看延迟，TTL 数据包的生存时间，每当数据包经过一个路由器，TTL减一，如果TTL等于0，则该数据包被路由器丢弃，这么做可以防止数据包循环传输占用带宽
	+ 如果ping命令时长过高，说明网络不畅通
	+ 如果没有设置网关，ping则计算机会返回“destination host unreachable”
	+ 如果ping路由器没有设置到达目的ip的路由表，会从路由器返回“destination host unreachable”
	+ 如果ping返回数据包的路由器没有设置返回ip的路由表，则请求超时
+ igmp协议
	+ 点对点，广播，多播 = 组播
	+ 多播：让多组计算机绑定多组多播地址，这样可以按照多播地址分别发送多播数据包，多播不建立会话，不能控制快进、倒退等
	+功能：安装在路由器的接口上，每隔一段时间检测该网段的计算机是否绑定多播地址，如果没有计算机绑定，就通知上个路由器不要发送多播数据包
+ ip协议
### 3、ip数据包结构
+ 版本：0~3bit 表示ipv4或ipv6
+ 首部长度：4~7bit 规定首部有多长（因为首部有可变长度部分）
+ 区分服务：8~15bit 区分数据包的优先级（因为有的数据包是着急的（比如电话）有的是不着急的（比如邮件）），路由器设置区分服务的优先级，选择哪些数据包先转发，哪些后转发
+ 数据包总长度：16~31bit 一个数据包的最大为2^16-1=65535字节
	+ 数据包分片：因为数据包最大字节超过数据链路层最大传输单元（1500字节）所以要分片，才能让数据链路层传输，数据包不分片，数据最大不能超好1480个字节（1500-20（首部长度））
+ 标识：32~47bit 为每个分片添加同一标识，为了说明他们数据同一数据包
+ 标志：48~50bit 标志该数据帧是分片还是完整数据包，占三位，第一位尚未定义，第二位 1：不允许分片 0：允许分片，第三位 1：后面还有分片 0：最后一个分片
+ 片偏移：51~63bit 记录了每个片的第一个数据在整个包的数据的第几个字节的位置
+ 生存时间：64~71bit 即TTL
	+ 默认TTL：linux 64，windows128，unix 255
+ 协议号：72~79bit 标识用的协议
+ 首部检验和：80~95bit 检验首部是否发生错误
	+ 先将首部所有的数按16位划分，在对所有的16位数反码算数运算求和，再取反，得到16位校验和放到首部校验和字段中，接收方对首部进行相同的运算，如果最终结果为0，则保留数据包，否则丢弃。
+ 源ip地址 96~127bit
+ 目的ip地址 128~159bit
+ 可选字段（长度可变）+ 填充 ：160~191bit 一般不用，如果用的话就是为了增加ip数据包的功能，如果可变部分不够4个字节，用0填充。ipv6没有此部分
+ 数据部分
### 4、ip协议
+ 所有能让路由器学习路由表的，都叫IP协议
+ 网络畅通的条件：数据包有去有回
	+ 网关
	+ 路由表必须知道到每个网段下一跳的路由
+ 静态路由需要告诉路由器说有没有直连的网络下一调给谁
	+ 缺点：不适用于大型复杂的网络，不能自动适应网络的变化
+ 动态路由  
	+  RIP协议 每个路由器周期性广播路由表给其他相邻路由器，接收方会在路由表的跳数上加一，默认路径选择最短跳数，每隔30秒广播一次
		+  最大跳数15，大于则默认为网络不可到达，不适合大型网络
	+ OSPF协议 默认路径选择带宽最高
# 第四章：传输层
### 1、TCP协议
+ 又叫传输控制协议
+ 需要将传输的数据分段传输时，就要用到TCP
+ 需要建立会话 有流量控制功能，拥塞控制功能
+ 可靠传输
+ 一对一
+ 提供全双工通信
+ 面向字节流
+ 如访问网站，传文件
### 2、UDP协议
+ 又叫用户报文协议
+ 一个数据包就能够完成数据通信，即不需要分段时，就要用UDP
+ 不需要建立会话（无连接的） 不需要流量控制，无拥塞控制
+ 不可靠传输
+ n对n
+ 如DNS服务器的域名解析，qq聊天，广播，多播
### 3、应用层协议和传输层协议
+ 应用层协议 = 传输层协议+端口
+ 默认端口如下
+ http = TCP + 80
+ https = TCP + 443
+ RDP = TCP + 3389
+ FTP = TCP + 21
+ 共享文件夹 = TCP + 445
+ SMTP = TCP + 25
+ POP3 = TCP + 110
+ telnet = TCP + 23
+ MSQL SERVER = TCP + 1433
+ DNS = UDP + 53
### 4、服务和应用层协议
+ 服务 = 应用层协议 + 侦听
+ 侦听客户端发来的数据包中的 传输层协议 + 端口
+ 客户端使用ip地址定位服务器，使用目标端口定位服务
+ 可以在服务器的网卡设置只开发必要端口，实现服务器的网络安全
### 5、端口
+ 0 ~ 65535
+ 熟知端口 0 ~ 1023
+ 登记端口 1024 ~ 49151
+ 客户端端口 49152 ~ 65535
### 6、UDP数据包格式
+ UDP首部 8个字节
	+ 源端口 2字节 目的端口 2 UDP数据包长度 2 校验和 2
+ UDP伪首部（为了凑够20字节计算检验和） 12字节 
	+ 源ip 4 目的ip 4 ，0 1，协议号 1，udp长度 2 
+ 数据如果不是4字节的倍数后面用0填充 
### 7、TCP的面向字节流传输
+ 不关源数据是字节还是bit的，都按照字节的方式传输
+ TCP缓存：在发送端和接收端都有缓存区，发送缓存会从源数据中按顺序复制若干字节，接收缓存会往目的应用按循序复制若干字节
+ TCP连接的端点叫做套接字（socket）
	+ socket = ip地址：端口 
### 8、TCP是如何实现可靠传输
+ 停止等待协议
	+ 计算机 A，计算机 B，数据包 M；
	+ 无差错情况：A发M1，B返回给A“确认收到M1”，A发M2，B返回给A“确认收到M2”
		+ 只要A不发，B就一直等，只要B不发，A就一直等
	+ 超时重传：A发M1，B丢弃有差错的包，A等待RTT时间（往返时间）长一点，A重发M1，B返回给A“确认收到M1”，A发M2 
	+ 确认丢失：A发M1，B返回给A“确认收到M1”，“确认收到M1”在传输时丢失，A重发M1，B收到第二个M1，B丢失重复的M1，B返回给A“确认收到M1”
	+ 确认迟到：A发送M1，B返回给A“确认收到M1”，A等待超时，A重发M1，B返回给A“确认收到M1”，A收到“确认收到M1”，A发M2，A收到迟到的“确认收到M1”，A什么也不做
	+ 这种可靠传输的协议成为ARQ（自动重传请求），表明重传的请求是自动的，接收方不需要请求发送发重传错误的数据包，发送方会自动发送出错数据包
	+ 优点：简单，缺点：信道利用率低（大部分时间都在等）
+ 改进：流水线传输：就是在等的时候直接发下一包，这样一直发包，边发	边等，提升信道利用率
	+ 连续ARQ协议：维护一个发送窗口，发送窗口里包含n个包，这n个包可以流水线传输，并且收到最前一个数据包的接收信息后，发送窗后后移
	+ 累计确认：接收方只返回连续接收数据包中最后的包的确认信息，比如1，2，3，5，6，收到，只返回3收到，发送方需要重传4，5，6
+ 以字节为单位的滑动窗口
	+ 发送窗口的大小根据数据包中TCP首部的窗口大小来分配
	+ 作用于缓存，本质是个队列
	+ 发送窗口连续发送窗口里面的若干字节组成的若干数据包，知道收到接收方的确认包，会根据包中的确认号，将确认号之前的字节出队，并从缓存中删除，并将缓存中剩余的数据入队
	+ 接收方在发送确认接收包之后，会将接收到信息出队，应用程序会读取这些字节 
	+ 如果因为丢包造成接收到的数据是间断的，接收方会发送选择性确认给发送发，发送方会再发间断的数据
+ 超时重传时间的选择
	+ 因为网络的不稳定性， 重传时间需要做调整以适应网络
	+ RTTs（新） = （1-α）* RTTs（旧）+ α * （新的RTTs样本）
	+ 网速变化越大α的值越大，反之越小，	一般为1/8 
### 9、TCP报文段首部
+ 源端口 2，目的端口 2
+ 序号(seq) 4 表示该数据包的第一个字节在整个文件的第几个字节
+ 确认号(ack) 4 告诉发送者下一次发送的数据包的序号
+ 数据偏移 4bit 表示从第几个字节开始是数据域，保留 6bit 没啥用，URG 1bit 发送优先级 1表示高 先传，ACK 1bit 标记位 0：确认号无效 1：确认号有效， PSH 1bit 接收优先级 1表示高 直接放到接收缓存的最前面，RST 1bit 1：异常中断数据包，SYN 1bit 1：建立会话的数据包 0：非建立会话的数据包，FIN 1bit 1释放连接数据包
+ 窗口大小 2 表示该计算机的最大接收窗口，双方会根据对方的窗口大小分配相同大小的发送窗口
+ 校验和 2 校验范围是首部+数据 和UDP一样 ，加伪首部，协议号改成TCP的协议号（6）
+ 紧急指针 和URG配合使用，当URG为1时 紧急指针中的值指向数据中的位置为需要紧急发送的数据的末端
+ 选项 可变长度 可有可无 0bit填充（4字节对齐）
### 10、TCP协议如何实现流量控制
+ 由于双方缓存的处理速度不同，可能接收方处理不过来
+ 接收端根据当前的未填数据的窗口大小适当调整发送端的发送窗口大小
+ 避免窗口为0之后，接受端的“窗口恢复”的数据包丢失，发送端会定时检验接受端的窗口大小
### 11、TCP协议如何实现拥塞控制
+ 出现拥塞后网络的丢包会严重，直至吞吐量变为0
+ 慢开始算法
	+ 拥塞窗口 连续发送数据包的窗口 
	+ 门限 ssthresh 
	+ 使用拥塞窗口从1开始先指数后线性增长的方式，调整拥塞窗口的大小，当指数增长达到ssthresh后，开始线性增长，当出现丢包情况时，将ssthresh = 当前拥塞窗口的值/2 在让拥塞窗口从1开始增长
+ 快重传 当接收方收到有间断的数据包后，会发送连续3个相同的确认包
+ 快恢复 如果发送方连续的接收到接收方发来的3个确认包 怎讲拥塞窗口直接设置为从新的ssthresh开始的线性增长
+ 发送窗口的上限 = min（接收窗口，拥塞窗口）
### 12、TCP协议的连接管理
+ 传输层连接的三个阶段 建立连接 数据传输 连接释放
+ 三次握手建立连接
	+ A->B 建立连接请求 SYN = 1 ACK = 0 seq = x 
		+ 状态 A:SYN-SENT B:LISTEN
	+ B->A 确认建立连接 SYN = 1 ACK = 1 seq = y ack = x + 1
		+ 状态 A:SYN-SENT B:SYN_RCVD
	+ A->B 确认收到B的确认 ACK = 1 seq = x + 1 ack = y + 1 
		+ 状态 A：ESTABLISHED B收到后 ESTABLISHED
+ 四次挥手释放连接
	+ A->B 连接释放请求 FIN = 1 seq = u
		+ A:FIN-WAIT-1 B：ESTABLISTHED 
	+ B->A 确认收到请求 ACK = 1 seq = v  ak - u + 1
		+ A:FIN-WAIT-1 B:CLOSE-WAIT
		+ A收到后进入FIN-WAIT-2
	+ B在关闭进程之后发送B->A 关闭请求 FIN = 1 ACK = 1 seq = w ack = u+1
		+ B：LAST-ACK
	+ A->B 确认关闭 ACK = 1 seq = u+1 ack = w+1
		+ A：TIME-WITE 等待2MSL
# 第五章：应用层
### 1、域名服务DNS
+ 使用DNS服务器 将域名解析成ip地址
+ 什么是域名 
	+ 根 .
	+ 顶级域名 com edu cn 
	+ 二级域名 baidu google
+ 域名注册
+ 域名解析的过程
	+ 根DNS服务器
	+ 分布式查询
+ 安装自己的DNS服务器
	+ 为了解析内网的域名
	+ 降低internet域名解析流量
	+ 域环境
### 2、动态主机分配DHCP
+ 使用DHCP服务器动态的分配IP地址 子网掩码 网关等配置信息
+ 计算机设置成自动获取ip地址和DNS 会发送广播包 DHCP服务器收到后会从地址池中选择一个发回去，如果客户机确认使用这个地址 ，则DHCP服务器会将配置信息发送给该客户机
+ DHCP服务器必须是静态ip地址 
+ 租约 获取ip地址的生命周期 如果没有在此期间重新申请 怎退回该IP地址
+ DHCP服务器会优先将客户机原来的ip地址分配给它（前提是该IP地址没有被占用）
+ 跨网段地址分配
+ 在网关上配置DHCP服务器的IP地址，并由该网关向DHCP服务器发送请求 获得IP地址
### 3、文件传输协议FTP
+ FTP有两个TCP连接 一个是控制连接 一个是数据连接
+ 控制连接 标准端口为21 用于发送FTP命令
+ 数据连接 标准端口为20，用于上传下载数据
+ 数据连接的建立：
	+ 主动模式：服务器从20端口主动向客户端发起连接
	+ 被动模式：服务器指定范围内的某个端口被动等待客户端发起连接
+ FTP的传输模式 
	+ 文本模式：ASCII码的文本序列传输
	+ 二进制模式： 以二进制序列传输
+ 服务端如果有防火墙，最好使用主动模式只打开20和21端口即可
### 4、远程终端协议telnet
+ 安装了telnet服务器的计算机可以被远程管理
### 5、远程桌面协议RDP
+ 仅用于微软操作系统
### 6、超文本传输协议http
+ www 分布式 万维网 
+ 网站的url 协议 域名 端口 路径
+ 网站的标识 不同端口 不同的地址 不同的域名
+ web代理服务器 代理网站 
	+ 节省访问internet的带宽
	+ 可以使用代理服务器让同网段的更多不能上网的计算机上网（访问网站）
	+ 绕过防火墙
	+ 防跟踪
+ http和https的区别 https更加安全
	+ https://baijiahao.baidu.com/s?id=1629455363537331894&wfr=spider&for=pc 
### 7、电子邮件协议
+ 发收双方是由双方各自的邮局发收，并发送给客户端
+ SMTP 发邮件协议
+ POP3 收
+ IMAP 收
