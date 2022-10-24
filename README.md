# TCL-BT-deepsleep

这个是极度保密的东西，只能透露一点点

实现核心方法是跑两个main函数

一个保存基带寄存器还有处理空包和跳频包

另一个跑正常基带和协议栈


实现方法很多芯片公司不同，deepsleep主要在interval * latency = deepslepp time 

偷着睡眠保持连接，功耗要降低，醒来时间要控制，这个是比较核心的东西，我们的参数非常美丽
