# sql教程

## 目录

- **[00_环境配置.md](00_环境配置.md)**
- **[01_初始数据库.md](01_初始数据库.md)**
- **[02_基础查询与排序.md](02_基础查询与排序.md)**
- **[03_复杂一点的查询.md](03_复杂一点的查询.md)**
- **[04_集合运算.md](04_集合运算.md)**
- **[05_SQL高级处理.md](05_SQL高级处理.md)**
- **[06_综合练习.md](06_综合练习.md)**



## <font color='red'> SQL语法规范   (千万注意)</font>

1. MySQL本身不区分大小写，但强烈要求关键字大写，表名、列名用小写；
2. 创建表时，使用统一的、描述性强的字段命名规则保证字段名是独一无二且不是保留字的，不要使用连续的下划线，不用下划线结尾；最好以字母开头；
3. 关键字右对齐，且不同层级的用空格或缩进控制，使其区分开，见样例二；
4. 列名少的时候写在一行里无伤大雅；多的时候以及涉及到CASE WHEN 或者聚合计算的时候，建议分行写；个人习惯是逗号在列名前面，方便之后删除某些列，放列名后亦可；
5. 表别名和列别名尽量用有具体含义的词组，不要用a b c，不然以后review的时候会非常痛苦；
6. 运算符前后都加一个空格；
7. 当用到多个表时，请在所有列名前写上引用的表别名，不要嫌麻烦；
8. 每条命令用分号结尾；
9. 养成随手写注释的习惯，注释方法：

```
单行注释 # 注释文字
单行注释 -- 注释文字
多行注释：/* 注释文字 */
```

- 样例

```sql
-- 样例一
(SELECT flora.species_name
        ,AVG(flora.height) AS average_height
        ,AVG(flora.diameter) AS average_diameter
  FROM flora
  WHERE flora.species_name = 'Banksia'
     OR flora.species_name = 'Sheoak'
     OR flora.species_name = 'Wattle'
  GROUP BY flora.species_name, flora.observation_date)
  UNION ALL
(SELECT botanic.species_name
        ,AVG(b.height) AS average_height
        ,AVG(b.diameter) AS average_diameter
   FROM botanic_garden_flora AS botanic
  WHERE botanic.species_name = 'Banksia'
     OR botanic.species_name = 'Sheoak'
     OR botanic.species_name = 'Wattle'
  GROUP BY botanic.species_name, botanic.observation_date);
-- 样例二
SELECT botanic.species_name
       ,AVG(b.height) AS average_height
       ,AVG(b.diameter) AS average_diameter
 FROM botanic_garden_flora AS botanic
 WHERE botanic.species_name IN (SELECT species_name
                                  FROM flora 
                                 WHERE height >= 3) 
 GROUP BY botanic.species_name, botanic.observation_da;
 
-- 样例三
SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.product_type, P.purchase_price
 FROM shopproduct  AS SP 
 INNER JOIN -- product
   (SELECT product_name, product_type, purchase_price
      FROM Product ) AS P 
    ON SP.product_id=P.product_id
 WHERE P.product_type='衣服';
```



---

## 补充

- [附录1_SQL语法规范.md](附录1_SQL语法规范.md)
- [shop.sql](shop.sql)

