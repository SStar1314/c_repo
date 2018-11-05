# command
stap  tps.d

## systemtap支持4种数据类型, 分别为long整型, 字符串, 数组, 统计类型.
stap  -g  test.stp
stap  -g  test1.stp


stap  -g  test2.stp

### 进程启动
stap -e 'probe process("pgsql9.3beta2/bin/postgres").begin {printf("%s, %s, %d, %d\n", execname(), pp(), pid(), cpu()); exit();}'  
### 进程结束
stap -e 'probe process("/opt/pgsql9.3beta2/bin/postgres").end {printf("%s, %s, %d, %d\n", execname(), pp(), pid(), cpu()); exit();}'  
### 系统调用
stap -e 'probe process("/opt/pgsql9.3beta2/bin/postgres").syscall { printf("%s, %d, %s, %d, %d, %d\n", execname(), $syscall, pp(), pid(), cpu(), $arg1); } probe timer.s(1) { exit(); }' 


