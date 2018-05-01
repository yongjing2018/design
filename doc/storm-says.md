# storm says  聊聊Storm
# 背景
当前storm已经在生产环境使用近8年，其中从2012年开始0.8版本开始，在稳定的运行。到2013年的时候出了0.9版本，基本上都是小的修改直到2016年4月发布1.0.0版本出现质的飞跃。 Storm曾一度作为流式计算的标准存在，几乎所有的大公司（BAT以及二线三线的公司）都有storm的身影。 

# 使用
1. 实时统计  2. 数据同步 3. 对账  4. 监控 5. 风控 6. 反作弊 等业务
实时统计： 其中常见的实时统计，即统计订单量，订单金额等最为核心的实时统计业务。

数据同步： 主要体现在mysql（canal）到hbase,日志kafka的同步到其他存储等等， 另外就是通过mq（rabbitmq）到redis等等其他方面的同步处理。

对账： 对账是业务最核心的功能

监控：针对服务器监控以及业务监控，主要处理流程，通logx将日志汇总到kafka，Storm对去kafka中的日志记录进行各种分析。

风控： 主要通过业务指定的各种指标进行风险控制，给出实时报警。

反作弊： 根据各个项指标进行预测以及风险值报警等等。


# 难点
1. 幂等性和最终一致性
数据重复处理是最麻烦的，需要采用ID进行唯一标识； 
针对无法通过ID进行唯一处理的可以采用modifyMdf来确保最终一致性。