# kaDesign KA用户设计
# 1背景
有的集团门店只有1个，有的集团门店数达到300+， 有的集团门店数仅仅10个，但是营业额达到10w+，所以就需要从某个维度来定义什么是KA用户
KA用户定义： 营业额在10w+以上的都叫KA用户。

# 2数据管理
有的集团开始就能确定为KA用户，但是有的集团是发展成KA用户的，因此就需要一套方案进行KA环境的管理。

## 2.1 KA用户创建方式
1. 确定KA用户
2. 开通KA用户并内部线会调用供应链initParam服务
3. 创建DB并配置canal以及client同步ES
4. 修改admin中KA用户对应集团的group-db路由关系
5. 修改initParam参数

## 2.2 数据迁移
需要将数据以groupID的映射逻辑


