## 第一章
### 运算器
* `MAR` 和 `MDR` 
    * `MAR`: `Memory Address Register`
    * `MDR`: `Memory Data Register`
        * 写操作: 目标内存地址首先被放入 MAR，然后数据被写入 MDR，最后将 MDR 中的数据写入 MAR 指定的内存地址。

        * 读操作：目标内存地址也首先被放入 MAR，然后启动读操作，将指定内存地址的数据传送到 MDR。

* `ACC`: `Accumulator`
    * 累加器, 用于存放操作数, 或运算结果

* `MQ`: `Multiple-Quotient Register`
    * 商乘寄存器

* `X`: 通用操作数寄存器

* `ALU`: 和上面用于存储数据的寄存器不同, 通过电路来实现运算
### 控制器
* `CU`: `Control Unit`
    * 控制单元, 分析指令, 给出控制信号

* `IR`: `Instruction Register`
    * 指令寄存器, 存放当前执行的指令

* `PC`: `Program Counter`
    * 存放下一条指令地址, 自动+1

* `执行一条指令`
    1. 取指令, 存放到 PC 中
    2. 分析指令, 先存放到 IR 中, CU 再分析
    3. CU 执行

### 存储器
* MAR 反映存储单元的个数
* MDR = 每个存储单元的大小
* 总容量 = 存储单元个数 * 存储字长(bit)

> Eg: MAR 为 32 位, MDR 为 8 位
> 总容量 = $2^{32} * 8bit = 4GB$

* $2^{10}: K$
* $2^{20}: M$
* $2^{30}: G$ 
* $2^{40}: T$
### 性能指标
* CPU主频: CPU内数字脉冲信号振荡的频率

* CPU时钟周期: 振荡一次需要的时间(单位: 微秒, 纳秒)

* CPI(Clock cycle Per Instruction): 执行一条指令所需的时钟周期数
    * CPU性能不能只看主频, 还应该看 CPI

* IPS(Instructions Per Second): 每秒执行多少条指令

* FLOPS(Floating-point Operations Per Second): 每秒执行多少次浮点运算
    * KFLOPS
    * GFLOPS
    * TFLOPS
    * K=Kilo=10^3, M=Million=10^6, G=Giga=10^9, T=Tera=10^12 

> 若A, B两个CPU的平均CPI相同, A的主频比B高, A一定更快吗
> 答: 不一定 
## 总线
