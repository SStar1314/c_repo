# automake examples

## Case 1 : simple example
~/amhello-1.0 % ./configure --prefix ~/usr
…
~/amhello-1.0 % make
…
~/amhello-1.0 % make install
…


## Case 2 : prefix changes build & installation directory
~/amhello-1.0 % ./configure --prefix ~/usr CC=gcc-3 \
CPPFLAGS=-I$HOME/usr/include LDFLAGS=-L$HOME/usr/lib


## Case 3 : config.site changes default variables
If a file named prefix/share/config.site exists, configure will source it at the beginning of its execution.
~/amhello-1.0 % ./configure --prefix ~/usr
configure: loading site script /home/adl/usr/share/config.site
…


## Case 4 : change all build output files to build directory
~ % tar zxf ~/amhello-1.0.tar.gz
~ % cd amhello-1.0
~/amhello-1.0 % mkdir build && cd build
~/amhello-1.0/build % ../configure
…
~/amhello-1.0/build % make
…

## case 5 : run the Autotools to instantiate the build system
~/amhello % autoreconf --install
configure.ac: installing './install-sh'
configure.ac: installing './missing'
configure.ac: installing './compile'
src/Makefile.am: installing './depcomp'



