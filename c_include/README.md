# compile
gcc  -include stdio.h  hello.c -o hi   --std=gnu99  -Wall -g -O3

# memory check
valgrind  ./hi

