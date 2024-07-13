* `MAR`: `Memory Address Register`
* `MDR`: `Memory Data Register`
    * 写操作: 目标内存地址首先被放入 MAR，然后数据被写入 MDR，最后将 MDR 中的数据写入 MAR 指定的内存地址。

    * 读操作：目标内存地址也首先被放入 MAR，然后启动读操作，将指定内存地址的数据传送到 MDR。

# 1.2_2 各个硬件的工作原理11:56
