[TOC]

<p align="center">ððððð</p>
<p align="center"><a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-hadoop-green" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-hive-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-zookeeper-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-hbase-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-flume-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-kafka-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-spark-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-sqoop-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-flink-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-java-yellowgreen" alt="github"></a></p>

<p align="center"><a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-scala-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei"><img src="https://img.shields.io/badge/-AI-yellowgreen" alt="github"></a>&emsp;<a href="https://gitee.com/fanggaolei" align="center"><img src="https://img.shields.io/badge/-ssm-yellowgreen" alt="github"></a></p>

>æ´å¤èµæºé¾æ¥ï¼æ¬¢è¿è®¿é®ä½ègiteeä»åºï¼[https://gitee.com/fanggaolei/learning-notes-warehouse/tree/master](https://gitee.com/fanggaolei/learning-notes-warehouse/tree/master)

## 1.0â½æ°æ®åå¤

**æ°æ®ç´é¾ä¸è½½ï¼åç»å½ï¼ï¼** https://www.123pan.com/s/T1n0Vv-gTc3d

## 2.0ðååºè¡¨ç»ä¹ 

ðå½Hiveè¡¨å¯¹åºçæ°æ®éå¤§ãæä»¶å¤æ¶ï¼ä¸ºäºé¿åæ¥è¯¢æ¶å¨è¡¨æ«ææ°æ®ï¼Hiveæ¯ææ ¹æ®ç¨æ·æå®çå­æ®µè¿è¡ååºï¼ååºçå­æ®µå¯ä»¥æ¯æ¥æãå°åãç§ç±»ç­å·ææ è¯æä¹çå­æ®µã

### 2.1æ°æ®è¯´æ

&emsp;&emsp;ç°æ6ä»½æ°æ®æä»¶ï¼åå«è®°å½äºãçèè£èãä¸­6ç§ä½ç½®çè±éç¸å³ä¿¡æ¯ãç°è¦æ±éè¿å»ºç«ä¸å¼ è¡¨**t_all_hero**ï¼æ6ä»½æä»¶åæ¶æ å°å è½½ã

![image-20221109201205145](https://pic-1313413291.cos.ap-nanjing.myqcloud.com/image-20221109201205145.png)

![image-20221109201220870](https://pic-1313413291.cos.ap-nanjing.myqcloud.com/image-20221109201220870.png)

==**éæ±ï¼ä»¥roleè§è²ä½ä¸ºååºå­æ®µåå»ºéæååºè¡¨åå¨æååºè¡¨**==

### 2.2éæååºè¡¨

ðæè°**éæååº**æçæ¯ååºçå­æ®µå¼æ¯ç±ç¨æ·å¨å è½½æ°æ®çæ¶åæå¨æå®çã

**1.åå»ºä¸ä¸ªéæååºè¡¨**

```sql
create table t_all_hero_part(
       id int,
       name string,
       hp_max int,
       mp_max int,
       attack_max int,
       defense_max int,
       attack_range string,
       role_main string,
       role_assist string
) partitioned by (role string)
row format delimited
fields terminated by "\t";
```

**2.å°æ°æ®ä¸ä¼ å°éæååºä¸­**

```sql
load data local inpath '/opt/module/hive/data/hero/archer.txt' into table t_all_hero_part partition(role='sheshou');
load data local inpath '/opt/module/hive/data/hero/assassin.txt' into table t_all_hero_part partition(role='cike');
load data local inpath '/opt/module/hive/data/hero/mage.txt' into table t_all_hero_part partition(role='fashi');
load data local inpath '/opt/module/hive/data/hero/support.txt' into table t_all_hero_part partition(role='fuzhu');
load data local inpath '/opt/module/hive/data/hero/tank.txt' into table t_all_hero_part partition(role='tanke');
load data local inpath '/opt/module/hive/data/hero/warrior.txt' into table t_all_hero_part partition(role='zhanshi');

```

![image-20221109202135653](https://pic-1313413291.cos.ap-nanjing.myqcloud.com/image-20221109202135653.png)



### 2.3å¨æååºè¡¨

ðæè°**å¨æååº**æçæ¯ååºçå­æ®µå¼æ¯åºäºæ¥è¯¢ç»æèªå¨æ¨æ­åºæ¥çãæ ¸å¿è¯­æ³å°±æ¯insert+select

**1.åå»ºä¸ä¸ªåå§æ°æ®è¡¨**

```sql
create table t_all_hero(
    id int,
    name string,
    hp_max int,
    mp_max int,
    attack_max int,
    defense_max int,
    attack_range string,
    role_main string,
    role_assist string
)
row format delimited
fields terminated by "\t";
```

**2.ååå§è¡¨ä¸­ä¸ä¼ æ°æ®**

```
hadoop dfs -put data/hero/* /user/hive/warehouse/db_hive.db/t_all_hero
```

**3.å¼å¯å¨æååº**

```sql
set hive.exec.dynamic.partition=true;
set hive.exec.dynamic.partition.mode=nonstrict;
```

**4.åå»ºä¸ä¸ªå¨æååºè¡¨**

```sql

create table t_all_hero_part_dynamic(
         id int,
         name string,
         hp_max int,
         mp_max int,
         attack_max int,
         defense_max int,
         attack_range string,
         role_main string,
         role_assist string
) partitioned by (role string)
row format delimited
fields terminated by "\t";
```

**5.åå¨æååºè¡¨ä¸­æå¥æ°æ®**

```sql
insert into table t_all_hero_part_dynamic partition(role)
select tmp.*,tmp.role_main from t_all_hero tmp;
```

![image-20221109202156967](https://pic-1313413291.cos.ap-nanjing.myqcloud.com/image-20221109202156967.png)



## 3.0ðåæ¡¶è¡¨

ðåæ¡¶è¡¨ä¹å«åæ¡¶è¡¨ï¼æºèªå»ºè¡¨è¯­æ³ä¸­bucketåè¯ãæ¯ä¸ç§ç¨äºä¼åæ¥è¯¢èè®¾è®¡çè¡¨ç±»åãè¯¥åè½å¯ä»¥è®©æ°æ®åè§£ä¸ºè¥å¹²ä¸ªé¨åæäºç®¡çã

### 3.1æ°æ®è¯´æ

&emsp;&emsp;ç°æç¾å½2021-1-28å·ï¼åä¸ªå¿countyçæ°å ç«æç´¯è®¡æ¡ä¾ä¿¡æ¯ï¼åæ¬ç¡®è¯çä¾åæ­»äº¡çä¾ï¼æ°æ®æ ¼å¼å¦ä¸æ

ç¤ºå­æ®µå«ä¹å¦ä¸ï¼count_dateï¼ç»è®¡æ¥æï¼,countyï¼å¿ï¼,stateï¼å·ï¼,fipsï¼å¿ç¼ç codeï¼,casesï¼ç´¯è®¡ç¡®è¯ç

ä¾ï¼,deathsï¼ç´¯è®¡æ­»äº¡çä¾ï¼ã

![image-20221109201307808](https://pic-1313413291.cos.ap-nanjing.myqcloud.com/image-20221109201307808.png)

==**éæ±ï¼æ ¹æ®stateå·ææ°æ®åä¸º5æ¡¶**==

### 3.2åæ¡¶è¡¨åå»ºç»ä¹ 

**1.åå§æ°æ®åå¤**

```sql
CREATE TABLE t_usa_covid19(
       count_date string,
       county string,
       state string,
       fips int,
       cases int,
       deaths int)
row format delimited fields terminated by ",";
```

**2.ååå§è¡¨ä¸­æå¥æ°æ®**

```
hadoop fs -put data/us-covid19-counties.dat /user/hive/warehouse/db_hive.db/t_usa_covid19
```

**3.åå»ºåæ¡¶è¡¨**

```sql
CREATE TABLE t_usa_covid19_bucket_sort(
      count_date string,
      county string,
      state string,
      fips int,
      cases int,
      deaths int)
CLUSTERED BY(state) sorted by (cases desc) INTO 5 BUCKETS;
```

**4.ååæ¡¶è¡¨ä¸­æå¥æ°æ®**

```sql
insert into t_usa_covid19_bucket_sort select * from t_usa_covid19;
```

![image-20221109202227990](https://pic-1313413291.cos.ap-nanjing.myqcloud.com/image-20221109202227990.png)

