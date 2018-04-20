# mysql2es 数据从mysql导入到es

主要通过针对mysql的表导入es中index.type中，es可以采用默认的mapping设置. 

## 处理步骤
### 第1步 批量高并发导入 
  根据createTime进行并发insert,并记录最大的insertDs， where createTime>insertDs；
  
### 第2步 实时增量同步
* 根据actionTime进行同步最新需要记录where actionTime>lastDs 
>  2.1 actionTime > insertDs（插入）
>  2.2 actionTime <= insertDs(更新)
* 在并行下可能会涉及到对应的乱序问题，所以需要针对Thread进行Hash队列化处理，即同样的ID总由一个固定的线程处理
