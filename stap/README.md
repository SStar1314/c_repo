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
### 函数
stap -e 'probe process("ls").function("*").call {  
           log (probefunc()." ".$$parms)  
           }' \  
       -c 'ls -l' 

###  more examples
stap -x  ${pid} -e 'probe process.syscall {printf("%s, %s, %d\n", pp(), execname(), $syscall); }' 
stap --download-debuginfo=yes -e 'probe process("/usr/local/lib/libevent-1.4.so.2.2.0").function("*") { printf ("%s, %s, %s\n", pp(), execname(), $$vars); } probe timer.s(1) {exit();}'  
stap --download-debuginfo=yes -e 'probe process("/usr/lib/libcblas.so").function("*") { printf ("%s, %s\n", pp(), execname()); } probe timer.s(1) {exit();}'
stap -e 'probe process("/usr/sbin/rpc.idmapd").library("/usr/local/lib/libevent-1.4.so.2.2.0").plt { printf ("%s, %s\n", pp(), execname()); } probe timer.s(1) {exit();}'  

### procfs
 stap --vp 05 -e 'probe procfs.read { $value = "abc\n"; }'
 stap --vp 05 -e 'probe procfs("digoal").read { $value = "abc\n"; }'
==>
ll /proc/systemtap/stap_c6373a2dc49ccd7f60f51cb02d421026_1078/
lsmod|grep stap

 stap --vp 05 -e 'probe procfs("digoal").write { printf("%s", $value) }'
==> 
ll  /proc/systemtap/stap_10bf2c7debb5d11ceba890b9aa1f1d97__828/digoal
echo  1 >   /proc/systemtap/stap_10bf2c7debb5d11ceba890b9aa1f1d97__828/digoal

 stap --vp 05 -e 'probe procfs("digoal").read { $value = "abc\n"; } probe procfs("digoal").write { printf("%s", $value) }'  
==> 
ll /proc/systemtap/stap_b1c04c3c9a55d7a90f0cb0b9634d6e85_1585/digoal

