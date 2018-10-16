# compile
gcc  getenv.c  -o  getenv -lm -g -Wall -O3

# execute
reps=10 msg="Ha" ./getenv 
msg="Ha" ./getenv
reps=20 msg=" " ./getenv

