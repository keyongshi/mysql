# Schema与数据类型优化



#### 选择数据类型的基本原则

- 更小的通常更好
- 简单就好
- 尽量避免null
  除非你有一个很特别的原因去使用 NULL 值，你应该总是让你的字段保持 NOT NULL。这看起来好像有点争议，请往下看。

首先，问问你自己“Empty”和“NULL”有多大的区别（如果是INT，那就是0和NULL）？如果你觉得它们之间没有什么区别，那么你就不要使用NULL。（你知道吗？在 Oracle 里，NULL 和 Empty 的字符串是一样的！)

不要以为 NULL 不需要空间，其需要额外的空间，并且，在你进行比较的时候，你的程序会更复杂。 当然，这里并不是说你就不能使用NULL了，现实情况是很复杂的，依然会有些情况下，你需要使用NULL值。

以下一句话摘自Mysql文档里：NULL columns require additional space in the row to record where their values are NULL. For MyISAM tables, rach NULL column takes one bit extra, rounded up to the nearest byte.

MySQL Innodb 存储结构 & 存储Null值 解析：http://www.cnblogs.com/zhoujinyi/articles/2726462.html

### varchar和char类型 

### 使用枚举代替字符串类型

### 日期和时间类型

- DateTime
- TimeStamp

datetime占8个字节，timestamp占4个字节，date占3个字节

关于mysql时间类型datetime与timestamp范围
datetime类型取值范围：1000-01-01 00:00:00 到 9999-12-31 23:59:59
timestamp类型取值范围：1970-01-01 00:00:00 到 2037-12-31 23:59:59

timestamp类型具有自动初始化和自动更新的特性。有时区概念，其他的没有。

date只有年月日，没有时分秒

### 位数据类型

- Bit
- Set

## MySQL schema设计中的陷阱

- 太多的列
- 太多的关联
- 全能的枚举
- 变相的枚举

## 范式和反范式

### 范式的优缺点

### 反范式的优缺点

### 混用范式和反范式

### 缓存表和汇总表