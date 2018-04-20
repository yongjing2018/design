# rabbitmq-storm-es 讲数据从rabbitmq读取通过storm处理后写入到ES

## 用例设计

### 场景一 扣库存处理
#### 1.1 造消息写入到topic： scm.shop.order
PUT "orderID 1001"
PUT "orderID 1002"
#### 1.2 storm提交topology
1. 订阅topic：scm.shop.order
2. 根据orderID从mysql读取订单数据
3. 进行扣库处理
4. 扣库成功将消息写入到topic：scm.shop.order.feldback

