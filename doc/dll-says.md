# ddl says 聊聊数据表创建
这里主要说明一下针对id，gmt_modify，gmt_create三个字段的说明

# id
id很多人都不明白为什么使用，而且还是自增，另外不允许有任何的业务意义，甚至有的人在建goods表的时候错误的认为goodsID就是id。
id自增主要为了让用户不关心， id的另外一个使用就是数据库单实例的自我数据管理，另外就是在使用到通用工具的时候，就可以直接使用id，而不是xxxid。

# gmt_modify,gmt_create
这个两个字段主要可以有效的进行数据的增量处理，以及数据产生时间的定位。