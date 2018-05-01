# code pan 代码碎片

mysql: 数据链接
```
url: jdbc:mysql://xx.xx.xx.xx:3306/db_name?autoReconnect=true&autoReconnectForPools=true&failOverReadOnly=false&allowMultiQueries=true
    username: root
    password: abc1234
```

java： 日志
```
private static Logger log = LoggerFactory.getLogger(MysqlDao.class);
```

java: 依赖构造
```
@Configuration
@DependsOn({"splitSentenceBolt","wordCountBolt","kafkaProducerSpout"})
public class DemoTopologyBuilder {
```

sql: 创建表
```
CREATE TABLE `tbl_chain_distribution_goods` (
  `ID` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '主键ID',
  `goodsID` bigint(20) NOT NULL DEFAULT '0' COMMENT '物资ID',
  `disName` varchar(100) COLLATE utf8mb4_bin NOT NULL DEFAULT '' COMMENT '配送中心名称',
  `demandType` tinyint(4) NOT NULL DEFAULT '1' COMMENT '物资归属：0、仓库，1、店铺',
  `price` decimal(20,8) NOT NULL DEFAULT '0.00000000' COMMENT '最新采购价格',
  `purchaseUnitper` decimal(20,8) NOT NULL DEFAULT '0.00000000' COMMENT '采购单位转换率',
  `isCosted` tinyint(4) NOT NULL DEFAULT '0' COMMENT '是否到货即耗用 0：否，1：是',
  `action` tinyint(4) NOT NULL DEFAULT '0',
  `actionTime` bigint(20) NOT NULL DEFAULT '0',
  `createTime` bigint(20) NOT NULL DEFAULT '0',
  PRIMARY KEY (`ID` ,`actionTime`),
  UNIQUE KEY `uniq_key` (`groupID`,`goodsID`,`distributionID`,`demandID`),
  KEY `groupID` (`groupID`,`distributionID`,`demandID`,`categoryID`),
  KEY `disID` (`distributionID`) USING BTREE,
  KEY `demID` (`demandID`) USING BTREE,
  KEY `idx_goodsID` (`goodsID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_bin COMMENT='xxx表'
PARTITION BY RANGE (voucherDate) (
    PARTITION p0 VALUES LESS THAN (20160000) ENGINE = INNODB,
    PARTITION p2016 VALUES LESS THAN (20170000) ENGINE = INNODB,
    PARTITION p2017 VALUES LESS THAN (20180000) ENGINE = INNODB,
    PARTITION p2018 VALUES LESS THAN (20190000) ENGINE = INNODB,
    PARTITION p2019 VALUES LESS THAN (20200000) ENGINE = INNODB,
    PARTITION p2020 VALUES LESS THAN (20210000) ENGINE = INNODB,
    PARTITION p2021 VALUES LESS THAN (20220000) ENGINE = INNODB,
    PARTITION pmax VALUES LESS THAN MAXVALUE ENGINE = INNODB
);
ALTER TABLE `tbl_chain_voucher` PARTITION BY RANGE (YEAR(voucherDate)) (
     PARTITION p2023 VALUES LESS THAN (2023),
    PARTITION p2024 VALUES LESS THAN (2024),
)
```


