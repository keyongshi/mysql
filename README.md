## mysql总结

工作中遇到了比较多的mysql查询慢问题，也学习了如何处理慢查询，记录下来备忘

阅读顺序为：
1. mysql总体概述:作为一个研发，从整体上简单了解Mysql的核心
2. schema与数据类型优化
3. 索引
4. 查询优化

## 参考书籍

- 深入理解MySQL核心技术
    - Sasha Pachev在2000年到2002年期间是MySQL开发团队成员之一

- 高性能MySQL
    - PeterZaitsev曾经是MySQLAB公司高性能组的经理,  现在是Percona CEO

- 高可用性MySQL
    - CharlesBell
    - Mats Kindahl
    - Lars Thalmann
- MySQL技术内幕:InnoDB存储引擎
    - 姜承尧
    
## 参考链接    
- http://blog.jcole.us/2013/01/10/btree-index-structures-in-innodb/
- http://www.xaprb.com/blog/2015/08/08/innodb-book-outline/
- http://hedengcheng.com/