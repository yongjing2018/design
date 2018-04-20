# mysql2es 数据从mysql导入到es

## 背景
主要通过针对mysql的表导入es中index.type中，es可以采用默认的mapping设置. 

## 设计方案
![Mysql2Es导入](./images/Mysql2Es导入.png)
* PS：如果线程数发生修改，启动重启后会取最小更新的时间
* 数据写入采用，直接PUT（存在就更新，不存在就插入）

### 第1步 批量高并发导入 
  根据createTime进行并发insert,并记录最大的insertDs， where createTime>insertDs；
  
### 第2步 实时增量同步
* 根据actionTime进行同步最新需要记录where actionTime>lastDs 

* 在并行下可能会涉及到对应的乱序问题，所以需要针对Thread进行Hash队列化处理，即同样的ID总由一个固定的线程处理


## 分表的数据同步
可以采用shell脚本，采用时间点切片ds1-ds2，进行
``` sql
insert into dstTable(field1,field2,...) 
select v1,v2,... 
from srcTable 
where activeTime>=ds and activeTime<ds2
  and createTime>=20180000 and createTime<20190000
```
