# likesearch 模糊搜索
## 背景
针对品项的搜索需要在"goodsCode", "goodsName","goodsMnemonicCode","barcode"这4个字段中进行模糊匹配。
例如： 10501028 库存武川莜面 kcwcym;ku;cun;wu;chuan;you;mian;kucunwuchuanyoumian
当输入： 1 102 0 02 1028 都会出现该记录， 当输入k u ku 等都会出现， 输入：武川 武 （PS输入：ian可以不出现）


## 业务分析
为了简单起见，什么都不关心仅仅简单的分词而已。 按照utf8进行逐字分词即可。 会得到 k-1001 ku-1001 .... 
按理说量比较大相邻的所有组合都会有，应该是所有组合。

## 关键算法
### 1. 分词函数
### 2. 字符串分词的所有组合
```
public class TermTest {
    @Test
    public void termSplit() {
        String str = "库存武川莜面1233abc";
        int len = str.length();
        for(int k=1;k<=len;++k) {
            for(int i=0;i<len;++i) {
                if(i+k>len) break;
                //System.out.println(""+i+","+k);
                String subx = str.substring(i,i+k);
                System.out.println(subx);
            }
        }

    }
}
```
