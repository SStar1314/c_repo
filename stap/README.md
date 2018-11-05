# command
stap  tps.d

## systemtap支持4种数据类型, 分别为long整型, 字符串, 数组, 统计类型.
stap  -g  test.stp
stap  -g  test1.stp


stap  -g  test2.stp

### stap -e 'probe process("pgsql9.3beta2/bin/postgres").begin {printf("%s, %s, %d, %d\n", execname(), pp(), pid(), cpu()); exit();}'  
### stap -e 'probe process("/opt/pgsql9.3beta2/bin/postgres").end {printf("%s, %s, %d, %d\n", execname(), pp(), pid(), cpu()); exit();}'  


