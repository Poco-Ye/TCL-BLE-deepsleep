# TCL-BLE-deepsleep


实现核心方法是跑两个main函数

一个保存基带寄存器还有处理空包和跳频包

另一个跑正常基带和协议栈


实现方法很多芯片公司不同，deepsleep主要在interval * latency = deepslepp time 

偷着睡眠保持连接，功耗要降低，醒来时间要控制
![image](./EM%E4%BD%BF%E7%94%A8%E6%83%85%E5%86%B5.png?raw=true)

刮一部分内存不掉电，保存ACL连接和EM ral rx等buf数据，0-15排帧可以从0开始


lld_con_start->lld_con_sched->evt插入链表->设置定时器->定时器中断(20中断)->sch_arb_event_start_isr->从链表pick出evt->lld_con_evt_start_cbk->sch_prog_push->将evt时间戳设置到寄存器->等待RX或者END中断->当END中断到来->rom_lld_con_frm_isr->重新调用lld_con_sched将新的evt插入链表->周而复始

