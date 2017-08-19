## 入坑
背景：
1. 一张表T有一个UK(A,B)，现有系统有Mybatis方法insert(Bean)，Bean中有a，b两个字段，对应的sql语句：insert into T(A,B) values (#{a},#{b})
2. 表T中增加了字段C允许null默认值"Default"，并扩张UK为UK(A,B,C)
3. Bean中增加了C字段，更改为insert into T(A,B,C) values (#{a},#{b},#{c})，而原来使用insert(Bean)方法的老逻辑中并没有插入c字段的值，也就是说c字段是null，所以sql语句就变成了insert into T(A,B,C) values ("str1","str2",null)

坑点：
SQL_INSERT语句可以重复插入数据，也就是说数据库会出现以下记录

| id   | A    | B    | C    |
| ---- | ---- | ---- | ---- |
| 1    | a    | b    | null |
| 2    | a    | b    | null |

为什么UK(A,B,C)没有发挥作用？按照我们的构想，SQL_INSERT重复执行时 应该抛出 `Duplicate key` 的异常。

## 调查

查了一下，发现MySQL官方文档上其实已经明确说了这一点， 唯一性索引是允许多个 NULL 值的存在的
> For all engines, a UNIQUE index permits multiple NULL values for columns that can contain NULL

[官方文档链接在此](https://dev.mysql.com/doc/refman/5.7/en/create-index.html)

## 出坑
- 将表T中的字段C设置为not null default "Default"
- 在调用SQL_INSERT时，C设置默认值"Default"，也就是说insert(Bean)方法中Bean的c字段不能为null，考虑到原有逻辑里很多地方都使用了insert(Bean)方法，为了统一收口，将c字段的默认值设置为"Default"
```
private String c = "DEFAULT";
```

## 其他
MySQL官网上也有蛮多人讨论过这个问题，一部分人认为这是MySQL的bug， 另一部分则认为是一个feature，附上链接。
https://bugs.mysql.com/bug.php?id=8173
